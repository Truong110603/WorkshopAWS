---
title: "Xây dựng Expense CRUD và Statistics"
weight: 5
pre: " <b> 4.5 </b> "
---

# Xây dựng Expense CRUD và Statistics

## Mục tiêu

Tạo các API quản lý giao dịch và API thống kê được sử dụng trên Dashboard.

---

## 1. Expense Model

Tạo file:

```text
backend/models/Expense.js
```

Expense Model gồm các trường:

```text
userId
title
amount
type
category
date
```

Ví dụ:

```json
{
    "title": "Đi xe",
    "amount": 50000,
    "type": "expense",
    "category": "Transport",
    "date": "2026-09-28"
}
```

---

## 2. Create Expense

Endpoint:

```text
POST http://localhost:3000/api/expenses
```

Header:

```text
Authorization: Bearer <TOKEN>
```

Request body:

```json
{
    "title": "Đi xe",
    "amount": 50000,
    "type": "expense",
    "category": "Transport",
    "date": "2026-09-28"
}
```

![alt text](/WorkshopAWS/images/4-Workshop/4.5/Post_API.png)

Backend xác thực JWT và tự động lấy `userId` từ User đang đăng nhập.

---

## 3. Read Expenses

Lấy danh sách giao dịch:

```text
GET http://localhost:3000/api/expenses
```

Header:

```text
Authorization: Bearer <TOKEN>
```

Backend lọc dữ liệu theo:

```text
userId
```

Do đó, mỗi User chỉ có thể xem các giao dịch thuộc tài khoản của mình.

Để lấy một giao dịch cụ thể:

```text
GET http://localhost:3000/api/expenses/:id
```

---

## 4. Update Expense

Endpoint:

```text
PUT http://localhost:3000/api/expenses/:id
```

Header:

```text
Authorization: Bearer <TOKEN>
```

Backend tìm giao dịch dựa trên:

```text
_id
userId
```

Sau đó cập nhật dữ liệu của giao dịch.

---

## 5. Delete Expense

Endpoint:

```text
DELETE http://localhost:3000/api/expenses/:id
```

Header:

```text
Authorization: Bearer <TOKEN>
```

Chỉ giao dịch thuộc User đang đăng nhập mới có thể được xóa.

---

## 6. Expense Summary

Endpoint:

```text
GET http://localhost:3000/api/expenses/summary
```

Header:

```text
Authorization: Bearer <TOKEN>
```

Response mẫu:

```json
{
    "totalIncome": 10000000,
    "totalExpense": 2000000,
    "balance": 8000000,
    "totalTransactions": 10
}
```

Số dư được tính theo công thức:

```text
balance = totalIncome - totalExpense
```

Dữ liệu Summary được sử dụng để hiển thị các thông tin tài chính trên Dashboard.

---

## 7. Category Statistics

Endpoint:

```text
GET http://localhost:3000/api/expenses/summary/category
```

Header:

```text
Authorization: Bearer <TOKEN>
```

Dữ liệu được tổng hợp theo `category`.

Ví dụ:

```json
[
    {
        "category": "Food",
        "total": 1500000
    },
    {
        "category": "Transport",
        "total": 500000
    }
]
```

Dữ liệu này được sử dụng để tạo biểu đồ thống kê chi tiêu theo danh mục trên Dashboard.

---

## 8. Lambda Statistics

Sau khi AWS Lambda được triển khai, Backend cung cấp endpoint:

```text
GET http://localhost:3000/api/expenses/lambda-statistics
```

Header:

```text
Authorization: Bearer <TOKEN>
```

API lấy dữ liệu thống kê mới nhất từ collection:

```text
statistics
```

Dữ liệu thống kê được AWS Lambda tạo ra và liên kết với User tương ứng.

---

## 9. Tổng hợp Expense API

Các API chính của Expense Tracker:

```text
POST   /api/expenses
GET    /api/expenses
GET    /api/expenses/:id
PUT    /api/expenses/:id
DELETE /api/expenses/:id

GET    /api/expenses/summary
GET    /api/expenses/summary/category
GET    /api/expenses/lambda-statistics
```

Các API Expense yêu cầu xác thực sử dụng Header:

```text
Authorization: Bearer <TOKEN>
```

---

## 10. Kết quả

Backend Expense Tracker cung cấp:

- Tạo giao dịch.
- Lấy danh sách giao dịch của User.
- Lấy một giao dịch cụ thể.
- Cập nhật giao dịch.
- Xóa giao dịch.
- Tính tổng thu nhập.
- Tính tổng chi tiêu.
- Tính số dư.
- Thống kê chi tiêu theo danh mục.
- Lấy dữ liệu thống kê được AWS Lambda xử lý.

Dữ liệu Expense được lưu trong MongoDB Atlas và liên kết với từng User thông qua `userId`.