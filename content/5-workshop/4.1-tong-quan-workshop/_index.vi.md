---
title: "Tổng quan Workshop"
weight: 1
pre: " <b> 4.1 </b> "
---


## Mục tiêu

Workshop hướng dẫn xây dựng và triển khai hệ thống **Expense Tracker - Quản lý chi tiêu cá nhân** trên nền tảng AWS.

Hệ thống cho phép người dùng đăng ký, đăng nhập, quản lý các giao dịch thu chi, xem thống kê tài chính và triển khai ứng dụng thực tế trên môi trường Cloud.

## Giới thiệu bài toán và giải pháp

Expense Tracker giải quyết nhu cầu theo dõi thu nhập và chi tiêu cá nhân. Ứng dụng được xây dựng với:

- Frontend HTML/CSS/JavaScript.
- Backend Node.js Express.
- Xác thực người dùng bằng JWT.
- Database MongoDB Atlas.

Kiến trúc triển khai:

```
User
 |
Internet
 |
Internet Gateway
 |
VPC
 |
Public Subnet
 |
EC2 (Node.js Express)
 |
MongoDB Atlas
```

Hệ thống sử dụng Amazon CloudWatch để theo dõi log và trạng thái hoạt động của ứng dụng.

