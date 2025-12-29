---
title: 주요사업
section: stdlib
sectionTitle: 표준 도서관
order: 20
searchKeywords: ["사이트맵","최근 댓글","일반 도서관","모듈","아이오","한국어","스트레이트","(주)","회사 소개"]
---
# Thư viện chuẩn

Tổng quan về Standard Library của Thagore.

## Các module chính

### IO - Input/Output

Xử lý nhập xuất dữ liệu:

```thagore
// Output
out("Hello")
out(v"Value: {x}")

// Input
name = in("Nhập tên: ")
```

[Xem chi tiết IO →](/docs/stdlib/io)

### Collections

Làm việc với danh sách và structures:

```thagore
list = [1, 2, 3, 4, 5]
length = len(list)
```

[Xem chi tiết Collections →](/docs/stdlib/collections)

### Math

Các hàm toán học:

```thagore
// Làm tròn
x = round(3.7)     // 4
y = floor(3.7)     // 3
z = ceil(3.2)      // 4

// Giá trị tuyệt đối
abs_val = abs(-5)  // 5

// Min/Max
min_val = min(3, 7)  // 3
max_val = max(3, 7)  // 7
```

### String

Xử lý chuỗi:

```thagore
text = "Hello World"

// Chuyển đổi
upper = uppercase(text)  // "HELLO WORLD"
lower = lowercase(text)  // "hello world"

// Kiểm tra
has = contains(text, "World")  // true

// Cắt chuỗi
sub = substring(text, 0, 5)  // "Hello"
```

### Time

Làm việc với thời gian:

```thagore
// Đo thời gian
time counter
// ... code ...
// Tự động in thời gian

// Lấy timestamp
now = timestamp()
```

## Ví dụ tổng hợp

```thagore
// Chương trình tính BMI
func calculate_bmi(weight, height)
    bmi = weight / (height * height)
    return round(bmi * 10) / 10

name = in("Nhập tên: ")
weight = float(in("Cân nặng (kg): "))
height = float(in("Chiều cao (m): "))

bmi = calculate_bmi(weight, height)

out(v"Xin chào {name}!")
out(v"BMI của bạn: {bmi}")

if bmi < 18.5
    out("Bạn thiếu cân")
else if bmi < 25
    out("Bạn có cân nặng bình thường")
else
    out("Bạn thừa cân")
```

## Bước tiếp theo

- [IO](/docs/stdlib/io) - Chi tiết về input/output
- [Collections](/docs/stdlib/collections) - Làm việc với lists
- [CLI Reference](/docs/tooling/cli-reference) - Lệnh command line
