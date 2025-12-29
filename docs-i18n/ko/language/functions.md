---
title: 제품정보
section: language
sectionTitle: * 이름
order: 11
searchKeywords: ["재미있는","제품 설명","인기있는","기타","이름 *","이름 *","관련 상품","관련 기사","기본 매개변수"]
---
# Hàm (Functions)

Hướng dẫn định nghĩa và sử dụng hàm trong Thagore.

## Định nghĩa hàm

### Hàm một dòng

Sử dụng cú pháp `=` cho hàm đơn giản:

```thagore
func greet(name) = out(v"Xin chào {name}!")

func double(x) = x * 2

func add(a, b) = a + b
```

### Hàm nhiều dòng

```thagore
func calculate_area(width, height)
    area = width * height
    return area

func process_user(name, age)
    out(v"Xử lý user: {name}")
    if age >= 18
        return "adult"
    else
        return "minor"
```

## Gọi hàm

```thagore
// Gọi hàm đơn giản
greet("Minh")

// Lưu kết quả
result = add(10, 20)
out(v"Kết quả: {result}")

// Hàm lồng nhau
total = add(double(5), double(10))
out(v"Total: {total}")  // 30
```

## Tham số mặc định

```thagore
func greet(name, greeting = "Xin chào")
    out(v"{greeting} {name}!")

greet("Minh")              // Xin chào Minh!
greet("An", "Hello")       // Hello An!
```

## Hàm với nhiều return

```thagore
func check_number(n)
    if n > 0
        return "positive"
    else if n < 0
        return "negative"
    else
        return "zero"

result = check_number(-5)
out(v"Số là: {result}")
```

## Hàm đệ quy

```thagore
func factorial(n)
    if n <= 1
        return 1
    else
        return n * factorial(n - 1)

result = factorial(5)
out(v"5! = {result}")  // 120
```

## Ví dụ thực tế

```thagore
// Ứng dụng greeting
default_days = 1

func active_days()
    date = in(v"Nhập số ngày hoạt động (mặc định {default_days}): ")
    if date
        out(v"Bạn đã hoạt động {date} ngày!")
    else
        out(v"Dùng mặc định {default_days} ngày")

func main()
    user = in("Nhập tên của bạn: ")
    if user
        greet(user)
        active_days()
    else
        out("Không nhập tên!")

main()
```

## Bước tiếp theo

- [Xử lý lỗi](/docs/language/error-handling) - Try/catch/finally
- [Vòng lặp](/docs/language/loops) - For và while
- [Thư viện chuẩn](/docs/stdlib/overview) - Các hàm có sẵn
