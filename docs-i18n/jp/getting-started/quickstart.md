---
title: クイックスタート
section: getting-started
sectionTitle: スタート
order: 2
searchKeywords: ["クイックスタート","クイックスタート","スタート","ハローワールド","ファーストプログラム","ファーストプログラム","ギッティングスタート"]
---
# Khởi đầu nhanh

Hãy tạo chương trình Thagore đầu tiên của bạn trong vài phút.

## Tạo file đầu tiên

Tạo một file mới với đuôi `.tg`:

```bash
# Tạo thư mục project
mkdir hello-thagore
cd hello-thagore

# Tạo file chương trình
touch main.tg
```

## Viết code

Mở file `main.tg` và thêm code sau:

```thagore
// main.tg - Chương trình đầu tiên
out "Xin chào thế giới!"

// Khai báo biến
name = "Thagore"
version = "2.3"
year = 2025

// String interpolation với v"..."
out(v"Bọn mình là ngôn ngữ {name}")
out(v"Phiên bản hiện tại: {version}")
out(v"Thành lập từ năm {year}")
```

## Chạy chương trình

```bash
thagore run main.tg
```

Kết quả:
```
Xin chào thế giới!
Bọn mình là ngôn ngữ Thagore
Phiên bản hiện tại: 2.3
Thành lập từ năm 2025
```

## Ví dụ với input

```thagore
// greeting.tg
func greet(name) = out(v"Xin chào {name}! Chào mừng đến với Thagore!")

user = in("Nhập tên của bạn: ")
if user
    greet(user)
    out("Cú pháp dễ và chạy nhanh như C++!")
else
    out("Bạn chưa nhập tên!")
```

## Bước tiếp theo

- [Tour ngôn ngữ](/docs/getting-started/tour) - Tìm hiểu chi tiết cú pháp
- [Kiểu dữ liệu](/docs/language/types) - Các kiểu dữ liệu trong Thagore
- [Hàm](/docs/language/functions) - Định nghĩa và sử dụng hàm
