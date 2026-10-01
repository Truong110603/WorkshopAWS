---
title: "Cấu hình EventBridge và CloudWatch"
weight: 11
pre: " <b> 4.11 </b> "
---

# Cấu hình EventBridge và CloudWatch

## Mục tiêu

Thiết lập lịch tự động gọi Lambda và kiểm tra log thực thi bằng CloudWatch.

---

# 1. EventBridge Scheduler

## a.Tạo Scheduler

Tạo Scheduler:

```text
expense-tracker-daily-statistics
```
![alt text](/WorkshopAWS/images/4-Workshop/4.11/EventBridge1.png)
Target:

```text
expense-tracker-statistics
```
![alt text](/WorkshopAWS/images/4-Workshop/4.11/EventBridge3.png)
---

## b. Schedule

Schedule sử dụng:

```text
rate(1 day)
```
![alt text](/WorkshopAWS/images/4-Workshop/4.11/EventBridge2.png)
Lambda được gọi tự động theo lịch.

Trong quá trình kiểm tra có thể sử dụng schedule ngắn hơn để xác nhận Scheduler hoạt động.

---

## c. Input

Lambda không yêu cầu dữ liệu đầu vào:

```json
{}
```

Luồng:

```text
EventBridge
      ↓
Lambda
      ↓
MongoDB Atlas
      ↓
statistics
```

---

# 2. CloudWatch

## a. Lambda Logs

Lambda ghi log vào CloudWatch.

Log Group:

```text
/aws/lambda/expense-tracker-statistics
```

Truy cập:

```text
AWS Console
→ CloudWatch
→ Logs
→ Log groups
```
![alt text](/WorkshopAWS/images/4-Workshop/4.11/Cloudwatchgroup.png)
---

## b. Nội dung Log

Các thông tin được ghi trong quá trình Lambda chạy:

![alt text](/WorkshopAWS/images/4-Workshop/4.11/CloudwatchLogStream.png)

---
## c. Cloudwatch Alarms
![alt text](/WorkshopAWS/images/4-Workshop/4.11/CloudwatchAlarms.png)
 Dùng để cảnh báo khi 1 giá trị vượt quá ngưỡng đã đặt, cụ thể như trên hình đặt **CPUUtilization** đặt ở ngưỡng 80%

---
## 6. Theo dõi Lambda

CloudWatch được sử dụng để kiểm tra:

- Lambda có được gọi hay không.
- Thời gian thực thi.
- Log của Function.
- Kết quả xử lý.
- Các thông báo trong quá trình chạy.
![alt text](/WorkshopAWS/images/4-Workshop/4.11/CloudwatchLogEvent.png)
---

## 7. Luồng hoàn chỉnh

```text
EventBridge Scheduler
          ↓
expense-tracker-statistics
          ↓
MongoDB Atlas
          ↓
statistics
          ↓
Backend API
          ↓
Frontend
```

CloudWatch theo dõi quá trình Lambda:

```text
Lambda
   ↓
CloudWatch Logs
```

---

## 8. Kết quả

EventBridge Scheduler và CloudWatch hoàn thiện phần tự động xử lý và theo dõi Lambda của hệ thống.