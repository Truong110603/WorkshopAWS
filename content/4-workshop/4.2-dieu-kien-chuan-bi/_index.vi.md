---
title: "Điều kiện chuẩn bị"
weight: 2
pre: " <b> 4.2 </b> "
---

# Điều kiện chuẩn bị

### Mục tiêu

Đảm bảo người thực hiện có đầy đủ công cụ lập trình, tài khoản AWS và mã nguồn cần thiết trước khi bắt đầu xây dựng và triển khai Expense Tracker.

---

## 1. Công cụ cần chuẩn bị

Workshop sử dụng các công cụ sau:

- **Node.js**: Chạy Backend và Frontend của dự án.
- **npm**: Quản lý package Node.js.
- **Git**: Quản lý mã nguồn.
- **Visual Studio Code**: Chỉnh sửa mã nguồn.
- **Postman**: Kiểm thử REST API.
- **MongoDB Atlas**: Cơ sở dữ liệu.
- **AWS Management Console**: Quản lý các dịch vụ AWS.

Không yêu cầu AWS CLI hoặc Docker trong phiên bản Workshop này.

---

## 2. Kiểm tra môi trường local

Mở Terminal hoặc PowerShell và kiểm tra:

```bash
node --version
npm --version
git --version
```

### Checkpoint

Các lệnh phải trả về phiên bản tương ứng.

---

## 3. Chuẩn bị AWS Account

Đăng nhập vào AWS Management Console.

Chọn Region sử dụng cho Workshop.

Ví dụ:

```text
Asia Pacific (Singapore)
ap-southeast-1
```

### Checkpoint

Xác nhận AWS Console đang sử dụng đúng Region trước khi tạo tài nguyên.

---

## 4. Chuẩn bị MongoDB Atlas

Tạo MongoDB Atlas Cluster và chuẩn bị:

- Database User.
- Password.
- Connection String.
- Network Access.

Database sử dụng trong project:

```text
expensetracker
```

Các collection chính:

```text
users
expenses
statistics
```
![alt text](/WorkshopAWS/images/4-Workshop/4.2/mongodb-database.jpg.png)
---

## 5. Chuẩn bị mã nguồn

Mở project bằng Visual Studio Code.

Cấu trúc project:

```text
expense-tracker/
├── backend/
├── frontend/
└── lambda-statistics/
```

Backend chứa:

```text
server.js
routes/
models/
middleware/
.env
```
![alt text](/WorkshopAWS/images/4-Workshop/4.2/cau-truc-project.png)

Frontend chứa giao diện Dashboard và các file JavaScript/CSS.

Lambda chứa mã nguồn xử lý thống kê.

---

## 6. Kết quả mong đợi

Sau khi hoàn thành bước chuẩn bị:

- Node.js đã hoạt động.
- npm đã hoạt động.
- Git đã sẵn sàng.
- Postman đã sẵn sàng.
- AWS Account đã có thể truy cập.
- MongoDB Atlas đã được chuẩn bị.
- Source code Expense Tracker đã sẵn sàng.