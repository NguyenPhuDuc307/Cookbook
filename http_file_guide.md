# Tài liệu hướng dẫn sử dụng file .http

## Mục lục
1. [Giới thiệu](#giới-thiệu)
2. [Cú pháp cơ bản](#cú-pháp-cơ-bản)
3. [Làm việc với nhiều requests](#làm-việc-với-nhiều-requests)
4. [Sử dụng biến](#sử-dụng-biến)
5. [Các phương thức HTTP](#các-phương-thức-http)
6. [Query Parameters](#query-parameters)
7. [Headers](#headers)
8. [Form Data và File Upload](#form-data-và-file-upload)
9. [Comments](#comments)
10. [Lưu response](#lưu-response)
11. [Request chain](#request-chain)
12. [Công cụ hỗ trợ](#công-cụ-hỗ-trợ)
13. [Best Practices](#best-practices)
14. [Ví dụ thực tế](#ví-dụ-thực-tế)

---

## Giới thiệu

File `.http` (hay `.rest`) là định dạng file văn bản đơn giản để lưu trữ và thực thi các HTTP requests. Chúng được hỗ trợ bởi nhiều IDE và editor như Visual Studio Code, IntelliJ IDEA, WebStorm, và các công cụ khác.

**Ưu điểm:**
- Dễ đọc, dễ viết
- Không cần cài đặt phần mềm nặng như Postman
- Có thể commit vào Git để chia sẻ với team
- Tích hợp tốt với IDE
- Hỗ trợ version control

---

## Cú pháp cơ bản

### Request đơn giản

```http
GET https://api.example.com/users
```

### Request với headers

```http
GET https://api.example.com/users
Content-Type: application/json
Authorization: Bearer your-token-here
```

### Request với body (POST/PUT/PATCH)

```http
POST https://api.example.com/users
Content-Type: application/json

{
  "name": "Nguyen Van A",
  "email": "nguyenvana@example.com"
}
```

**⚠️ Lưu ý quan trọng**: Phải có một dòng trống giữa headers và body.

---

## Làm việc với nhiều requests

Sử dụng `###` để phân tách các requests trong cùng một file:

```http
### Lấy danh sách users
GET https://api.example.com/users

### Tạo user mới
POST https://api.example.com/users
Content-Type: application/json

{
  "name": "Tran Thi B",
  "email": "tranthib@example.com"
}

### Cập nhật user
PUT https://api.example.com/users/123
Content-Type: application/json

{
  "name": "Tran Thi B Updated"
}

### Xóa user
DELETE https://api.example.com/users/123
```

---

## Sử dụng biến

### Biến trong file

```http
@baseUrl = https://api.example.com
@token = your-token-here
@userId = 123

### Request sử dụng biến
GET {{baseUrl}}/users/{{userId}}
Authorization: Bearer {{token}}
```

### Biến môi trường

Tạo file `http-client.env.json` (IntelliJ) hoặc `.env` (REST Client):

**http-client.env.json:**
```json
{
  "dev": {
    "baseUrl": "https://dev-api.example.com",
    "token": "dev-token-123"
  },
  "staging": {
    "baseUrl": "https://staging-api.example.com",
    "token": "staging-token-456"
  },
  "prod": {
    "baseUrl": "https://api.example.com",
    "token": "prod-token-789"
  }
}
```

Sử dụng trong file `.http`:

```http
GET {{baseUrl}}/users
Authorization: Bearer {{token}}
```

### Biến hệ thống (System variables)

```http
### Sử dụng timestamp
POST https://api.example.com/events
Content-Type: application/json

{
  "event": "user_login",
  "timestamp": "{{$timestamp}}",
  "uuid": "{{$uuid}}",
  "randomInt": {{$randomInt}}
}
```

Các biến hệ thống có sẵn:
- `{{$timestamp}}` - Unix timestamp
- `{{$isoTimestamp}}` - ISO 8601 timestamp
- `{{$randomInt}}` - Random integer
- `{{$uuid}}` - UUID v4
- `{{$guid}}` - GUID

---

## Các phương thức HTTP

```http
### GET - Lấy dữ liệu
GET https://api.example.com/users/123

### POST - Tạo mới
POST https://api.example.com/users
Content-Type: application/json

{
  "name": "New User",
  "email": "newuser@example.com"
}

### PUT - Cập nhật toàn bộ
PUT https://api.example.com/users/123
Content-Type: application/json

{
  "name": "Updated User",
  "email": "updated@example.com",
  "phone": "0123456789"
}

### PATCH - Cập nhật một phần
PATCH https://api.example.com/users/123
Content-Type: application/json

{
  "name": "Patched Name"
}

### DELETE - Xóa
DELETE https://api.example.com/users/123

### HEAD - Lấy headers
HEAD https://api.example.com/users/123

### OPTIONS - Lấy các phương thức được hỗ trợ
OPTIONS https://api.example.com/users
```

---

## Query Parameters

### Cách 1: Inline (một dòng)

```http
GET https://api.example.com/users?page=1&limit=10&sort=name&order=asc
```

### Cách 2: Nhiều dòng (dễ đọc hơn)

```http
GET https://api.example.com/users
  ?page=1
  &limit=10
  &sort=name
  &order=asc
  &status=active
```

### Cách 3: Sử dụng biến

```http
@page = 1
@limit = 20

GET https://api.example.com/users?page={{page}}&limit={{limit}}
```

---

## Headers

### Headers cơ bản

```http
POST https://api.example.com/data
Content-Type: application/json
Accept: application/json
Authorization: Bearer token123
User-Agent: MyApp/1.0
X-Custom-Header: custom-value
```

### Headers thường dùng

```http
### Authentication
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=
X-API-Key: your-api-key

### Content negotiation
Content-Type: application/json
Accept: application/json
Accept-Language: vi-VN,vi;q=0.9,en-US;q=0.8,en;q=0.7

### Caching
Cache-Control: no-cache
If-None-Match: "686897696a7c876b7e"

### CORS
Origin: https://example.com
Access-Control-Request-Method: POST

### Custom headers
X-Request-ID: {{$uuid}}
X-Client-Version: 1.0.0
```

---

## Form Data và File Upload

### URL-encoded form data

```http
POST https://api.example.com/login
Content-Type: application/x-www-form-urlencoded

username=user@example.com&password=secret123&remember=true
```

### Multipart form data

```http
POST https://api.example.com/upload
Content-Type: multipart/form-data; boundary=WebAppBoundary

--WebAppBoundary
Content-Disposition: form-data; name="username"

john_doe
--WebAppBoundary
Content-Disposition: form-data; name="avatar"; filename="photo.jpg"
Content-Type: image/jpeg

< ./path/to/photo.jpg
--WebAppBoundary--
```

### Upload file đơn giản

```http
POST https://api.example.com/files
Content-Type: image/jpeg

< ./path/to/image.jpg
```

---

## Comments

```http
# Comment một dòng - Cách 1
// Comment một dòng - Cách 2

### Comment dạng separator (phân tách requests)

GET https://api.example.com/users  # Comment cuối dòng

/*
  Comment nhiều dòng
  Sử dụng để mô tả chi tiết
*/
POST https://api.example.com/users
Content-Type: application/json

{
  "name": "Test User"  // Comment trong JSON (có thể không work)
}
```

---

## Lưu response

### Lưu vào file

```http
### Download PDF
GET https://api.example.com/reports/monthly.pdf
> /path/to/save/report.pdf

### Lưu JSON response
GET https://api.example.com/users
> /path/to/save/users.json
```

### Redirect output

```http
### Append to file (>>)
GET https://api.example.com/logs
>> /path/to/logs.txt
```

---

## Request chain

Sử dụng response từ request trước để tạo chuỗi requests:

```http
### 1. Login và lấy token
POST https://api.example.com/auth/login
Content-Type: application/json

{
  "username": "admin",
  "password": "secret123"
}

> {%
    client.global.set("auth_token", response.body.token);
    client.global.set("user_id", response.body.user.id);
%}

### 2. Sử dụng token để lấy profile
GET https://api.example.com/users/{{user_id}}/profile
Authorization: Bearer {{auth_token}}

> {%
    client.global.set("profile_name", response.body.name);
%}

### 3. Cập nhật profile
PUT https://api.example.com/users/{{user_id}}/profile
Authorization: Bearer {{auth_token}}
Content-Type: application/json

{
  "name": "{{profile_name}} - Updated",
  "bio": "New bio"
}
```

### Tests trong response handler

```http
POST https://api.example.com/users
Content-Type: application/json

{
  "name": "Test User"
}

> {%
    client.test("Status is 201", function() {
        client.assert(response.status === 201, "Expected 201");
    });
    
    client.test("Response has id", function() {
        client.assert(response.body.id !== undefined, "ID should exist");
    });
    
    client.test("Name is correct", function() {
        client.assert(response.body.name === "Test User", "Name mismatch");
    });
%}
```

---

## Công cụ hỗ trợ

### Visual Studio Code

**Extension:** REST Client by Huachao Mao

**Cài đặt:**
1. Mở VS Code
2. Vào Extensions (Ctrl+Shift+X)
3. Tìm "REST Client"
4. Click Install

**Shortcuts:**
- `Ctrl+Alt+R` (Windows/Linux) hoặc `Cmd+Alt+R` (Mac): Chạy request
- `Ctrl+Alt+C` (Windows/Linux) hoặc `Cmd+Alt+C` (Mac): Cancel request
- `Ctrl+Alt+E` (Windows/Linux) hoặc `Cmd+Alt+E` (Mac): Chọn môi trường

**Settings (settings.json):**
```json
{
  "rest-client.environmentVariables": {
    "dev": {
      "baseUrl": "http://localhost:3000",
      "token": "dev-token"
    },
    "prod": {
      "baseUrl": "https://api.example.com",
      "token": "prod-token"
    }
  },
  "rest-client.defaultHeaders": {
    "User-Agent": "vscode-rest-client"
  }
}
```

### IntelliJ IDEA / WebStorm / Rider

**Tích hợp sẵn** HTTP Client

**Shortcuts:**
- `Ctrl+Enter` (Windows/Linux) hoặc `Cmd+Enter` (Mac): Chạy request
- `Alt+Enter`: Show context actions
- `Ctrl+Shift+A`: Find action

**File môi trường:**
- `http-client.env.json` - Biến môi trường
- `http-client.private.env.json` - Biến bảo mật (không commit)

### Các công cụ khác

- **Rider** - Tích hợp sẵn
- **PhpStorm** - Tích hợp sẵn
- **Neovim** - Plugin: rest.nvim
- **Emacs** - restclient.el
- **CLI** - httpYac,rest-cli

---

## Best Practices

### 1. Tổ chức file

```
api-tests/
├── auth/
│   ├── login.http
│   └── register.http
├── users/
│   ├── crud.http
│   └── profile.http
├── products/
│   └── products.http
├── http-client.env.json
└── http-client.private.env.json
```

### 2. Đặt tên rõ ràng

```http
### [GET] Lấy danh sách tất cả users - Paginated
GET {{baseUrl}}/users?page=1&limit=20

### [POST] Tạo user mới với role admin
POST {{baseUrl}}/users
Content-Type: application/json

{
  "name": "Admin User",
  "role": "admin"
}
```

### 3. Sử dụng biến môi trường

**✅ Tốt:**
```http
@baseUrl = {{$dotenv BASE_URL}}
GET {{baseUrl}}/users
```

**❌ Không tốt:**
```http
GET https://production-api-key-12345.example.com/users
```

### 4. Bảo mật

**File .gitignore:**
```
# Không commit file chứa secrets
http-client.private.env.json
.env
*.private.http
*secret*.http
```

**File http-client.private.env.json:**
```json
{
  "dev": {
    "apiKey": "secret-key-dev",
    "password": "dev-password"
  },
  "prod": {
    "apiKey": "secret-key-prod",
    "password": "prod-password"
  }
}
```

### 5. Documentation

```http
###
# User Management API
# 
# Base URL: https://api.example.com/v1
# Authentication: Bearer token required
# Rate limit: 100 requests/minute
###

### Get all users
# Returns paginated list of users
# Query params:
#   - page: Page number (default: 1)
#   - limit: Items per page (default: 20)
#   - sort: Sort field (default: createdAt)
GET {{baseUrl}}/users?page=1&limit=20
Authorization: Bearer {{token}}
```

### 6. Error handling

```http
### Test error cases

# 400 Bad Request
POST {{baseUrl}}/users
Content-Type: application/json

{
  "invalid": "data"
}

###

# 401 Unauthorized
GET {{baseUrl}}/protected
# No Authorization header

###

# 404 Not Found
GET {{baseUrl}}/users/999999

###

# 500 Internal Server Error (if applicable)
POST {{baseUrl}}/trigger-error
```

---

## Ví dụ thực tế

### API JSONPlaceholder (Free API for testing)

```http
@baseUrl = https://jsonplaceholder.typicode.com

### 1. Lấy tất cả posts
GET {{baseUrl}}/posts

###

### 2. Lấy một post cụ thể
GET {{baseUrl}}/posts/1

###

### 3. Lấy comments của post
GET {{baseUrl}}/posts/1/comments

###

### 4. Lấy posts của user
GET {{baseUrl}}/posts?userId=1

###

### 5. Tạo post mới
POST {{baseUrl}}/posts
Content-Type: application/json

{
  "title": "Bài viết tiếng Việt",
  "body": "Đây là nội dung bài viết bằng tiếng Việt với dấu thanh đầy đủ",
  "userId": 1
}

###

### 6. Cập nhật post (PUT)
PUT {{baseUrl}}/posts/1
Content-Type: application/json

{
  "id": 1,
  "title": "Bài viết đã cập nhật",
  "body": "Nội dung hoàn toàn mới",
  "userId": 1
}

###

### 7. Cập nhật một phần (PATCH)
PATCH {{baseUrl}}/posts/1
Content-Type: application/json

{
  "title": "Chỉ cập nhật tiêu đề"
}

###

### 8. Xóa post
DELETE {{baseUrl}}/posts/1

###

### 9. Filter và search
GET {{baseUrl}}/posts?userId=1&_limit=5&_sort=id&_order=desc
```

### REST API với Authentication

```http
@baseUrl = https://api.example.com/v1
@email = user@example.com
@password = secretPassword123

### 1. Register
POST {{baseUrl}}/auth/register
Content-Type: application/json

{
  "email": "{{email}}",
  "password": "{{password}}",
  "name": "Nguyen Van A"
}

###

### 2. Login
POST {{baseUrl}}/auth/login
Content-Type: application/json

{
  "email": "{{email}}",
  "password": "{{password}}"
}

> {%
    client.global.set("accessToken", response.body.accessToken);
    client.global.set("refreshToken", response.body.refreshToken);
%}

###

### 3. Get profile (Protected)
GET {{baseUrl}}/users/me
Authorization: Bearer {{accessToken}}

###

### 4. Update profile
PUT {{baseUrl}}/users/me
Authorization: Bearer {{accessToken}}
Content-Type: application/json

{
  "name": "Nguyen Van A - Updated",
  "bio": "Software Developer",
  "phone": "+84123456789"
}

###

### 5. Refresh token
POST {{baseUrl}}/auth/refresh
Content-Type: application/json

{
  "refreshToken": "{{refreshToken}}"
}

> {%
    client.global.set("accessToken", response.body.accessToken);
%}

###

### 6. Logout
POST {{baseUrl}}/auth/logout
Authorization: Bearer {{accessToken}}
```

### GraphQL API

```http
@graphqlUrl = https://api.example.com/graphql

### Query - Lấy dữ liệu
POST {{graphqlUrl}}
Content-Type: application/json

{
  "query": "query GetUsers { users { id name email } }"
}

###

### Query với variables
POST {{graphqlUrl}}
Content-Type: application/json

{
  "query": "query GetUser($id: ID!) { user(id: $id) { id name email posts { title } } }",
  "variables": {
    "id": "123"
  }
}

###

### Mutation - Tạo dữ liệu
POST {{graphqlUrl}}
Content-Type: application/json

{
  "query": "mutation CreateUser($input: UserInput!) { createUser(input: $input) { id name email } }",
  "variables": {
    "input": {
      "name": "New User",
      "email": "newuser@example.com"
    }
  }
}
```

### File Upload

```http
@baseUrl = https://api.example.com

### Upload single file
POST {{baseUrl}}/upload
Content-Type: multipart/form-data; boundary=----Boundary

------Boundary
Content-Disposition: form-data; name="file"; filename="document.pdf"
Content-Type: application/pdf

< ./files/document.pdf
------Boundary--

###

### Upload với metadata
POST {{baseUrl}}/upload
Content-Type: multipart/form-data; boundary=----Boundary

------Boundary
Content-Disposition: form-data; name="title"

My Document
------Boundary
Content-Disposition: form-data; name="description"

Important document for review
------Boundary
Content-Disposition: form-data; name="file"; filename="document.pdf"
Content-Type: application/pdf

< ./files/document.pdf
------Boundary--
```

---

## Kết luận

File `.http` là công cụ mạnh mẽ và đơn giản để:
- Test API trong quá trình phát triển
- Tài liệu hóa API endpoints
- Chia sẻ examples với team
- Tự động hóa testing workflows

**Ưu điểm chính:**
- ✅ Nhẹ, không cần phần mềm nặng
- ✅ Tích hợp tốt với IDE
- ✅ Dễ dàng version control
- ✅ Hỗ trợ nhiều môi trường
- ✅ Có thể automation

**Bắt đầu ngay:**
1. Cài extension REST Client cho VS Code hoặc dùng IntelliJ
2. Tạo file `test.http`
3. Viết request đầu tiên
4. Nhấn shortcut để chạy
5. Xem kết quả ngay trong IDE

Chúc bạn thành công! 🚀