---
title: "Tổng quan Workshop"
weight: 1
pre: " <b> 4.1 </b> "
---

# Expense Tracker - Hệ thống quản lý chi tiêu cá nhân trên AWS

## Mục tiêu

Workshop này hướng dẫn xây dựng và triển khai hệ thống **Expense Tracker (Quản lý chi tiêu cá nhân)** trên nền tảng AWS.

Hệ thống cho phép người dùng đăng ký tài khoản, đăng nhập bằng JWT, quản lý các khoản thu nhập và chi tiêu cá nhân, theo dõi lịch sử giao dịch và xem thống kê tài chính thông qua giao diện web.

Sau khi hoàn thành workshop, người học có thể hiểu được quy trình phát triển một ứng dụng web hoàn chỉnh từ giai đoạn xây dựng Backend, kết nối cơ sở dữ liệu, triển khai trên môi trường Cloud và giám sát hệ thống bằng các dịch vụ AWS.


## 1. Giới thiệu bài toán và giải pháp

Trong cuộc sống hàng ngày, việc quản lý thu nhập và chi tiêu cá nhân là một nhu cầu phổ biến. Tuy nhiên, nhiều người vẫn theo dõi các khoản giao dịch bằng phương pháp thủ công như ghi chú trên giấy hoặc sử dụng bảng tính, gây khó khăn trong việc tổng hợp và phân tích dữ liệu.

Hệ thống **Expense Tracker** được xây dựng nhằm giải quyết vấn đề này bằng cách cung cấp một nền tảng trực tuyến giúp người dùng quản lý tài chính cá nhân một cách đơn giản và hiệu quả.

Ứng dụng hỗ trợ các chức năng chính:

- Đăng ký tài khoản người dùng.
- Đăng nhập và xác thực bằng JWT Token.
- Thêm các giao dịch thu nhập và chi tiêu.
- Xem danh sách lịch sử giao dịch.
- Cập nhật và xóa giao dịch.
- Phân loại chi tiêu theo danh mục.
- Hiển thị thống kê tổng thu, tổng chi và số dư.


Thay vì chạy ứng dụng hoàn toàn trên máy tính cá nhân, workshop triển khai hệ thống trên nền tảng điện toán đám mây AWS.

Backend của ứng dụng được triển khai trên **Amazon EC2**, giúp cung cấp môi trường máy chủ ổn định để chạy ứng dụng Node.js.

Dữ liệu người dùng và giao dịch được lưu trữ trên **MongoDB Atlas**, kết hợp với hệ thống xác thực JWT nhằm đảm bảo mỗi người dùng chỉ có thể truy cập dữ liệu của chính mình.

Hệ thống được giám sát thông qua **Amazon CloudWatch**, giúp theo dõi trạng thái hoạt động, log ứng dụng và hỗ trợ xử lý lỗi trong quá trình vận hành.


## 2. Kiến trúc hệ thống

Kiến trúc hệ thống Expense Tracker bao gồm các thành phần chính:

* Người dùng (Client Browser)
* Internet Gateway
* Amazon VPC
* Public Subnet
* Amazon EC2
* Node.js Express Backend
* MongoDB Atlas Database
* IAM quản lý quyền truy cập AWS
* Amazon CloudWatch Monitoring


![Hình 1 – Kiến trúc hệ thống Expense Tracker](/Workshop/images/expense-tracker-architecture.png)


*Hình 1 – Kiến trúc hệ thống Expense Tracker trên AWS*


Luồng kiến trúc tổng quát:

