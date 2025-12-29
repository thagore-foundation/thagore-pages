---
title: Install
section: getting-started
sectionTitle: Start
order: 1
searchKeywords: ["install","install","compiz","homebrew","apt","chocolate","macos","compiz","window","download"]
---
# Cài đặt Thagore

Thagore có thể được cài đặt trên macOS, Linux và Windows.

## Yêu cầu hệ thống

- macOS 10.15+, Linux (kernel 4.0+), hoặc Windows 10+
- RAM tối thiểu 4GB
- Dung lượng đĩa trống 500MB

## Cài đặt nhanh

### macOS

```bash
# Sử dụng Homebrew
brew install thagore

# Hoặc script cài đặt
curl -fsSL https://thagore.dev/install.sh | sh
```

### Linux

```bash
# Debian/Ubuntu
sudo apt install thagore

# Hoặc script cài đặt
curl -fsSL https://thagore.dev/install.sh | sh
```

### Windows

```powershell
# Sử dụng Chocolatey
choco install thagore

# Hoặc PowerShell script
iwr -useb https://thagore.dev/install.ps1 | iex
```

## Xác minh cài đặt

Sau khi cài đặt, chạy lệnh sau để xác minh:

```bash
thagore --version
```

Kết quả mong đợi:
```
Thagore v2.3.0
```

## Bước tiếp theo

- [Khởi đầu nhanh](/docs/getting-started/quickstart) - Viết chương trình đầu tiên
- [Tour ngôn ngữ](/docs/getting-started/tour) - Tìm hiểu cú pháp Thagore
