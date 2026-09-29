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



Ngoài ra hệ thống sử dụng Amazon CloudWatch để thu thập log và giám sát trạng thái hoạt động của ứng dụng.


## 3. Quy trình hoạt động của hệ thống

Luồng hoạt động chính của hệ thống được thực hiện theo các bước:


### Bước 1: Người dùng truy cập hệ thống

Người dùng truy cập website thông qua địa chỉ Public IPv4 của Amazon EC2.

Trình duyệt gửi các request đến Backend API được xây dựng bằng Node.js.


### Bước 2: Đăng ký tài khoản

Người dùng nhập thông tin:

- Họ tên
- Email
- Mật khẩu


Backend tiếp nhận dữ liệu thông qua API:

![POST /api/auth/register]


Mật khẩu được mã hóa bằng thư viện bcrypt trước khi lưu vào MongoDB.


### Bước 3: Đăng nhập hệ thống

Người dùng gửi thông tin đăng nhập:
![POST /api/auth/login]



Backend kiểm tra thông tin tài khoản trong MongoDB.

Nếu hợp lệ, hệ thống tạo JWT Token và trả về cho Client.


JWT Token được lưu trong LocalStorage và được sử dụng trong các request tiếp theo.


### Bước 4: Quản lý giao dịch

Sau khi đăng nhập thành công, người dùng có thể:

- Thêm giao dịch mới.
- Xem danh sách giao dịch.
- Cập nhật dữ liệu.
- Xóa giao dịch.


Mỗi request gửi lên API đều kèm theo JWT:

![Authorization: Bearer <token>]



Middleware xác thực token trước khi cho phép truy cập dữ liệu.


### Bước 5: Lưu trữ dữ liệu

Backend Node.js sử dụng MongoDB Driver thông qua thư viện Mongoose để giao tiếp với MongoDB Atlas.


Dữ liệu giao dịch bao gồm:

- Tên giao dịch.
- Số tiền.
- Loại giao dịch.
- Danh mục.
- Ngày giao dịch.
- Người sở hữu dữ liệu.


Mỗi giao dịch được liên kết với User ID nhằm đảm bảo tính riêng tư.


### Bước 6: Triển khai trên AWS EC2

Ứng dụng Backend được triển khai trên Amazon EC2:


- Cấu hình Ubuntu Server.
- Cài đặt Node.js.
- Cài đặt npm packages.
- Chạy ứng dụng bằng PM2.
- Cấu hình Security Group mở cổng 3000.


PM2 giúp ứng dụng duy trì hoạt động ngay cả khi server được khởi động lại.


### Bước 7: Giám sát hệ thống

Amazon CloudWatch được sử dụng để:

- Theo dõi trạng thái EC2.
- Kiểm tra CPU, RAM.
- Theo dõi log ứng dụng.
- Phát hiện lỗi trong quá trình chạy.


## 4. Các dịch vụ được sử dụng


Workshop sử dụng các dịch vụ AWS sau:


## Compute

### Amazon EC2

Được sử dụng để triển khai Backend Node.js.

Chức năng:

- Cung cấp môi trường chạy ứng dụng.
- Quản lý tài nguyên máy chủ.
- Cho phép truy cập thông qua Public IPv4.


## Networking

### Amazon VPC

Tạo môi trường mạng riêng cho hệ thống.


### Public Subnet

Chứa EC2 Instance có khả năng truy cập Internet.


### Internet Gateway

Kết nối VPC với Internet.


## Security

### AWS IAM

Quản lý quyền truy cập AWS.


IAM được sử dụng để:

- Tạo User.
- Phân quyền quản lý tài nguyên.
- Kiểm soát quyền truy cập dịch vụ AWS.


## Database

### MongoDB Atlas

Lưu trữ:

- Thông tin người dùng.
- Danh sách giao dịch.
- Dữ liệu tài chính cá nhân.


## Monitoring

### Amazon CloudWatch

Dùng để:

- Thu thập log.
- Theo dõi hiệu suất.
- Kiểm tra trạng thái hệ thống.


## 5. Kết quả đạt được


Sau khi hoàn thành workshop, người học có thể:


* Xây dựng ứng dụng quản lý chi tiêu bằng Node.js và Express.

* Thiết kế hệ thống đăng nhập sử dụng JWT Authentication.

* Kết nối Backend với MongoDB Atlas.

* Xây dựng REST API phục vụ quản lý giao dịch.

* Triển khai ứng dụng Web trên Amazon EC2.

* Cấu hình VPC, Subnet và Internet Gateway.

* Quản lý quyền truy cập AWS bằng IAM.

* Sử dụng PM2 để quản lý tiến trình Node.js.

* Giám sát ứng dụng thông qua Amazon CloudWatch.

* Hiểu được quy trình triển khai một ứng dụng Web thực tế trên nền tảng Cloud.


Sau khi hoàn thành workshop, toàn bộ tài nguyên AWS có thể được xóa để tránh phát sinh chi phí ngoài mong muốn.



