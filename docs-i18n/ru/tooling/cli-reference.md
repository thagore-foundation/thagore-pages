---
title: КЛИ Ссылка
section: tooling
sectionTitle: Инструменты
order: 30
searchKeywords: ["кли","командная строка","поврей","тагор потрясает","тагор строит","тагореинит","тагор фмт","тагор инт","тагор тест","повторять"]
---
# CLI Reference

Hướng dẫn sử dụng Thagore Command Line Interface.

## Cài đặt

```bash
# macOS
brew install thagore

# Linux
sudo apt install thagore

# Windows
choco install thagore
```

## Lệnh cơ bản

### thagore run

Chạy chương trình Thagore:

```bash
# Chạy file
thagore run main.tg

# Chạy với arguments
thagore run main.tg -- arg1 arg2
```

### thagore build

Biên dịch thành executable:

```bash
# Build file
thagore build main.tg

# Build với output name
thagore build main.tg -o myapp

# Build release (optimized)
thagore build main.tg --release
```

### thagore init

Tạo project mới:

```bash
# Tạo project
thagore init my-project
cd my-project

# Tạo trong thư mục hiện tại
thagore init .
```

### thagore --version

Kiểm tra phiên bản:

```bash
thagore --version
# Thagore v2.3.0
```

## Công cụ phát triển

### thagore fmt

Format code tự động:

```bash
# Format một file
thagore fmt main.tg

# Format tất cả files
thagore fmt .

# Kiểm tra format (không sửa)
thagore fmt --check main.tg
```

### thagore lint

Kiểm tra lỗi và warnings:

```bash
# Lint một file
thagore lint main.tg

# Lint toàn bộ project
thagore lint .

# Strict mode
thagore lint --strict main.tg
```

### thagore test

Chạy tests:

```bash
# Chạy tất cả tests
thagore test

# Chạy test cụ thể
thagore test test_math.tg

# Verbose output
thagore test -v
```

## Package Manager

### thagore pkg

Quản lý dependencies:

```bash
# Cài đặt package
thagore pkg add thagore-http

# Xóa package
thagore pkg remove thagore-http

# Liệt kê packages
thagore pkg list

# Cập nhật tất cả
thagore pkg update
```

Xem chi tiết: [Package Manager](/docs/tooling/package-manager)

## REPL

Chạy interactive mode:

```bash
thagore repl

# Trong REPL:
> x = 42
> out(v"x = {x}")
x = 42
> exit
```

## Options phổ biến

```bash
# Hiện help
thagore --help
thagore run --help

# Verbose output
thagore run -v main.tg

# Quiet mode
thagore run -q main.tg

# Watch mode (auto-reload)
thagore run --watch main.tg
```

## Cấu trúc Project

```
my-project/
├── main.tg           # Entry point
├── thagore.toml      # Project config
├── src/
│   ├── utils.tg
│   └── models.tg
├── tests/
│   └── test_main.tg
└── packages/         # Dependencies
```

## thagore.toml

```toml
[package]
name = "my-project"
version = "1.0.0"
author = "Your Name"

[dependencies]
thagore-http = "2.1.0"
thagore-json = "1.5.0"

[dev-dependencies]
thagore-testing = "1.8.0"
```

## Bước tiếp theo

- [Package Manager](/docs/tooling/package-manager) - Quản lý packages
- [Quickstart](/docs/getting-started/quickstart) - Bắt đầu coding
- [Tour ngôn ngữ](/docs/getting-started/tour) - Học cú pháp
