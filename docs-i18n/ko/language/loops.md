---
title: 제품정보
section: language
sectionTitle: * 이름
order: 13
searchKeywords: ["루프","제품정보","제품정보","사이트맵","뚱 베어","제품 설명","제품정보","뚱 베어","시간 아웃"]
---
# Vòng lặp

Thagore hỗ trợ các cấu trúc vòng lặp đơn giản và hiệu quả.

## For với Range

Sử dụng `for...in` với range `1..n`:

```thagore
// Lặp từ 1 đến 5
for i in 1..5
    out(v"Số: {i}")

// Output:
// Số: 1
// Số: 2
// Số: 3
// Số: 4
// Số: 5
```

## For với Danh sách

```thagore
fruits = ["Táo", "Cam", "Xoài", "Chuối"]

for fruit in fruits
    out(v"Trái cây: {fruit}")

// Output:
// Trái cây: Táo
// Trái cây: Cam
// Trái cây: Xoài
// Trái cây: Chuối
```

## While Loop

```thagore
count = 0

while count < 5
    out(v"Count: {count}")
    count = count + 1

// Output:
// Count: 0
// Count: 1
// Count: 2
// Count: 3
// Count: 4
```

## Tính toán trong vòng lặp

```thagore
// Tính tổng từ 1 đến 100
sum = 0
for i in 1..100
    sum = sum + i

out(v"Tổng: {sum}")  // 5050
```

## Đo thời gian thực thi

Sử dụng `time counter` để đo performance:

```thagore
time counter

sum = 0
for i in 1..1000000
    sum = sum + i

out(v"Tổng: {sum}")
// Tự động in thời gian thực thi
```

## Benchmark ví dụ

```thagore
time counter

for j in 1..1000000000
    a = 1

out("done")
// In thời gian để benchmark
```

## Vòng lặp lồng nhau

```thagore
for i in 1..3
    for j in 1..3
        out(v"i={i}, j={j}")

// Output:
// i=1, j=1
// i=1, j=2
// i=1, j=3
// i=2, j=1
// ...
```

## Ví dụ thực tế

```thagore
// In bảng cửu chương
for i in 1..9
    out(v"--- Bảng {i} ---")
    for j in 1..10
        result = i * j
        out(v"{i} x {j} = {result}")
```

## Kết hợp với điều kiện

```thagore
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

for num in numbers
    if num % 2 == 0
        out(v"{num} là số chẵn")
    else
        out(v"{num} là số lẻ")
```

## Bước tiếp theo

- [Hàm](/docs/language/functions) - Định nghĩa functions
- [Xử lý lỗi](/docs/language/error-handling) - Try/catch
- [Collections](/docs/stdlib/collections) - Làm việc với danh sách
