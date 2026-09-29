---
title: "Tổng quan Workshop"
weight: 1
pre: " <b> 4.1 </b> "
---

## Mục tiêu

Workshop này hướng dẫn xây dựng và triển khai ứng dụng **Expense Tracker (Hệ thống quản lý chi tiêu cá nhân)** trên nền tảng AWS bằng cách sử dụng mô hình triển khai Cloud Computing, dịch vụ máy chủ ảo Amazon EC2, hệ thống mạng Amazon VPC, quản lý quyền truy cập AWS IAM và dịch vụ giám sát Amazon CloudWatch.

Sau khi hoàn thành workshop, bạn sẽ có thể triển khai một ứng dụng web hoàn chỉnh với khả năng xác thực người dùng, quản lý dữ liệu giao dịch cá nhân, kết nối cơ sở dữ liệu trên Cloud và vận hành ứng dụng trên môi trường AWS.


## 1. Giới thiệu bài toán và giải pháp

**Expense Tracker** là một ứng dụng web hỗ trợ người dùng quản lý các khoản thu nhập và chi tiêu cá nhân một cách trực quan và hiệu quả.

Trong thực tế, việc theo dõi tài chính cá nhân thường gặp khó khăn khi người dùng phải ghi chép thủ công hoặc sử dụng nhiều công cụ khác nhau. Điều này gây khó khăn trong việc tổng hợp dữ liệu, kiểm soát chi tiêu và phân tích tình hình tài chính.

Hệ thống Expense Tracker được xây dựng nhằm giải quyết vấn đề trên bằng cách cung cấp một nền tảng trực tuyến cho phép người dùng:

- Đăng ký tài khoản cá nhân.
- Đăng nhập bảo mật bằng JWT Authentication.
- Quản lý các giao dịch thu nhập và chi tiêu.
- Thêm, sửa, xóa các khoản giao dịch.
- Phân loại chi tiêu theo từng nhóm.
- Theo dõi tổng thu nhập, tổng chi tiêu và số dư hiện tại.
- Xem lịch sử giao dịch cá nhân.


Thay vì chỉ chạy ứng dụng trên môi trường máy tính cá nhân, workshop này triển khai hệ thống trên nền tảng AWS nhằm mô phỏng quy trình triển khai một ứng dụng web thực tế trên Cloud.

Backend của hệ thống được xây dựng bằng **Node.js và Express.js**, sau đó được triển khai trên **Amazon EC2**.

Dữ liệu người dùng và dữ liệu giao dịch được lưu trữ trên **MongoDB Atlas**, đảm bảo khả năng mở rộng và quản lý dữ liệu hiệu quả.

Hệ thống sử dụng **JWT Token** để xác thực người dùng, đảm bảo mỗi tài khoản chỉ có thể truy cập và quản lý dữ liệu của chính mình.

Toàn bộ quá trình hoạt động của ứng dụng được giám sát thông qua **Amazon CloudWatch**, giúp theo dõi trạng thái máy chủ, log ứng dụng và hỗ trợ xử lý sự cố.


## 2. Kiến trúc hệ thống

Kiến trúc của hệ thống bao gồm các thành phần chính sau:

* Người dùng (Client Browser)
* Giao diện Web Frontend (HTML/CSS/JavaScript)
* Amazon VPC (Virtual Private Cloud)
* Public Subnet
* Internet Gateway
* Amazon EC2 (Backend Server)
* Node.js Express API
* MongoDB Atlas Database
* Quản lý danh tính và quyền hạn AWS IAM
* Giám sát hệ thống Amazon CloudWatch


![Hình 1 – Kiến trúc hệ thống Expense Tracker](/Workshop/images/expense-tracker-architecture.png)

*Hình 1 – Kiến trúc hệ thống Expense Tracker trên AWS (Lưu ý: Hãy đảm bảo bạn đã lưu ảnh sơ đồ kiến trúc vào thư mục `/images/expense-tracker-architecture.png`)*


Kiến trúc tổng quát:

## 3. Quy trình hoạt động của hệ thống

Luồng xử lý chính của hệ thống diễn ra theo các bước sau:

1. Người dùng truy cập ứng dụng Expense Tracker thông qua trình duyệt web.

2. Người dùng đăng ký hoặc đăng nhập tài khoản. Hệ thống xác thực thông tin người dùng và cấp JWT Token để duy trì phiên đăng nhập.

3. Sau khi đăng nhập thành công, người dùng thực hiện các thao tác quản lý chi tiêu như thêm, xem, cập nhật hoặc xóa giao dịch.

4. Frontend gửi các yêu cầu HTTP (Request) đến Backend thông qua các REST API.

5. Backend Node.js trên Amazon EC2 tiếp nhận và xử lý yêu cầu, kiểm tra quyền truy cập thông qua JWT Token.

6. Dữ liệu người dùng và thông tin giao dịch được lưu trữ, truy vấn và cập nhật trên MongoDB Atlas.

7. Hệ thống phân tách dữ liệu theo từng tài khoản người dùng, đảm bảo mỗi người dùng chỉ có thể quản lý các giao dịch của chính mình.

8. Amazon EC2 duy trì hoạt động của ứng dụng Backend thông qua PM2, đảm bảo dịch vụ luôn sẵn sàng xử lý yêu cầu.

9. Nhật ký hoạt động và trạng thái hệ thống được theo dõi thông qua Amazon CloudWatch để hỗ trợ giám sát và xử lý sự cố.

## 4. Các dịch vụ được sử dụng

Workshop sử dụng các dịch vụ AWS sau:

* **Dịch vụ tính toán (Compute)**
  * Amazon EC2

* **Mạng (Networking)**
  * Amazon VPC
  * Public Subnet
  * Internet Gateway

* **Cơ sở dữ liệu (Database)**
  * MongoDB Atlas

* **Bảo mật & Quản lý (Security & Management)**
  * AWS Identity and Access Management (IAM)

* **Giám sát (Monitoring)**
  * Amazon CloudWatch


## 5. Kết quả đạt được

Sau khi hoàn thành workshop, bạn sẽ có thể:

* Xây dựng ứng dụng quản lý chi tiêu cá nhân với kiến trúc Web Application.

* Triển khai Backend Node.js trên môi trường máy chủ Amazon EC2.

* Xây dựng hệ thống xác thực người dùng bằng JWT và quản lý quyền truy cập dữ liệu.

* Thiết kế và triển khai REST API phục vụ các chức năng quản lý giao dịch.

* Kết nối ứng dụng với cơ sở dữ liệu MongoDB Atlas để lưu trữ thông tin người dùng và dữ liệu chi tiêu.

* Cấu hình hệ thống mạng AWS bao gồm VPC, Subnet và Internet Gateway.

* Quản lý quyền truy cập tài nguyên AWS thông qua IAM.

* Sử dụng PM2 để duy trì và quản lý tiến trình ứng dụng trên máy chủ.

* Theo dõi trạng thái hoạt động, log và lỗi hệ thống thông qua Amazon CloudWatch.

* Hiểu được quy trình triển khai một ứng dụng Web thực tế trên nền tảng Cloud AWS.
