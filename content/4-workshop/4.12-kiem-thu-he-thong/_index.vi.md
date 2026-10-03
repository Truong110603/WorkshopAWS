---
title: "Kiểm thử hệ thống"
weight: 12
pre: " <b> 4.12 </b> "
---

# Kiểm thử hệ thống

## Mục tiêu

Kiểm tra các chức năng của Expense Tracker sau khi Backend được triển khai trên EC2 và các thành phần AWS đã được cấu hình.

---

## 1. Kiểm tra EC2

Kết nối:

```bash
ssh -i ".\expense-tracker-key.pem" ubuntu@47.129.176.80
```

Kiểm tra PM2:

```bash
pm2 status
```
![alt text](/WorkshopAWS/images/4-Workshop/4.9/pm2status-api-health.png)
Kiểm tra log:

```bash
pm2 logs expense-tracker
```
![alt text](/WorkshopAWS/images/4-Workshop/4.12/ubuntu_check_log.png)
---

## 2. Health API

```bash
curl http://localhost:3000/api/health
```

Response:

```json
{
    "status": "ok"
}
```
![alt text](/WorkshopAWS/images/4-Workshop/4.9/pm2status-api-health.png)
---

## 3. Kiểm tra Register

Truy cập trang Register và nhập:

```text
Name
Email
Password
```
![alt text](/WorkshopAWS/images/4-Workshop/4.12/signup_test.png)
Kiểm tra User trong:

```text
MongoDB Atlas
→ expensetracker
→ users
```
![alt text](/WorkshopAWS/images/4-Workshop/4.12/database_signup_test.png)
---

## 4. Kiểm tra Login

Đăng nhập bằng tài khoản đã tạo.

Kiểm tra:

```text
Login
   ↓
JWT
   ↓
Dashboard
```
![alt text](/WorkshopAWS/images/4-Workshop/4.12/login-test.png)
---

## 5. Thêm giao dịch

Thêm một giao dịch:

```text
Title: Ăn tối
Amount: 100000
Type: expense
Category: Food
Date: 2026-09-30
```
![alt text](/WorkshopAWS/images/4-Workshop/4.6/add_trans.png)
Kiểm tra trong:

```text
MongoDB Atlas
→ expensetracker
→ expenses
```

Document có:

```text
userId
title
amount
type
category
date
```
![alt text](/WorkshopAWS/images/4-Workshop/4.12/database_add_test.png)
---

## 6. Kiểm tra Dashboard

Kiểm tra các thành phần:

```text
Balance
Total Income
Total Expense
Transactions
Category Chart
```

Các số liệu được lấy từ API Backend.

---

## 7. Kiểm tra Update

Chọn một giao dịch và cập nhật thông tin.

Kiểm tra lại:

```text
Dashboard
API
MongoDB Atlas
```

---

## 8. Kiểm tra Delete

Xóa một giao dịch.

Kiểm tra lại danh sách giao dịch và collection:

```text
expenses
```

---

## 9. Kiểm tra User Data
![alt text](/WorkshopAWS/images/4-Workshop/4.12/database_user_test.png)
Tạo hai tài khoản:


**User A**
![alt text](/WorkshopAWS/images/4-Workshop/4.12/test_user1.png)


**User B**
![alt text](/WorkshopAWS/images/4-Workshop/4.12/test_user2.png)

Tạo giao dịch cho User A.

Đăng nhập bằng User B và kiểm tra danh sách giao dịch.

API chỉ trả về dữ liệu theo:

```text
userId
```


---

## 10. Kiểm tra Authentication

Gọi:

```text
GET /api/expenses
```

không có token.

Response:

```text
401 Unauthorized
```
![alt text](/WorkshopAWS/images/4-Workshop/4.7/callapiWithoutJWT.png)
Gửi:

```text
Authorization: Bearer <TOKEN>
```
![alt text](/WorkshopAWS/images/4-Workshop/4.7/callapiWithJWT.png)
API có thể truy cập.

---

## 11. Kiểm tra Lambda

Function:

```text
expense-tracker-statistics
```

Kết quả:

```json
{
    "statusCode": 200,
    "body": "{\"message\":\"Thống kê chi tiêu thành công\",\"expensesFound\":16,\"usersProcessed\":2}"
}
```
![alt text](/WorkshopAWS/images/4-Workshop/4.10/lambdaTest.png)
Kiểm tra collection:

```text
expensetracker
→ statistics
```

---

## 12. Kiểm tra EventBridge

Scheduler:

```text
expense-tracker-daily-statistics
```

Target:

```text
expense-tracker-statistics
```
![alt text](/WorkshopAWS/images/4-Workshop/4.11/EventBridge2.png)

![alt text](/WorkshopAWS/images/4-Workshop/4.11/CloudwatchLogEvent.png)

Kiểm tra trạng thái Scheduler và các lần gọi Lambda.

---

## 13. Kiểm tra CloudWatch

Log Group:

```text
/aws/lambda/expense-tracker-statistics
```

Kiểm tra Log Stream sau khi Lambda được gọi.

Các log chính:

```text
Connected to MongoDB Atlas
Total expenses found: 16
Users found: 2
Statistics saved for user: ...
```
![alt text](/WorkshopAWS/images/4-Workshop/4.11/CloudwatchLogStream.png)
---

## 14. Kiểm tra toàn bộ hệ thống

![Hình 1 – Kiến trúc hệ thống quản lý chi tiêu](/Workshop/images/architecture-diagram.png)
*Hình 1 – Kiến trúc hệ thống quản lý chi tiêu

---

## 15. Các thành phần hoàn thành

| Thành phần | Trạng thái |
|---|---|
| Node.js | Hoàn thành |
| Express | Hoàn thành |
| MongoDB Atlas | Hoàn thành |
| Register | Hoàn thành |
| Login | Hoàn thành |
| JWT | Hoàn thành |
| bcrypt | Hoàn thành |
| Expense CRUD | Hoàn thành |
| Dashboard | Hoàn thành |
| Chart.js | Hoàn thành |
| EC2 | Hoàn thành |
| PM2 | Hoàn thành |
| Lambda | Hoàn thành |
| EventBridge | Hoàn thành |
| CloudWatch | Hoàn thành |

---

## 16. Kết quả

Expense Tracker có thể chạy trên EC2 và kết nối với MongoDB Atlas để lưu trữ dữ liệu.

Người dùng có thể đăng ký, đăng nhập và quản lý các giao dịch của tài khoản.

Lambda thực hiện thống kê dữ liệu và lưu kết quả vào collection `statistics`. EventBridge gọi Lambda theo lịch và CloudWatch lưu log để theo dõi quá trình thực thi.

Kiến trúc cuối cùng:

![Hình 1 – Kiến trúc hệ thống quản lý chi tiêu](/WorkshopAWS/images/4-Workshop/4.2/Exspense_Tracker_Architecture_Diagram.drawio.png)
*Hình 1 – Kiến trúc hệ thống quản lý chi tiêu
