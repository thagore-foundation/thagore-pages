---
title: Phân tích dragon_ice_clientbuildV1.2 – Trojan/Stealer với cơ chế Persistence đa lớp
titleEn: Analysis of dragon_ice_clientbuildV1.2 – A Trojan/Stealer with Multi-layer Persistence
excerpt: Báo cáo phân tích kỹ thuật mẫu file dragon_ice_clientbuildV1.2 cho thấy hành vi drop payload, giả mạo Windows service, thiết lập persistence nhiều lớp và đánh cắp dữ liệu trình duyệt.
excerptEn: This report provides a technical analysis of dragon_ice_clientbuildV1.2, revealing payload dropping, Windows service masquerading, multi-layer persistence, and browser data theft behaviors.
date: 2025-12-30
author: Thagore Security Team
tags: ["malware-analysis", "trojan", "stealer", "windows", "persistence", "pyinstaller", "incident-response"]
image: /content/baocao_malware.png
---

# Phân tích kỹ thuật dragon_ice_clientbuildV1.2: Trojan/Stealer ngụy trang “Windows Audio Service”

**Threat Level (Mức độ đe doạ):** Critical ⚠️  
**Classification (Phân loại):** Trojan Dropper · Information Stealer · Multi-layer Persistence  
**Platform (Nền tảng):** Windows  
**Verdict (Kết luận):** Malicious (Độc hại)

> **Thagore Security Team – Nhận định nhanh:**  
> “Không còn mức ‘nghi’. Đây là chuỗi malware hoàn chỉnh: unpack → persistence → credential/browser access → exfil. Nếu file đã được chạy trên máy thật, xử lý như compromise.”

---

## 1) Executive Summary (Tóm tắt điều tra)

Mẫu **dragon_ice_clientbuildV1.2** là một mẫu malware dạng **dropper + stealer**. Ngay khi chạy, nó tự bung runtime Python (PyInstaller), sau đó thiết lập nhiều lớp persistence để đảm bảo “sống dai” trong hệ thống. Điểm nguy hiểm nhất nằm ở việc nó có dấu hiệu truy cập dữ liệu trình duyệt và credential (Chrome cache + Windows Credentials), và có kênh exfiltration rõ ràng ra ngoài (Discord webhook). Song song đó, nó tải config/payload động từ GitHub raw — nghĩa là attacker có thể thay đổi hành vi bất cứ lúc nào.

| Hạng mục | Kết quả | Ý nghĩa |
|---|---|---|
| File type | PyInstaller-packed executable | Dropper/Payload đóng gói Python, dễ obfuscate |
| Persistence | Service + Task + Startup + Registry | Bám trụ nhiều lớp, khó làm sạch thủ công |
| Masquerading | Windows Audio Service / AudioEndpointBuilder / TaskScheduler | Ngụy trang thành thành phần hệ thống |
| Stealing target | Chrome cache + Windows Credentials | Token/cookie/password/session hijacking |
| Exfil/C2 | Discord webhook + GitHub raw | Gửi dữ liệu ra ngoài + tải config/payload động |
| Risk | High → Critical | Account takeover, tái nhiễm, khó xử lý |

---

## 2) Evidence (Bằng chứng kỹ thuật chính)

### 2.1 PyInstaller Bundle (Dropper Stage)

Khi thực thi, file tự giải nén vào folder dạng:

```
%TEMP%_MEIxxxxx\

```

Đây là hành vi điển hình của **PyInstaller** (Python bundler). Nó thả ra các file như `python313.dll`, `base_library.zip`, `_ssl.pyd`, `_socket.pyd`, `libcrypto-3.dll`, `libssl-3.dll`. Những module này cung cấp runtime Python + network/TLS, giúp malware có thể kết nối internet và gửi dữ liệu ra ngoài.  

**Điểm quan trọng:** PyInstaller không “xấu” tự thân, nhưng khi kết hợp với persistence + exfiltration thì gần như chắc chắn là malware.

| Loại artifact | Dấu hiệu | Ý nghĩa |
|---|---|---|
| Folder | `%TEMP%\_MEIxxxxx\` | Runtime unpack của PyInstaller |
| Runtime libs | `python313.dll`, `base_library.zip` | Python runtime + standard library |
| Network/TLS | `_ssl.pyd`, `_socket.pyd`, `libssl-3.dll` | Hỗ trợ kết nối + mã hoá truyền dữ liệu |

> **Thagore note:** “_MEI + python runtime chỉ là dấu hiệu ‘đáng nghi’. Nhưng khi đi cùng persistence/service/task và discord webhook thì verdict chốt luôn.”

---

## 3) Persistence & Masquerading (Bám trụ + Ngụy trang)

### 3.1 Service Persistence (Dịch vụ Windows giả)

Malware tạo các service như `AudioSrv339`, `AudioSrv458`, `AudioSrv693` bằng lệnh `sc create`. Nó set `DisplayName` thành **Windows Audio Service** và mô tả giống hệ thống để đánh lừa người kiểm tra. Service được cấu hình `start= auto`, tức sẽ chạy mỗi lần boot.

Điểm độc hại nằm ở chỗ `binPath` trỏ về các file bất thường như `SystemGuard.dat` hoặc `TaskScheduler.exe` nằm ngoài vị trí hệ thống chuẩn.

| Thành phần | Dấu hiệu | Tại sao nguy hiểm |
|---|---|---|
| Service name | `AudioSrv339/458/693` | Tạo service mới để persistence |
| DisplayName | `Windows Audio Service` | Ngụy trang giống dịch vụ thật |
| Start type | `auto` | Tự chạy cùng hệ thống |
| BinPath | `.dat`, `TaskScheduler.exe` ở path lạ | Chạy payload bị ngụy trang |

### 3.2 Scheduled Tasks (Task Scheduler XML)

Ngoài service, malware tạo thêm scheduled tasks như `WindowsAudioService3829.xml` và `WindowsAudioService8768.xml`. Việc dùng XML giúp attacker cấu hình task linh hoạt, chạy định kỳ hoặc theo trigger. Đây là **persistence dự phòng** — nếu service bị xoá, task vẫn chạy.

| Thành phần | Dấu hiệu | Mục tiêu |
|---|---|---|
| Task creation | `schtasks /create /xml ...` | Tự chạy theo lịch |
| Task name | `WindowsAudioService****` | Ngụy trang như task hệ thống |
| Redundancy | nhiều task cùng theme | “Sống dai” khi bị xoá một phần |

### 3.3 Startup Shortcut + Fake Components (Tự chạy khi login)

Malware tạo shortcut `Windows Audio.lnk` trong Startup và drop các file giả danh Windows component như `TaskScheduler.exe`, `AudioEndpointBuilder.dll`, `AudioEndpointBuilder.sys`. Những file này có tên giống file hệ thống nhưng đặt tại `Themes`, `Recent`, `Temp`, `Startup` — cực bất thường.

**Đây là kỹ thuật Masquerading:** cố tình đặt tên để người dùng nghĩ là file Windows hợp pháp.

| File | Vị trí | Nhận định |
|---|---|---|
| `Windows Audio.lnk` | Startup | Auto-run khi login |
| `TaskScheduler.exe` | Themes | Sai vị trí hệ thống, nghi payload |
| `AudioEndpointBuilder.sys` | Temp | Driver đặt ở Temp là red flag |

---

## 4) Registry Persistence (HKCU Run/RunOnce)

Malware chỉnh sửa:

```
HKCU\Software\Microsoft\Windows\CurrentVersion\Run

```

và tạo value như `ChromeHelper`, `SecurityMonitor`, `SystemUpdate`, `WindowsAudio`. Đây là persistence theo kiểu “classic”, giúp malware chạy mỗi lần user đăng nhập mà không cần quyền admin.

Điểm đáng chú ý là các tên value được đặt rất “hợp lý” để tránh nghi ngờ.

| Key | Value | Ý đồ |
|---|---|---|
| HKCU Run | `ChromeHelper` | giả danh Chrome helper |
| HKCU Run | `SystemUpdate` | giả danh update service |
| HKCU Run | `WindowsAudio` | đồng bộ với theme audio |

> **Thagore note:** “Bản này không phải ‘1 persistence’. Nó dựng redundancy: service + task + startup + registry. Dọn thiếu một cái là nó tự hồi.”

---

## 5) Stealer Behavior (Dấu hiệu đánh cắp dữ liệu)

Mẫu malware truy cập vào Chrome cache `NetworkService.dat` và chạm tới Windows Credentials. Đây là hai vùng dữ liệu có liên quan trực tiếp tới **cookie/token/password/session**. Với stealer, chỉ cần lấy được cookie/token là có thể chiếm session, đôi khi bypass MFA vì MFA thường chỉ bảo vệ login mới, không bảo vệ session token đã có.

| Target | Dấu hiệu | Rủi ro |
|---|---|---|
| Chrome cache | `NetworkService.dat` | token/cookie theft, session hijack |
| Credentials | `WindowsUpdate.tmp` trong Credentials | credential staging/theft |

---

## 6) C2 & Exfiltration (Kênh liên lạc ngoài)

Mẫu malware giao tiếp ra ngoài qua:
- `discord.com/api/webhooks/...` → kênh exfiltration
- `raw.githubusercontent.com/.../main/pi.txt` → tải config/payload động

Điều này xác nhận **nó có cơ chế gửi dữ liệu ra ngoài** và có thể cập nhật hành vi từ xa.

| Kênh | Dấu hiệu | Vai trò |
|---|---|---|
| Discord webhook | `discord.com/api/webhooks/...` | gửi dữ liệu đánh cắp |
| GitHub raw | `raw.githubusercontent.com/...` | tải config/payload |

---

## 7) Attack Chain (Chuỗi tấn công)

Toàn bộ flow có thể tóm gọn như sau:

| Bước | Hành vi | Kết quả |
|---:|---|---|
| 1 | User chạy file | khởi tạo execution |
| 2 | PyInstaller unpack | drop runtime vào `_MEI` |
| 3 | Drop payload | thả file giả hệ thống |
| 4 | Create service | persistence khi boot |
| 5 | Create tasks | persistence dự phòng |
| 6 | Startup + Registry | persistence khi login |
| 7 | Steal | lấy cookie/token/credential |
| 8 | Exfil | gửi qua Discord |
| 9 | Pull config | lấy config từ GitHub raw |

---

## 8) Risk Assessment (Đánh giá)

Tổng thể, rủi ro nằm ở hai điểm:
1) **Stealer** → mất tài khoản (Google/Email/Discord/Telegram, v.v.)  
2) **Persistence đa lớp** → cực khó đảm bảo sạch nếu chỉ “dọn thủ công”

| Hạng mục | Mức độ | Lý do |
|---|---|---|
| Account takeover | High | stealer + session |
| Persistence | Critical | 4 lớp persistence |
| Cleanup | High | masquerading + redundancy |
| Future updates | Medium/High | config/payload động |

---

## 9) Recommended Actions (Khuyến nghị xử lý)

### Nếu chưa chạy file
| Việc cần làm | Lý do |
|---|---|
| Xoá file + quét Defender/EDR | loại bỏ trước khi persistence chạy |
| Check hash (VirusTotal) | xác nhận IOC theo cộng đồng |

### Nếu đã chạy file (quan trọng)
| Ưu tiên | Hành động | Ghi chú |
|---:|---|---|
| 1 | Ngắt mạng ngay | hạn chế exfil |
| 2 | Đổi password trên máy sạch + logout sessions | chống takeover |
| 3 | Defender Offline Scan | quét ngoài OS |
| 4 | Gỡ service/task/startup/registry + xoá file dropped | remove persistence |
| 5 | Nếu yêu cầu sạch tuyệt đối | backup dữ liệu → clean reinstall |

> **Thagore Security Team – Kết luận xử lý:**  
> “Nếu không có EDR + forensic đầy đủ, clean reinstall là cách duy nhất chắc chắn. Stealer không đáng để ‘tiết kiệm công’.”

---

## 10) Kết luận

**dragon_ice_clientbuildV1.2** là **Trojan/Stealer hoàn chỉnh** với các yếu tố xác thực:
- unpack PyInstaller
- persistence đa lớp (service/task/startup/registry)
- truy cập Chrome cache + Credentials
- exfiltration qua Discord webhook
- config/payload động từ GitHub raw

Nếu đã chạy file trên máy thật, nên coi endpoint là **đã compromise** và xử lý theo quy trình incident response nghiêm túc.

---
## Lưu ý
*Báo cáo này là phân tích độc quyền từ **Thagore Security Team**; không sao chép khi chưa có sự cho phép, được phép đăng lại nếu **ghi rõ nguồn/credit Thagore Security Team**.*
