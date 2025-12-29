---
title: Языковой тур
section: getting-started
sectionTitle: Начинать
order: 3
searchKeywords: ["тур","тур в очереди","мяч","базовый","переменный","переменные","грибы","функция","петли","петля","консуммы","состояние"]
---
# Tour ngôn ngữ Thagore

Hướng dẫn tổng quan về các tính năng chính của Thagore.

## Biến

Thagore sử dụng type inference - bạn không cần khai báo kiểu:

```thagore
// Số nguyên
tuoi = 25

// Số thực
diem = 8.5

// Chuỗi
ten = "Minh"

// Boolean
is_student = true

// Danh sách
numbers = [1, 2, 3, 4, 5]
```

## Output và Input

```thagore
// Output đơn giản
out "Hello World"
out("Hello World")

// String interpolation
name = "Thagore"
out(v"Xin chào {name}!")

// Input từ người dùng
user = in("Nhập tên: ")
```

## Điều kiện

```thagore
tuoi = 20

if tuoi >= 18
    out("Đã trưởng thành")
else
    out("Chưa trưởng thành")

// Điều kiện lồng nhau
if tuoi < 13
    out("Trẻ em")
else if tuoi < 18
    out("Thiếu niên")
else
    out("Người lớn")
```

## Vòng lặp

```thagore
// For với range
for i in 1..5
    out(v"Số: {i}")

// For với danh sách
fruits = ["Táo", "Cam", "Xoài"]
for fruit in fruits
    out(v"Trái cây: {fruit}")

// While loop (nếu cần)
count = 0
while count < 5
    out(v"Count: {count}")
    count = count + 1
```

## Hàm

```thagore
// Hàm một dòng
func greet(name) = out(v"Xin chào {name}!")

// Hàm nhiều dòng
func calculate_sum(a, b)
    result = a + b
    return result

// Sử dụng
greet("Thagore")
sum = calculate_sum(10, 20)
out(v"Tổng: {sum}")
```

## Xử lý lỗi

```thagore
func risky_operation()
    throw "Something went wrong!"

try
    risky_operation()
catch err
    out(v"Lỗi: {err}")
finally
    out("Cleanup xong!")
```

## Đo thời gian

```thagore
time counter

for i in 1..1000000
    a = i * 2

out "Done!"
// Tự động in thời gian thực thi
```

## Bước tiếp theo

- [Kiểu dữ liệu](/docs/language/types) - Chi tiết về types
- [Hàm](/docs/language/functions) - Nâng cao về functions
- [Xử lý lỗi](/docs/language/error-handling) - Try/catch/finally
