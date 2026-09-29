---
title: "Tổng quan Workshop"
weight: 1
pre: " <b> 4.1 </b> "
---

## Mục tiêu

Workshop này hướng dẫn triển khai ứng dụng **Expense Tracker – Hệ thống Quản lý Chi tiêu** trên nền tảng AWS bằng cách kết hợp các dịch vụ điện toán đám mây, cơ sở dữ liệu được quản lý (Managed Database), kiến trúc xử lý serverless và luồng thực thi tự động theo lịch (Scheduled Processing).

Sau khi hoàn thành workshop, bạn sẽ có thể triển khai một ứng dụng web quản lý tài chính cá nhân hoàn chỉnh với khả năng xác thực người dùng, quản lý dữ liệu thu chi, thống kê tài chính tự động và giám sát hoạt động của hệ thống thông qua Amazon CloudWatch.

---

## 1. Giới thiệu bài toán và giải pháp

**Expense Tracker** là một ứng dụng web hỗ trợ người dùng quản lý các khoản thu nhập và chi tiêu cá nhân.

Hệ thống cung cấp các chức năng như đăng ký tài khoản, đăng nhập, thêm giao dịch, xem lịch sử giao dịch, cập nhật giao dịch, xóa giao dịch và thống kê tình hình tài chính.

Mỗi giao dịch được lưu trữ cùng với thông tin người dùng tương ứng, giúp hệ thống đảm bảo mỗi người dùng chỉ có thể truy cập và quản lý dữ liệu của chính mình.

Thay vì chỉ chạy ứng dụng trên máy tính cá nhân, workshop này triển khai Backend của hệ thống trên **Amazon EC2**. Backend được xây dựng bằng **Node.js và Express.js**, cung cấp các REST API để giao tiếp giữa giao diện Web và cơ sở dữ liệu.

Dữ liệu của hệ thống được lưu trữ trên **MongoDB Atlas**, bao gồm thông tin tài khoản người dùng, các giao dịch thu chi và dữ liệu thống kê.

Để thực hiện các tác vụ thống kê độc lập với Backend chính, hệ thống sử dụng **AWS Lambda**. Lambda thực hiện việc tổng hợp dữ liệu chi tiêu theo từng người dùng và lưu kết quả vào collection `statistics` trong MongoDB Atlas.

**Amazon EventBridge Scheduler** được sử dụng để tự động kích hoạt Lambda theo lịch định kỳ, giúp hệ thống có thể cập nhật dữ liệu thống kê mà không cần người dùng thực hiện thủ công.

Hệ thống được giám sát thông qua **Amazon CloudWatch**, trong đó các log thực thi của Lambda và các thông tin giám sát liên quan đến EC2 được sử dụng để kiểm tra hoạt động và phát hiện lỗi.

Quyền truy cập các tài nguyên AWS được quản lý thông qua **AWS Identity and Access Management (IAM)**.

---

## 2. Kiến trúc hệ thống

Kiến trúc của hệ thống bao gồm các thành phần chính sau:

* Người dùng (Client Browser)
* Giao diện Web Expense Tracker
* Amazon VPC
* Public Subnet
* Internet Gateway
* Amazon EC2
* Node.js / Express.js Backend
* MongoDB Atlas
* AWS Lambda
* Amazon EventBridge Scheduler
* AWS Identity and Access Management (IAM)
* Amazon CloudWatch

![Hình 1 – Kiến trúc hệ thống Expense Tracker](/Workshop/images/expense-tracker-architecture.png)

*Hình 1 – Kiến trúc hệ thống Expense Tracker (Lưu ý: Hãy đảm bảo bạn đã lưu ảnh sơ đồ kiến trúc vào thư mục `/images/expense-tracker-architecture.png`)*

Kiến trúc tổng thể:

## 3. Quy trình hoạt động của hệ thống

Luồng xử lý chính của hệ thống diễn ra theo các bước sau:

1. Người dùng truy cập website Expense Tracker thông qua địa chỉ của ứng dụng được triển khai trên Amazon EC2.

2. Người dùng thực hiện đăng ký tài khoản hoặc đăng nhập vào hệ thống. Thông tin tài khoản được xử lý thông qua REST API và mật khẩu được mã hóa bằng thư viện bcrypt trước khi lưu vào MongoDB Atlas.

3. Sau khi đăng nhập thành công, hệ thống tạo một JSON Web Token (JWT) và gửi token về trình duyệt. Token được lưu tại LocalStorage và được sử dụng để xác thực các request tiếp theo.

4. Khi người dùng thêm một giao dịch thu nhập hoặc chi tiêu, trình duyệt gửi dữ liệu thông qua REST API đến Backend Node.js/Express đang chạy trên Amazon EC2.

5. Backend kiểm tra JWT để xác định người dùng thực hiện request, sau đó lưu thông tin giao dịch vào MongoDB Atlas. Mỗi giao dịch được gắn với `userId` tương ứng để đảm bảo dữ liệu của từng người dùng được phân biệt.

6. Khi người dùng truy cập Dashboard, Backend truy vấn MongoDB Atlas để lấy danh sách giao dịch và thực hiện các phép tính tổng thu nhập, tổng chi tiêu, số dư và thống kê theo danh mục.

7. Dashboard hiển thị dữ liệu thống kê cho người dùng thông qua giao diện web và biểu đồ Chart.js, giúp người dùng theo dõi tình hình thu nhập và chi tiêu.

8. Theo lịch được cấu hình bằng Amazon EventBridge Scheduler, AWS Lambda `expense-tracker-statistics` được tự động kích hoạt để thực hiện quá trình thống kê dữ liệu chi tiêu.

9. AWS Lambda kết nối đến MongoDB Atlas, truy vấn dữ liệu giao dịch và thực hiện thống kê riêng cho từng người dùng. Kết quả thống kê bao gồm tổng số giao dịch, tổng thu nhập và tổng chi tiêu, sau đó được lưu vào collection `statistics` trong cơ sở dữ liệu `expensetracker`.

10. Backend cung cấp API `/api/expenses/lambda-statistics` để lấy kết quả thống kê mới nhất do AWS Lambda tạo ra. Dashboard có thể sử dụng API này để hiển thị kết quả xử lý từ Lambda.

11. Nhật ký hoạt động và lỗi thực thi của AWS Lambda được ghi nhận trên Amazon CloudWatch. CloudWatch đồng thời được sử dụng để theo dõi hoạt động của các tài nguyên AWS và hỗ trợ việc kiểm tra, giám sát hệ thống.

## 4. Các dịch vụ được sử dụng

Workshop sử dụng các dịch vụ AWS và công nghệ sau:

* **Dịch vụ tính toán (Compute)**
  * Amazon EC2
  * AWS Lambda

* **Mạng & triển khai (Networking & Deployment)**
  * Amazon VPC
  * Public Subnet
  * Internet Gateway
  * Security Group

* **Cơ sở dữ liệu (Database)**
  * MongoDB Atlas

* **Tự động hóa (Automation)**
  * Amazon EventBridge Scheduler

* **Bảo mật & Quản lý (Security & Management)**
  * AWS Identity and Access Management (IAM)

* **Giám sát (Monitoring)**
  * Amazon CloudWatch

* **Công nghệ ứng dụng (Application Technologies)**
  * Node.js
  * Express.js
  * REST API
  * JWT
  * bcrypt
  * Mongoose
  * Chart.js

## 5. Kết quả đạt được

Sau khi hoàn thành workshop, bạn sẽ có thể:

* Xây dựng ứng dụng quản lý thu nhập và chi tiêu với kiến trúc Backend Node.js/Express kết hợp MongoDB Atlas.

* Triển khai ứng dụng web lên Amazon EC2 và cho phép người dùng truy cập thông qua Internet.

* Thiết kế và triển khai REST API phục vụ các chức năng đăng ký, đăng nhập và quản lý giao dịch.

* Xây dựng cơ chế xác thực người dùng bằng JSON Web Token (JWT) và mã hóa mật khẩu bằng bcrypt.

* Thiết kế cơ sở dữ liệu MongoDB Atlas để lưu trữ thông tin người dùng, giao dịch và dữ liệu thống kê.

* Thực hiện các chức năng thêm, xem, cập nhật và xóa giao dịch thu nhập hoặc chi tiêu.

* Xây dựng Dashboard hiển thị tổng thu nhập, tổng chi tiêu, số dư và biểu đồ thống kê theo danh mục bằng Chart.js.

* Xây dựng chức năng Serverless bằng AWS Lambda để tự động thực hiện thống kê dữ liệu chi tiêu.

* Sử dụng Amazon EventBridge Scheduler để tự động kích hoạt AWS Lambda theo lịch được cấu hình.

* Lưu kết quả thống kê được xử lý bởi AWS Lambda vào MongoDB Atlas và cung cấp API để Backend truy vấn kết quả.

* Sử dụng Amazon CloudWatch Logs để theo dõi hoạt động, nhật ký và lỗi thực thi của AWS Lambda.

* Sử dụng Amazon IAM để quản lý quyền truy cập vào các tài nguyên AWS cần thiết cho hệ thống.

* Hiểu và triển khai mô hình kết hợp giữa Amazon EC2 và AWS Lambda, trong đó EC2 đảm nhiệm Backend API còn Lambda đảm nhiệm các tác vụ xử lý thống kê tự động.

* Kiểm thử toàn bộ hệ thống từ đăng ký, đăng nhập, quản lý giao dịch, thống kê dữ liệu đến quá trình Lambda tự động xử lý.

* Dọn dẹp các tài nguyên AWS sau khi hoàn thành workshop để hạn chế phát sinh chi phí không cần thiết.
