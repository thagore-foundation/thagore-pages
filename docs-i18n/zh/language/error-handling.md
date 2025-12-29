---
title: Xử lý lỗi
section: language
sectionTitle: Ngôn ngữ
order: 12
searchKeywords: ["error handling","xử lý lỗi","try","catch","finally","throw","exception","ngoại lệ","lỗi"]
---
# Xử lý lỗi

Thagore hỗ trợ try/catch/finally để xử lý lỗi an toàn.

## Try/Catch cơ bản

```thagore
try
    // Code có thể gây lỗi
    result = risky_operation()
    out(v"Kết quả: {result}")
catch err
    // Xử lý lỗi
    out(v"Có lỗi xảy ra: {err}")
```

## Try/Catch/Finally

`finally` block luôn chạy, dù có lỗi hay không:

```thagore
try
    out("Bắt đầu xử lý...")
    do_something()
catch err
    out(v"Lỗi: {err}")
finally
    out("Cleanup hoàn tất!")
```

## Throw - Ném lỗi

Sử dụng `throw` để ném lỗi:

```thagore
func divide(a, b)
    if b == 0
        throw "Không thể chia cho 0!"
    return a / b

try
    result = divide(10, 0)
catch err
    out(v"Lỗi: {err}")
```

## Ví dụ đầy đủ

```thagore
out "Testing try/catch/finally..."

func risky_operation()
    throw "Something went wrong!"

func safe_operation()
    return 42

// Test 1: Lỗi được bắt
try
    out "Executing risky operation..."
    risky_operation()
catch err
    out(v"Caught error: {err}")
finally
    out "Cleanup: This always runs!"

// Test 2: Thành công
try
    result = safe_operation()
    out(v"Got result: {result}")
catch err
    out(v"Error: {err}")
finally
    out "Cleanup: Success case!"

out "All tests completed!"
```

Output:
```
Testing try/catch/finally...
Executing risky operation...
Caught error: Something went wrong!
Cleanup: This always runs!
Got result: 42
Cleanup: Success case!
All tests completed!
```

## Best Practices

### 1. Luôn catch lỗi cụ thể

```thagore
try
    data = load_file("config.json")
catch err
    out(v"Không thể đọc file: {err}")
    // Sử dụng giá trị mặc định
    data = default_config()
```

### 2. Cleanup trong finally

```thagore
try
    file = open("data.txt")
    process(file)
catch err
    out(v"Lỗi xử lý: {err}")
finally
    close(file)  // Luôn đóng file
```

### 3. Throw với thông báo rõ ràng

```thagore
func validate_age(age)
    if age < 0
        throw "Tuổi không thể âm!"
    if age > 150
        throw "Tuổi không hợp lệ!"
    return true
```

## Bước tiếp theo

- [Vòng lặp](/docs/language/loops) - For và while loops
- [Hàm](/docs/language/functions) - Functions nâng cao
- [IO](/docs/stdlib/io) - Đọc/ghi file
