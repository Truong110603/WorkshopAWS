---
title: "Xây dựng Backend và kết nối MongoDB"
weight: 3
pre: " <b> 4.3 </b> "
---

# Xây dựng Backend và kết nối MongoDB

## Mục tiêu

Tạo Backend bằng Node.js và Express, sau đó kết nối với MongoDB Atlas.

---

## 1. Tạo Backend

Tạo thư mục:

```text
C:\Codes\expense-tracker\backend
```

Khởi tạo Node.js:

```bash
npm init -y
```

Cài các package:

```bash
npm install express mongoose cors dotenv
```

---

## 2. Tạo Server

File:

```text
backend/server.js
```

Các thành phần chính:

```javascript
const express = require("express");
const mongoose = require("mongoose");
const cors = require("cors");
require("dotenv").config();

const app = express();

app.use(cors());
app.use(express.json());

mongoose
    .connect(process.env.MONGO_URI)
    .then(() => {
        console.log("MongoDB connected successfully");
    })
    .catch((error) => {
        console.error("MongoDB connection error:", error);
    });

app.get("/api/health", (req, res) => {
    res.json({ status: "ok" });
});

const PORT = process.env.PORT || 3000;

app.listen(PORT, () => {
    console.log(`Server running on http://localhost:${PORT}`);
});
```

---

## 3. Cấu hình MongoDB

Tạo file:

```text
backend/.env
```

Nội dung:

```text
MONGO_URI=<MONGODB_CONNECTION_STRING>
PORT=3000
JWT_SECRET=<SECRET>
```

Database sử dụng:

```text
expensetracker
```
![alt text](/WorkshopAWS/images/4-Workshop/4.3/env-file.png)
---

## 4. Chạy Backend

Tại thư mục Backend:

```bash
node server.js
```
![alt text](/WorkshopAWS/images/4-Workshop/4.2/runbackend.png)

Kiểm tra:

```text
GET http://localhost:3000/api/health
```
![alt text](/WorkshopAWS/images/4-Workshop/4.2/apihealth.png)
Response:

```json
{
    "status": "ok"
}
```

---

## 5. Tổ chức Backend

Sau khi hoàn thiện, Backend có cấu trúc:

```text
backend/
├── middleware/
│   └── authMiddleware.js
├── models/
│   ├── User.js
│   └── Expense.js
├── routes/
│   ├── authRoutes.js
│   └── expenseRoutes.js
├── .env
├── package.json
└── server.js
```

---

## 6. Kết quả

Backend chạy trên port `3000` và kết nối đến MongoDB Atlas.

Các API Authentication và Expense được triển khai ở các bước tiếp theo.