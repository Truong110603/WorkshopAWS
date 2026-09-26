---
title: "Đề xuất "
weight: 2
pre: " <b> 2. </b> "
---

# ỨNG DỤNG QUẢN LÝ CHI TIÊU CÁ NHÂN (EXPENSE TRACKER APPLICATION)

## 1. Thông tin chung (General Information)

* **Tên đề tài (Project Title):** Xây dựng ứng dụng quản lý chi tiêu cá nhân trên nền tảng Web (Personal Expense Tracker Web Application).
* **Thành viên thực hiện (Author):** Nguyễn Xuân Trường
* **Bối cảnh (Context):** Trong cuộc sống hiện đại, việc quản lý tài chính cá nhân ngày càng trở nên quan trọng. Tuy nhiên, nhiều người vẫn gặp khó khăn trong việc theo dõi các khoản thu nhập, chi tiêu hằng ngày do thiếu một công cụ quản lý tập trung và trực quan.
* Đề tài này xây dựng một hệ thống quản lý chi tiêu cá nhân giúp người dùng ghi nhận các giao dịch tài chính, phân loại khoản chi, theo dõi ngân sách và phân tích thói quen sử dụng tiền thông qua các biểu đồ thống kê trực quan.

## 2. Bài toán và Mục tiêu (Problem Statement & Objectives)

### 2.1. Bối cảnh và Bài toán (Context & Problem)
* **Hệ thống dùng để làm gì?** Hệ thống Expense Tracker được xây dựng nhằm hỗ trợ người dùng quản lý toàn bộ hoạt động tài chính cá nhân.
* Người dùng có thể:
<br>-Thêm các khoản thu nhập.
<br>-Ghi nhận các khoản chi tiêu.
<br>-Phân loại giao dịch theo nhóm.
<br>-Theo dõi lịch sử sử dụng tiền.
<br>-Xem báo cáo thống kê tài chính theo thời gian.

Hệ thống lưu trữ dữ liệu tập trung trên cơ sở dữ liệu đám mây, cho phép truy cập nhanh chóng và bảo mật thông tin cá nhân.
* **Đối tượng sử dụng (Target Users):** -Sinh viên muốn kiểm soát chi phí sinh hoạt.
<br>-Nhân viên văn phòng muốn quản lý thu nhập và chi tiêu hàng tháng.
<br>-Người dùng cá nhân có nhu cầu lập kế hoạch tài chính.
* **Vấn đề giải quyết (Problem Solved):** Khắc phục các hạn chế của phương pháp quản lý truyền thống như:

<br>-Ghi chép thủ công bằng giấy dễ thất lạc.
<br>-Sử dụng Excel khó theo dõi trên nhiều thiết bị.
<br>-Không có biểu đồ phân tích trực quan.
<br>-Không có cảnh báo khi vượt quá ngân sách.

<br>Hệ thống cung cấp một giải pháp số hóa giúp người dùng kiểm soát tài chính hiệu quả hơn.

### 2.2. Mục tiêu cụ thể (Specific Objectives)
* **Output mong muốn:**
  * Hệ thống đăng ký và đăng nhập người dùng.
  * Module quản lý thu nhập và chi tiêu.
  * Hệ thống phân loại giao dịch theo danh mục.
  * Dashboard thống kê tài chính trực quan.
  * Biểu đồ phân tích xu hướng chi tiêu.
  * Cơ sở dữ liệu lưu trữ thông tin người dùng và giao dịch.
  * API Backend phục vụ giao tiếp giữa giao diện và cơ sở dữ liệu.
* **Tiêu chí đánh giá thành công (Success Criteria):**
  * Người dùng có thể tạo tài khoản và đăng nhập thành công.
  * Các giao dịch được lưu trữ chính xác vào cơ sở dữ liệu.
  * Dashboard hiển thị đúng tổng thu nhập, tổng chi tiêu và số dư.
  * Biểu đồ thống kê phản ánh chính xác dữ liệu thực tế.
  * Dữ liệu cá nhân được phân quyền bảo mật, mỗi người dùng chỉ truy cập được dữ liệu của chính mình.
## 3. Kiến trúc và Thiết kế Kỹ thuật (Architecture & Technical Design)

## Sơ đồ kiến trúc (Architecture Diagram)
![Sơ đồ kiến trúc Hệ thống Tự động xử lý hình ảnh Serverless](/Workshop/images/sodo.jpg)

### 3.1. Các dịch vụ AWS sử dụng (AWS Services Selection)
* **ReactJS + TypeScript (Frontend):** Sử dụng để xây dựng giao diện người dùng hiện đại, có khả năng tương tác cao.
<br>Các chức năng chính:
<br>-Hiển thị dashboard.
<br>-Quản lý giao dịch.
<br>-Hiển thị biểu đồ thống kê.
<br>-Tương tác với REST API.
* **Node.js + Express.js (Backend):**
<br>Được lựa chọn để xây dựng hệ thống API xử lý nghiệp vụ.
<br>Backend chịu trách nhiệm:

<br>-Xác thực người dùng.
<br>-Kiểm tra dữ liệu đầu vào.
<br>-Xử lý logic giao dịch.
<br>-Kết nối với cơ sở dữ liệu.
* **MongoDB Atlas (Database):**
<br>Sử dụng cơ sở dữ liệu NoSQL MongoDB để lưu trữ:
<br>-Thông tin tài khoản.
<br>-Danh sách giao dịch.
<br>-Danh mục chi tiêu.
<br>-Dữ liệu thống kê.
<br>MongoDB phù hợp với hệ thống có dữ liệu thay đổi linh hoạt và dễ dàng mở rộng.
* **AWS Lambda:** Dịch vụ tính toán Serverless. Được lựa chọn vì không cần quản trị hệ thống phần cứng, chỉ tính phí theo số lượng request thực tế và tự động co giãn theo tải.
* **Amazon DynamoDB:** Cơ sở dữ liệu NoSQL hiệu năng cao, quản lý toàn bộ dữ liệu cấu trúc nhẹ của tệp hình ảnh.
* **Amazon CloudWatch:** Giám sát, thu thập log và đo lường hiệu suất hoạt động của hàm Lambda.

### 3.2. Bảo mật và Nguyên tắc Least Privilege (Security & IAM)
* Hệ thống cấu hình IAM Role riêng biệt cho AWS Lambda.
* Tuân thủ tuyệt đối nguyên tắc Least Privilege (Quyền tối thiểu): Hàm Lambda chỉ có quyền GetObject trên kho gốc, PutObject trên kho đích, quyền ghi log vào CloudWatch và quyền ghi dữ liệu vào bảng DynamoDB định sẵn. Không sử dụng quyền quản trị toàn cục (AdministratorAccess).

## 4. Rủi ro Tiềm ẩn và Hướng giải quyết (Potential Risks & Mitigation)

* **Rủi ro 1: Mất dữ liệu giao dịch (Data Loss)**
  * *Mô tả:* Dữ liệu chi tiêu của người dùng có thể bị mất do lỗi database hoặc thao tác sai.
  * *Hướng giải quyết:*
    <br>-Sử dụng MongoDB Atlas có cơ chế backup.
    <br>-Kiểm tra dữ liệu trước khi lưu.
    <br>-Xây dựng chức năng xác nhận trước khi xóa.
* **Rủi ro 2: Lỗi phân quyền bảo mật (IAM Permission Denied)**
  * *Mô tả:* Hàm Lambda không có quyền đọc/ghi bucket hoặc không thể kết nối vào bảng DynamoDB do cấu hình IAM Role sai.
  * *Hướng giải quyết:* Kiểm tra kỹ cấu hình ARN của tài nguyên trong IAM Policy, đồng thời sử dụng Amazon CloudWatch Logs để truy vết mã lỗi chính xác ngay khi gặp sự cố thực thi.
* **Rủi ro 3: Phát sinh chi phí ngoài ý muốn (Cost Overruns)**
  * *Mô tả:* Quên dọn dẹp các tài nguyên sau khi thử nghiệm làm phát sinh chi phí vượt định mức Free Tier.
  * *Hướng giải quyết:* Xây dựng sẵn quy trình dọn dẹp tài nguyên (Clean-up steps) sau khi hoàn tất lab và kiểm tra định kỳ trên bảng điều khiển AWS Billing.

## 5. Kế hoạch Triển khai Lab (Implementation Lab Steps)

Dự án được triển khai qua các bước chuẩn hóa end-to-end:
* **Bước 1:** Khởi tạo 2 Amazon S3 Bucket (Input và Output).
* **Bước 2:** Tạo bảng Amazon DynamoDB để lưu vết metadata hình ảnh.
* **Bước 3:** Thiết lập IAM Policy và IAM Role tuân thủ nguyên tắc Least Privilege.
* **Bước 4:** Xây dựng hàm AWS Lambda (Python) xử lý logic sao chép và ghi dữ liệu.
* **Bước 5:** Cấu hình S3 Event Trigger để kích hoạt tự động hàm Lambda khi có tệp mới.
* **Bước 6:** Kiểm thử (Test), xác thực kết quả trên DynamoDB và kiểm tra CloudWatch Logs.
* **Bước 7:** Thực hiện dọn dẹp tài nguyên (Clean-up) để tối ưu chi phí.

## 6. Đóng góp Cá nhân và Sáng tạo (Personal Contributions & Customization)

* **Tùy biến mở rộng:** Không chỉ dừng lại ở việc sao chép tệp đơn thuần, hệ thống tích hợp thêm Amazon DynamoDB để tự động trích xuất, định hình và lưu trữ thông tin chi tiết (tên tệp, dung lượng, thời gian xử lý), phục vụ cho việc thống kê báo cáo.
* **Định hướng phát triển tương lai:** Tích hợp thêm giao diện web tĩnh (Static Web Front-end) trên S3 kết hợp chính sách CORS để người dùng cuối có thể thao tác trực tiếp qua trình duyệt web một cách trực quan.
