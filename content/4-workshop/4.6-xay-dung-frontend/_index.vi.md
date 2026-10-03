---
title: "Xây dựng Frontend và Dashboard"
weight: 6
pre: " <b> 4.6 </b> "
---

# Xây dựng Frontend và Dashboard

## Mục tiêu

Tạo giao diện cho Expense Tracker và kết nối Frontend với các API của Backend.

---

## 1. Cấu trúc Frontend

```text
frontend/
├── index.html
├── login.html
├── register.html
├── app.js
├── login.js
├── register.js
└── style.css
```

---

## 2. Register

Trang Register gồm:

```text
Name
Email
Password
```
![alt text](/WorkshopAWS/images/4-Workshop/4.6/signup.png)




---

## 3. Login
rang Login gồm:

```text
Email
Password
```

![Màn hình login](/WorkshopAWS/images/4-Workshop/4.6/Login.png)

Sau khi đăng nhập, token được lưu vào Local Storage:

```javascript
localStorage.setItem("token", data.token);
```

Thông tin User:

```javascript
localStorage.setItem(
    "user",
    JSON.stringify(data.user)
);
```

---

## 4. Gửi JWT

Khi gọi các API cần xác thực:

```javascript
const token = localStorage.getItem("token");
```

Header:

```javascript
headers: {
    "Authorization": `Bearer ${token}`
}
```

---

## 5. Dashboard

Dashboard hiển thị:

- User name.
- Balance.
- Total Income.
- Total Expense.
- Danh sách giao dịch.
- Form thêm giao dịch.
- AWS Lambda Statistics
- Biểu đồ theo Category.
![alt text](/WorkshopAWS/images/4-Workshop/4.6/dashbroadfull.png)
---

## 6. Chart.js

Thêm Chart.js:

```html
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
```

Dữ liệu biểu đồ lấy từ:

```text
GET http://localhost:3000/api/expenses/summary/category
```
![alt text](/WorkshopAWS/images/4-Workshop/4.6/Chart.png)
Sau đó tạo Doughnut Chart để hiển thị tỷ lệ chi tiêu theo Category.

---

## 7. Thêm giao dịch

Form gồm:

```text
Title
Amount
Type
Category
Date
```

Frontend gửi:

```text
POST http://localhost:3000/api/expenses
```
![alt text](/WorkshopAWS/images/4-Workshop/4.6/add_trans.png)
Sau khi thêm thành công, Dashboard cập nhật lại danh sách và số liệu.


---
## 8. Tự động cập nhật thống kê chi tiêu

* Cho phép người dùng xem trực tiếp bảng thống kê chi tiêu.
![alt text](/WorkshopAWS/images/4-Workshop/4.6/Lambda_Statistics.png)
---
## 9. Giao dịch gần đây
![alt text](/WorkshopAWS/images/4-Workshop/4.6/recent_trans.png)
* Cho phép người dùng xem trực tiếp các giao dịch gần đây.

---

## 10. Logout

Khi Logout:

```javascript
localStorage.removeItem("token");
localStorage.removeItem("user");
```
![alt text](/WorkshopAWS/images/4-Workshop/4.6/logout.png)

Sau đó chuyển về trang Login.

---

## 10. Kết quả

Frontend hoàn chỉnh gồm:

```text
Register
   ↓
Login
   ↓
Dashboard
   ├── Balance
   ├── Income
   ├── Expense
   ├── Chart
   └── Transactions
```

Frontend sử dụng REST API để trao đổi dữ liệu với Backend.