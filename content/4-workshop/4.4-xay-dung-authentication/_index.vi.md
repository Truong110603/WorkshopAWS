---
title: "Xây dựng Authentication và JWT"
weight: 4
pre: " <b> 4.4 </b> "
---

# Xây dựng Authentication và JWT

## Mục tiêu

Thêm chức năng đăng ký, đăng nhập và xác thực người dùng cho Expense Tracker.

---

## 1. Cài đặt package

Trong thư mục Backend, cài đặt các package:

```bash
npm install bcryptjs jsonwebtoken
```

- `bcryptjs`: Hash mật khẩu trước khi lưu vào MongoDB.
- `jsonwebtoken`: Tạo và xác thực JWT Token.

---

## 2. User Model

Tạo file:

```text
backend/models/User.js
```

User Model gồm các thông tin:

```text
name
email
password
createdAt
```

Mật khẩu được hash bằng `bcryptjs` trước khi lưu vào MongoDB.

---

## 3. Register API

API đăng ký sử dụng endpoint:

```text
POST http://localhost:3000/api/auth/register
```

Request:

```json
{
    "name": "Test User",
    "email": "test@gmail.com",
    "password": "123456"
}
```

![alt text](../../images/4-Workshop/4.5/Post_API.png)

Backend thực hiện các bước:

1. Kiểm tra dữ liệu đầu vào.
2. Kiểm tra email đã tồn tại hay chưa.
3. Hash mật khẩu bằng bcrypt.
4. Tạo User mới.
5. Lưu User vào MongoDB Atlas.
6. Trả về kết quả đăng ký.

---

## 4. Login API

API đăng nhập sử dụng endpoint:

```text
POST http://localhost:3000/api/auth/login
```

Request:

```json
{
    "email": "test@gmail.com",
    "password": "123456"
}
```

Sau khi xác thực thành công, Backend tạo JWT:

```javascript
const token = jwt.sign(
    {
        userId: user._id,
        email: user.email
    },
    process.env.JWT_SECRET,
    {
        expiresIn: "1d"
    }
);
```

Response chứa:

```text
token
user
```

Frontend lưu Token vào `localStorage` và gửi Token trong các request yêu cầu xác thực.

---

## 5. Authentication Middleware

Tạo file:

```text
backend/middleware/authMiddleware.js
```

Middleware đọc JWT từ Header:

```text
Authorization: Bearer <TOKEN>
```

Sau khi xác thực Token thành công, thông tin User được lưu vào:

```javascript
req.user = decoded;
```

Các API Expense sử dụng Middleware này để kiểm tra người dùng đã đăng nhập.

---

## 6. User ID

Khi tạo Expense, `userId` được lấy từ JWT:

```javascript
userId: req.user.userId
```

Không lấy `userId` trực tiếp từ dữ liệu do Frontend gửi lên.

Mối quan hệ dữ liệu:

```text
User
 │
 └── userId
       │
       ├── Expense
       ├── Expense
       └── Expense
```

Điều này đảm bảo mỗi giao dịch được liên kết với đúng tài khoản người dùng.

---

## 7. Quy trình Authentication

```text
Register
    ↓
Login
    ↓
JWT Token
    ↓
Authentication Middleware
    ↓
Expense API
```

---

## 8. Kết quả

Chức năng Authentication hoàn chỉnh gồm:

- Đăng ký tài khoản.
- Đăng nhập.
- Hash mật khẩu bằng bcrypt.
- Tạo JWT Token.
- Xác thực JWT bằng Middleware.
- Quản lý giao dịch theo từng User.

Mỗi giao dịch được liên kết với tài khoản tương ứng thông qua `userId`.