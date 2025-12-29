---
title: OI
section: stdlib
sectionTitle: Bibliothèque standard
order: 21
searchKeywords: ["io","entrée","continue","imprimés","dehors","imprimer","lire","wrate","fichier","entrée","sortie","lire le fichier","écrire un fichier"]
---
# IO - Input/Output

Hướng dẫn xử lý nhập xuất trong Thagore.

## Output cơ bản

### out - In ra màn hình

```thagore
// Cú pháp đơn giản (không cần ngoặc)
out "Hello World"

// Cú pháp với ngoặc
out("Hello World")

// In biến
x = 42
out(x)
```

### String Interpolation

Sử dụng `v"..."` để chèn biến vào chuỗi:

```thagore
name = "Minh"
age = 25
score = 8.5

out(v"Tên: {name}")
out(v"Tuổi: {age}, Điểm: {score}")
out(v"{name} được {score} điểm")
```

### In danh sách

```thagore
numbers = [1, 2, 3, 4, 5]
out(numbers)  // [1, 2, 3, 4, 5]

for num in numbers
    out(v"Số: {num}")
```

## Input

### in - Nhập từ bàn phím

```thagore
// Nhập với prompt
name = in("Nhập tên của bạn: ")
out(v"Xin chào {name}!")

// Nhập số (cần convert)
age_str = in("Nhập tuổi: ")
age = int(age_str)

// Nhập số thực
score_str = in("Nhập điểm: ")
score = float(score_str)
```

### Xử lý input rỗng

```thagore
user = in("Nhập tên: ")

if user
    out(v"Xin chào {user}!")
else
    out("Bạn chưa nhập tên!")
```

### Input với giá trị mặc định

```thagore
default_name = "Guest"

name = in(v"Nhập tên (mặc định: {default_name}): ")

if name == ""
    name = default_name

out(v"Chào mừng {name}!")
```

## File I/O

### Đọc file

```thagore
// Đọc toàn bộ file
content = read_file("data.txt")
out(content)

// Đọc từng dòng
lines = read_lines("data.txt")
for line in lines
    out(line)
```

### Ghi file

```thagore
// Ghi nội dung mới
write_file("output.txt", "Hello World")

// Thêm vào cuối file
append_file("log.txt", "New log entry")
```

### Xử lý file an toàn

```thagore
try
    content = read_file("config.json")
    out("Đọc file thành công!")
catch err
    out(v"Lỗi đọc file: {err}")
finally
    out("Hoàn tất xử lý file")
```

## Ví dụ thực tế

### Chương trình greeting

```thagore
func greet(name) = out(v"Xin chào {name}! Chào mừng đến với Thagore!")

default_days = 1

func active_days()
    date = in(v"Nhập số ngày (mặc định {default_days}): ")
    if date
        out(v"Bạn đã hoạt động {date} ngày!")
    else
        out(v"Dùng mặc định {default_days} ngày")

user = in("Nhập tên của bạn: ")
if user
    greet(user)
    active_days()
else
    out("Không nhập tên!")
```

## Bước tiếp theo

- [Collections](/docs/stdlib/collections) - Làm việc với lists
- [Xử lý lỗi](/docs/language/error-handling) - Try/catch
- [CLI Reference](/docs/tooling/cli-reference) - Command line
