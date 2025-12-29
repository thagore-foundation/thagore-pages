---
title: Collections
section: stdlib
sectionTitle: Thư viện chuẩn
order: 22
searchKeywords: ["collections","list","danh sách","array","mảng","filter","map","reduce","sort","push","pop","len"]
---
# Collections

Hướng dẫn làm việc với danh sách và collections trong Thagore.

## List (Danh sách)

### Tạo danh sách

```thagore
// Danh sách số
numbers = [1, 2, 3, 4, 5]

// Danh sách chuỗi
names = ["An", "Bình", "Chi"]

// Danh sách rỗng
empty = []

// Danh sách hỗn hợp
mixed = [1, "hello", 3.14, true]
```

### Truy cập phần tử

```thagore
list = [10, 20, 30, 40, 50]

// Index bắt đầu từ 0
first = list[0]   // 10
second = list[1]  // 20
last = list[4]    // 50

out(v"Phần tử đầu: {first}")
```

### Thêm/Xóa phần tử

```thagore
list = [1, 2, 3]

// Thêm vào cuối
push(list, 4)     // [1, 2, 3, 4]

// Xóa phần tử cuối
pop(list)         // [1, 2, 3]

// Thêm vào đầu
unshift(list, 0)  // [0, 1, 2, 3]
```

### Chiều dài

```thagore
list = [1, 2, 3, 4, 5]
length = len(list)  // 5

out(v"Danh sách có {length} phần tử")
```

## Lặp qua Collections

### For loop

```thagore
fruits = ["Táo", "Cam", "Xoài"]

for fruit in fruits
    out(v"Trái cây: {fruit}")
```

### Với index

```thagore
items = ["a", "b", "c"]

for i in 0..len(items)
    out(v"Index {i}: {items[i]}")
```

## Các hàm hữu ích

### Tìm kiếm

```thagore
list = [10, 20, 30, 40, 50]

// Kiểm tra tồn tại
has_30 = contains(list, 30)  // true
has_99 = contains(list, 99)  // false

// Tìm vị trí
pos = index_of(list, 30)  // 2
```

### Sắp xếp

```thagore
numbers = [3, 1, 4, 1, 5, 9, 2, 6]

sorted = sort(numbers)
// [1, 1, 2, 3, 4, 5, 6, 9]

reversed = reverse(numbers)
// [6, 2, 9, 5, 1, 4, 1, 3]
```

### Filter và Map

```thagore
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

// Lọc số chẵn
evens = filter(numbers, func(x) = x % 2 == 0)
// [2, 4, 6, 8, 10]

// Nhân đôi mỗi số
doubled = map(numbers, func(x) = x * 2)
// [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```

### Reduce

```thagore
numbers = [1, 2, 3, 4, 5]

// Tính tổng
sum = reduce(numbers, 0, func(acc, x) = acc + x)
// 15

// Tìm max
max_val = reduce(numbers, numbers[0], func(acc, x) = max(acc, x))
// 5
```

## Ví dụ thực tế

### Quản lý danh sách tasks

```thagore
tasks = []

func add_task(name)
    push(tasks, name)
    out(v"Đã thêm: {name}")

func list_tasks()
    if len(tasks) == 0
        out("Không có task nào!")
    else
        out("Danh sách tasks:")
        for i in 0..len(tasks)
            out(v"  {i + 1}. {tasks[i]}")

func remove_task(index)
    if index >= 0 and index < len(tasks)
        removed = tasks[index]
        // Remove logic...
        out(v"Đã xóa: {removed}")
    else
        out("Index không hợp lệ!")

// Sử dụng
add_task("Học Thagore")
add_task("Viết code")
add_task("Review PR")
list_tasks()
```

## Bước tiếp theo

- [IO](/docs/stdlib/io) - Input/Output
- [Vòng lặp](/docs/language/loops) - For và while
- [Hàm](/docs/language/functions) - Functions
