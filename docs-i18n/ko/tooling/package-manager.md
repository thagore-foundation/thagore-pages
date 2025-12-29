---
title: 패키지 관리자
section: tooling
sectionTitle: 제품정보
order: 31
searchKeywords: ["패키지manager","사료 pkg","관련 제품","설치하기","₢ 킹","한국어","다운로드","톰슨","관련 기사"]
---
# Package Manager

Hướng dẫn sử dụng Thagore Package Manager.

## Giới thiệu

Thagore Package Manager (thagore pkg) giúp bạn quản lý dependencies cho project.

## Lệnh cơ bản

### Cài đặt package

```bash
# Cài đặt package mới nhất
thagore pkg add thagore-http

# Cài đặt version cụ thể
thagore pkg add thagore-http@2.1.0

# Cài đặt nhiều packages
thagore pkg add thagore-http thagore-json thagore-sql
```

### Xóa package

```bash
thagore pkg remove thagore-http
```

### Cập nhật

```bash
# Cập nhật một package
thagore pkg update thagore-http

# Cập nhật tất cả
thagore pkg update
```

### Liệt kê packages

```bash
# Packages đã cài
thagore pkg list

# Kiểm tra outdated
thagore pkg outdated
```

## File cấu hình

### thagore.toml

```toml
[package]
name = "my-app"
version = "1.0.0"
description = "My Thagore application"
author = "Your Name <you@email.com>"
license = "MIT"

[dependencies]
thagore-http = "2.1.0"
thagore-json = "1.5.0"
thagore-sql = "3.0.1"

[dev-dependencies]
thagore-testing = "1.8.0"
```

### Lock file

File `thagore.lock` tự động tạo để đảm bảo reproducible builds.

## Tìm kiếm packages

```bash
# Tìm theo tên
thagore pkg search http

# Xem thông tin package
thagore pkg info thagore-http
```

## Packages phổ biến

### thagore-http

HTTP client và server:

```thagore
import "thagore-http"

// GET request
response = http.get("https://api.example.com/users")
out(response.body)

// POST request
data = {"name": "Minh", "age": 25}
response = http.post("https://api.example.com/users", data)
```

### thagore-json

JSON parser:

```thagore
import "thagore-json"

// Parse JSON
text = '{"name": "Thagore", "version": "2.3"}'
data = json.parse(text)
out(data.name)  // Thagore

// Stringify
obj = {"key": "value"}
json_str = json.stringify(obj)
```

### thagore-sql

Database driver:

```thagore
import "thagore-sql"

// Kết nối database
db = sql.connect("postgresql://localhost/mydb")

// Query
users = db.query("SELECT * FROM users")
for user in users
    out(v"User: {user.name}")

// Close
db.close()
```

### thagore-crypto

Mã hóa:

```thagore
import "thagore-crypto"

// Hash
hash = crypto.sha256("password")

// Random
token = crypto.random_string(32)
```

## Tạo package

### Cấu trúc

```
my-package/
├── thagore.toml
├── README.md
├── LICENSE
├── src/
│   └── lib.tg      # Entry point
└── tests/
    └── test_lib.tg
```

### Publish

```bash
# Login
thagore pkg login

# Publish
thagore pkg publish
```

## Scripts

Trong `thagore.toml`:

```toml
[scripts]
dev = "thagore run --watch main.tg"
build = "thagore build main.tg --release"
test = "thagore test"
lint = "thagore lint ."
```

Chạy script:

```bash
thagore run-script dev
# hoặc
thagore dev
```

## Bước tiếp theo

- [CLI Reference](/docs/tooling/cli-reference) - Tất cả lệnh CLI
- [Quickstart](/docs/getting-started/quickstart) - Bắt đầu project
- [Packages Registry](/dragos) - Duyệt packages
