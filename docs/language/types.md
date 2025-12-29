---
title: Kiểu dữ liệu
titleEn: Types
section: language
sectionTitle: Ngôn ngữ
sectionTitleEn: Language
order: 10
searchKeywords: ["types", "kiểu dữ liệu", "integer", "float", "string", "boolean", "list", "array", "dictionary", "số nguyên", "số thực", "chuỗi"]
---

# Kiểu dữ liệu

Thagore hỗ trợ các kiểu dữ liệu cơ bản với type inference tự động.

## Kiểu cơ bản

### Số nguyên (Integer)

```thagore
tuoi = 25
nam_sinh = 2000
so_am = -10
```

### Số thực (Float)

```thagore
diem = 8.5
pi = 3.14159
nhiet_do = -5.5
```

### Chuỗi (String)

```thagore
ten = "Minh"
message = "Hello World"

// String interpolation
out(v"Tên: {ten}")
```

### Boolean

```thagore
is_active = true
is_done = false

if is_active
    out("Đang hoạt động")
```

## Kiểu phức hợp

### Danh sách (List)

```thagore
// Danh sách số
numbers = [1, 2, 3, 4, 5]

// Danh sách chuỗi
names = ["An", "Bình", "Chi"]

// Truy cập phần tử
first = numbers[0]  // 1
out(v"Phần tử đầu: {first}")

// Lặp qua danh sách
for num in numbers
    out(v"Số: {num}")
```

### Dictionary (nếu hỗ trợ)

```thagore
person = {
    "name": "Minh",
    "age": 25,
    "city": "Hanoi"
}

out(v"Tên: {person.name}")
```

## Type inference

Thagore tự động suy luận kiểu từ giá trị:

```thagore
x = 42       // Integer
y = 3.14     // Float  
z = "hello"  // String
b = true     // Boolean
```

## Ép kiểu

```thagore
// Chuyển đổi kiểu
str_num = "42"
num = int(str_num)  // 42

float_num = 3.7
int_num = int(float_num)  // 3
```

## Bước tiếp theo

- [Hàm](/docs/language/functions) - Định nghĩa functions
- [Vòng lặp](/docs/language/loops) - For và while loops
- [Xử lý lỗi](/docs/language/error-handling) - Try/catch
