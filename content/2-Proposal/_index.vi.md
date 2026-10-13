---
title: "Đề xuất"
weight: 2
pre: " <b> 2. </b> "
---

# XÂY DỰNG VÀ TRIỂN KHAI ỨNG DỤNG QUẢN LÝ CHI TIÊU CÁ NHÂN TRÊN AWS (EXPENSE TRACKER APPLICATION)

## 1. Thông tin chung (General Information)

* **Tên đề tài (Project Title):** Xây dựng và triển khai ứng dụng quản lý chi tiêu cá nhân trên nền tảng AWS.
* **Thành viên thực hiện (Author):** Nguyễn Hồng Quân
* **Bối cảnh (Context):** Trong cuộc sống hiện đại, việc theo dõi và quản lý thu nhập, chi tiêu cá nhân đóng vai trò quan trọng trong việc lập kế hoạch tài chính. Tuy nhiên, việc ghi chép thủ công khiến người dùng khó tổng hợp dữ liệu và đánh giá thói quen chi tiêu. Đề tài xây dựng ứng dụng Expense Tracker sử dụng Node.js, Express.js và MongoDB Atlas, triển khai backend trên Amazon EC2, đồng thời sử dụng AWS Lambda, Amazon EventBridge và Amazon CloudWatch để tự động hóa tác vụ thống kê và giám sát hệ thống.

## 2. Bài toán và Mục tiêu (Problem Statement & Objectives)

### 2.1. Bối cảnh và Bài toán (Context & Problem)

* **Hệ thống dùng để làm gì?** Hệ thống cung cấp nền tảng quản lý tài chính cá nhân, cho phép người dùng đăng ký, đăng nhập, thêm, xem, sửa và xóa các giao dịch thu chi. Ứng dụng tổng hợp dữ liệu để hiển thị tổng thu nhập, tổng chi tiêu, số dư và biểu đồ chi tiêu theo danh mục. Ngoài ra, hệ thống sử dụng AWS Lambda để thực hiện thống kê chi tiêu tự động theo lịch được cấu hình bằng Amazon EventBridge, đồng thời ghi lại nhật ký hoạt động trên Amazon CloudWatch.
* **Đối tượng sử dụng (Target Users):** Cá nhân, sinh viên và người đi làm có nhu cầu theo dõi thu nhập, quản lý chi tiêu và lập kế hoạch tài chính cá nhân.
* **Vấn đề giải quyết (Problem Solved):** Giảm sự phụ thuộc vào ghi chép thủ công, hỗ trợ tổng hợp dữ liệu tài chính nhanh chóng, cung cấp giao diện trực quan để theo dõi tình hình thu chi và triển khai ứng dụng trên môi trường đám mây có khả năng truy cập qua Internet.

### 2.2. Mục tiêu cụ thể (Specific Objectives)

* **Output mong muốn:**
  * Xây dựng hệ thống đăng ký và đăng nhập người dùng sử dụng JWT để xác thực và bcrypt để băm mật khẩu.
  * Phát triển backend bằng Node.js và Express.js để cung cấp API quản lý giao dịch thu chi.
  * Xây dựng giao diện web bằng HTML, CSS và JavaScript, kết hợp Chart.js để hiển thị dữ liệu tài chính trực quan.
  * Sử dụng MongoDB Atlas để lưu trữ thông tin người dùng và giao dịch.
  * Triển khai ứng dụng backend và frontend trên Amazon EC2 chạy Ubuntu, sử dụng PM2 để quản lý tiến trình Node.js.
  * Xây dựng hàm AWS Lambda thực hiện thống kê dữ liệu chi tiêu và sử dụng Amazon EventBridge Scheduler để kích hoạt tác vụ định kỳ.
  * Sử dụng Amazon CloudWatch Logs để theo dõi nhật ký thực thi Lambda và hỗ trợ kiểm tra lỗi.

* **Tiêu chí đánh giá thành công (Success Criteria):**
  * Người dùng có thể đăng nhập và thực hiện các thao tác quản lý giao dịch theo chức năng đã xây dựng.
  * Dữ liệu giao dịch được lưu trữ trên MongoDB Atlas và được truy xuất theo tài khoản người dùng đã xác thực.
  * Dashboard hiển thị được tổng thu nhập, tổng chi tiêu, số dư và biểu đồ phân tích chi tiêu.
  * Ứng dụng có thể truy cập thông qua địa chỉ công khai của máy chủ EC2 khi máy chủ và cấu hình mạng hoạt động bình thường.
  * Hàm Lambda thực thi thành công tác vụ thống kê và ghi nhận kết quả xử lý.
  * Nhật ký thực thi được ghi lại trên CloudWatch để phục vụ việc theo dõi và xử lý sự cố.

## 3. Kiến trúc và Thiết kế Kỹ thuật (Architecture & Technical Design)

### Sơ đồ kiến trúc (Architecture Diagram)

![Hình 1 – Kiến trúc hệ thống quản lý chi tiêu](/WorkshopAWS/images/4-Workshop/4.2/Exspense_Tracker_Architecture_Diagram.drawio.png)
*Hình 1 – Kiến trúc hệ thống quản lý chi tiêu
### 3.1. Các dịch vụ AWS và công nghệ sử dụng (AWS Services & Technology Selection)

* **Amazon EC2:** Cung cấp máy chủ ảo chạy Ubuntu để triển khai ứng dụng Expense Tracker. Backend Node.js/Express.js và các tệp frontend được phục vụ từ máy chủ này.
* **Amazon VPC:** Cung cấp môi trường mạng riêng cho các tài nguyên AWS. EC2 được đặt trong subnet phù hợp để có thể giao tiếp qua Internet theo cấu hình mạng.
* **Public Subnet:** Chứa máy chủ EC2 có cấu hình địa chỉ IP công khai, cho phép người dùng truy cập ứng dụng theo các quy tắc định tuyến và bảo mật đã thiết lập.
* **Internet Gateway:** Cho phép VPC giao tiếp với Internet khi kết hợp với route table và cấu hình mạng phù hợp.
* **Route Table:** Xác định đường đi của lưu lượng mạng, bao gồm tuyến mặc định ra Internet thông qua Internet Gateway.
* **Security Group:** Kiểm soát lưu lượng vào và ra của EC2. Các cổng được mở theo nhu cầu triển khai, chẳng hạn SSH để quản trị máy chủ và cổng ứng dụng để truy cập web.
* **Node.js và Express.js:** Xây dựng backend, xử lý yêu cầu HTTP, xác thực người dùng và cung cấp API cho các chức năng quản lý chi tiêu.
* **PM2:** Quản lý tiến trình Node.js trên EC2, hỗ trợ theo dõi trạng thái, xem nhật ký và khởi động lại ứng dụng khi cần thiết.
* **MongoDB Atlas:** Cơ sở dữ liệu đám mây lưu trữ thông tin tài khoản, giao dịch và dữ liệu thống kê của ứng dụng. MongoDB Atlas là dịch vụ cơ sở dữ liệu bên ngoài AWS.
* **AWS Lambda:** Thực thi tác vụ thống kê chi tiêu mà không cần duy trì một máy chủ riêng cho tác vụ này.
* **Amazon EventBridge Scheduler:** Kích hoạt hàm Lambda theo lịch định kỳ đã cấu hình, giúp tự động hóa quá trình thống kê.
* **Amazon CloudWatch:** Thu thập nhật ký thực thi của Lambda, hỗ trợ theo dõi kết quả và phát hiện lỗi trong quá trình xử lý.
* **HTML, CSS, JavaScript và Chart.js:** Xây dựng giao diện người dùng và biểu đồ tổng hợp dữ liệu thu chi.

### 3.2. Bảo mật và Quản lý quyền truy cập (Security & Access Management)

* **Xác thực người dùng:** Sử dụng JWT để xác thực các yêu cầu API và bcrypt để băm mật khẩu trước khi lưu trữ.
* **Bảo vệ dữ liệu giao dịch:** Backend xác định người dùng từ thông tin xác thực và giới hạn truy vấn giao dịch theo tài khoản tương ứng.
* **Quản lý quyền AWS:** Sử dụng IAM Role và chính sách quyền phù hợp khi cần cấp quyền cho các dịch vụ AWS, tuân thủ nguyên tắc Least Privilege.
* **Bảo mật mạng EC2:** Cấu hình Security Group chỉ cho phép các cổng cần thiết. Nên giới hạn quyền SSH theo địa chỉ IP quản trị và không mở rộng quyền truy cập không cần thiết.
* **Bảo vệ thông tin kết nối:** Lưu thông tin kết nối MongoDB Atlas và các biến cấu hình nhạy cảm trong môi trường cấu hình phù hợp, không đưa mật khẩu hoặc JWT Secret vào mã nguồn công khai.
* **Giám sát hệ thống:** Sử dụng CloudWatch Logs để theo dõi hoạt động của Lambda và hỗ trợ kiểm tra lỗi. Nhật ký không nên chứa mật khẩu, token hoặc thông tin nhạy cảm của người dùng.

## 4. Rủi ro Tiềm ẩn và Hướng giải quyết (Potential Risks & Mitigation)

* **Rủi ro 1: Máy chủ EC2 không hoạt động hoặc ứng dụng bị dừng**
  * *Hướng giải quyết:* Sử dụng PM2 để quản lý tiến trình Node.js, kiểm tra trạng thái ứng dụng và nhật ký lỗi. Cấu hình PM2 khởi động cùng hệ thống để hỗ trợ phục hồi sau khi EC2 khởi động lại.

* **Rủi ro 2: Không thể kết nối đến MongoDB Atlas**
  * *Hướng giải quyết:* Kiểm tra chuỗi kết nối trong biến môi trường, thông tin xác thực database, cấu hình Network Access của Atlas và khả năng kết nối mạng từ EC2. Chỉ cho phép các địa chỉ IP cần thiết truy cập cơ sở dữ liệu.

* **Rủi ro 3: Người dùng truy cập hoặc sửa dữ liệu của tài khoản khác**
  * *Hướng giải quyết:* Xác minh JWT ở backend và sử dụng định danh người dùng đã xác thực trong các truy vấn dữ liệu. Không tin tưởng `userId` do client tự gửi nếu chưa được kiểm tra.

* **Rủi ro 4: Hàm Lambda thực thi thất bại hoặc thống kê sai**
  * *Hướng giải quyết:* Kiểm tra logic thống kê, quyền truy cập MongoDB Atlas, biến môi trường và nhật ký trên CloudWatch. Kiểm thử hàm với các trường hợp có dữ liệu, không có dữ liệu và xảy ra lỗi kết nối.

* **Rủi ro 5: Tác vụ thống kê chạy nhiều lần hoặc ghi dữ liệu trùng lặp**
  * *Hướng giải quyết:* Thiết kế thao tác ghi thống kê có khả năng xử lý việc chạy lặp lại an toàn, xác định rõ kỳ thống kê và sử dụng khóa định danh phù hợp để tránh tạo bản ghi trùng.

* **Rủi ro 6: Truy cập ứng dụng qua HTTP hoặc cấu hình cổng chưa an toàn**
  * *Hướng giải quyết:* Cấu hình Security Group theo nguyên tắc tối thiểu. Khi triển khai cho người dùng thực tế, cân nhắc thiết lập HTTPS và hạn chế truy cập trực tiếp đến cổng backend.

## 5. Kế hoạch Triển khai Lab (Implementation Lab Steps)

Dự án được triển khai theo các bước:

* **Bước 1:** Chuẩn bị môi trường phát triển, cài đặt Node.js, npm và các công cụ cần thiết.
* **Bước 2:** Xây dựng backend bằng Node.js và Express.js, cấu hình kết nối MongoDB Atlas.
* **Bước 3:** Xây dựng chức năng đăng ký, đăng nhập, xác thực JWT và băm mật khẩu bằng bcrypt.
* **Bước 4:** Phát triển API quản lý giao dịch thu chi, bao gồm thêm, xem, sửa, xóa và tổng hợp dữ liệu thống kê.
* **Bước 5:** Xây dựng giao diện frontend bằng HTML, CSS và JavaScript; sử dụng Chart.js để trực quan hóa dữ liệu tài chính.
* **Bước 6:** Kiểm thử các API và chức năng chính tại môi trường local trước khi triển khai lên AWS.
* **Bước 7:** Tạo và cấu hình VPC, public subnet, Internet Gateway, route table và Security Group cho máy chủ EC2.
* **Bước 8:** Khởi tạo EC2 chạy Ubuntu, cài đặt Node.js và các thư viện cần thiết, triển khai ứng dụng và sử dụng PM2 để quản lý backend.
* **Bước 9:** Kiểm tra kết nối từ EC2 đến MongoDB Atlas và xác minh các chức năng đăng nhập, quản lý giao dịch và dashboard trên môi trường AWS.
* **Bước 10:** Xây dựng hàm AWS Lambda thực hiện thống kê dữ liệu chi tiêu và kiểm thử kết quả thực thi.
* **Bước 11:** Cấu hình Amazon EventBridge Scheduler để kích hoạt Lambda theo lịch định kỳ.
* **Bước 12:** Sử dụng Amazon CloudWatch Logs để kiểm tra nhật ký, xác minh kết quả xử lý và hỗ trợ khắc phục lỗi.
* **Bước 13:** Kiểm thử toàn bộ hệ thống, đánh giá kết quả triển khai và dọn dẹp các tài nguyên AWS không còn sử dụng.

## 6. Đóng góp Cá nhân và Kết quả đạt được (Personal Contributions & Results)

* **Xây dựng ứng dụng quản lý chi tiêu:** Phát triển các chức năng xác thực người dùng, quản lý giao dịch và hiển thị dashboard tổng hợp thu chi.
* **Triển khai ứng dụng trên AWS:** Đưa ứng dụng lên EC2 chạy Ubuntu, cấu hình mạng và sử dụng PM2 để quản lý tiến trình backend.
* **Tích hợp cơ sở dữ liệu đám mây:** Kết nối ứng dụng với MongoDB Atlas để lưu trữ và truy xuất dữ liệu người dùng, giao dịch.
* **Tự động hóa thống kê:** Xây dựng hàm Lambda để xử lý dữ liệu chi tiêu và kết hợp EventBridge Scheduler để kích hoạt theo lịch.
* **Theo dõi quá trình thực thi:** Sử dụng CloudWatch Logs để kiểm tra hoạt động của Lambda, ghi nhận kết quả và hỗ trợ phát hiện lỗi.
* **Nâng cao kiến thức AWS:** Thực hành các khái niệm về EC2, VPC, subnet, Internet Gateway, route table, Security Group, IAM, Lambda, EventBridge và CloudWatch thông qua một dự án ứng dụng thực tế.
