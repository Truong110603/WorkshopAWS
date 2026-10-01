---
title: "Triển khai Expense Tracker lên EC2"
weight: 9
pre: " <b> 4.9 </b> "
---

# Triển khai Expense Tracker lên EC2

## Mục tiêu

Triển khai Backend Node.js lên EC2 Ubuntu và chạy ứng dụng bằng PM2.

---

## 1. Tạo EC2

Tạo EC2 instance sử dụng Ubuntu.

Instance được đặt trong:

```text
expense-tracker-vpc
    ↓
expense-tracker-public-subnet
```
![alt text](/WorkshopAWS/images/4-Workshop/4.9/EC2instances.png)
Security Group:

```text
expense-tracker-sg
```

Port sử dụng:

```text
22
3000
```
![alt text](/WorkshopAWS/images/4-Workshop/4.9/EC2instances-2.png)
---

## 2. SSH

Kết nối đến EC2:

```bash
ssh -i ".\expense-tracker-key.pem" ubuntu@47.129.176.80
```
![alt text](/WorkshopAWS/images/4-Workshop/4.9/ubuntu.png)
---

## 3. Tạo thư mục project

Trên EC2:

```bash
mkdir -p ~/expense-tracker
cd ~/expense-tracker
```

Backend được đặt tại:

```text
~/expense-tracker/backend
```

---

## 4. Cài đặt Node.js và npm

Kiểm tra:

```bash
node --version
npm --version
```

---

## 5. Cài đặt package

Di chuyển vào Backend:

```bash
cd ~/expense-tracker/backend
```

Cài package:

```bash
npm install
```

---

## 6. Cấu hình Environment Variables

Tạo:

```text
backend/.env
```

Nội dung:

```text
MONGO_URI=<MONGODB_CONNECTION_STRING>
PORT=3000
JWT_SECRET=<SECRET>
```

---

## 7. Chạy Backend

Chạy:

```bash
node server.js
```

Kiểm tra:

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

## 8. Cài PM2

```bash
sudo npm install -g pm2
```

Khởi động:

```bash
cd ~/expense-tracker/backend
pm2 start server.js --name expense-tracker
```

Kiểm tra:

```bash
pm2 status
```

Xem log:

```bash
pm2 logs expense-tracker
```

Restart:

```bash
pm2 restart expense-tracker
```
![alt text](/WorkshopAWS/images/4-Workshop/4.9/pm2status.png)
---

## 9. Truy cập ứng dụng

Truy cập:

```text
http://47.129.176.80:3000/:3000
```

Frontend được phục vụ từ Backend Express.

---

## 10. Kết quả

Backend chạy trên:

```text
Amazon EC2
    ↓
Node.js
    ↓
Express
    ↓
MongoDB Atlas
```

PM2 được sử dụng để chạy ứng dụng dưới dạng process nền.