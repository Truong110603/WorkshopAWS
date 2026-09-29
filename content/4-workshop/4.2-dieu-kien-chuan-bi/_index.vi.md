# Điều kiện chuẩn bị

### Mục tiêu

Đảm bảo người đọc có thể truy cập AWS Management Console, chuẩn bị đầy đủ các công cụ phát triển cần thiết và tải mã nguồn dự án trước khi bắt đầu triển khai hệ thống Expense Tracker.

---

## 1. Công cụ cần chuẩn bị

Workshop này sử dụng **AWS Management Console (Web UI)** để tạo và quản lý các tài nguyên AWS. Không yêu cầu sử dụng AWS CLI hoặc các công cụ Infrastructure as Code (IaC).

Chuẩn bị các phần mềm sau:

- **Node.js (v18+)**: Dùng để chạy Backend Node.js/Express và phát triển ứng dụng.
- **Git**: Quản lý và tải mã nguồn dự án.
- **Visual Studio Code (hoặc IDE khác)**: Dùng để chỉnh sửa mã nguồn.
- **MongoDB Atlas**: Cung cấp cơ sở dữ liệu MongoDB cho hệ thống.

---

## 2. Các bước thực hiện

**Đăng nhập AWS Console:** Đăng nhập vào AWS Management Console và đảm bảo Region được chọn là **ap-southeast-1 (Singapore)**.

**Checkpoint:** Xác nhận Region đang sử dụng là **ap-southeast-1** trước khi tạo tài nguyên.

**Kiểm tra công cụ cục bộ:** Đảm bảo các phần mềm đã được cài đặt thành công.

**Chuẩn bị tài khoản MongoDB Atlas:** Đăng nhập MongoDB Atlas và chuẩn bị MongoDB Cluster, Database User và Connection String để hệ thống Backend và AWS Lambda có thể kết nối đến cơ sở dữ liệu.

**Checkpoint:** MongoDB Cluster đã được tạo và có thông tin kết nối cần thiết.

**Chuẩn bị mã nguồn dự án:** Tải mã nguồn Expense Tracker từ GitHub và mở dự án bằng Visual Studio Code.

Mã nguồn bao gồm các thành phần chính:

```text
expense-tracker/
├── backend/
├── frontend/
└── lambda-statistics/
```
**Kiểm tra công cụ cục bộ:** Đảm bảo các phần mềm đã được cài đặt thành công.

```bash
node --version
npm --version
git --version
```

**Checkpoint:** Tất cả các lệnh đều trả về phiên bản hợp lệ.

**Tải mã nguồn dự án:** Clone mã nguồn từ GitHub và mở dự án bằng Visual Studio Code.

**Checkpoint:** Dự án được mở thành công và sẵn sàng cho quá trình triển khai.

---


## 3. Kết quả mong đợi
Đăng nhập thành công vào AWS Management Console.
* Xác định Region sử dụng cho Workshop.
* Chuẩn bị tài khoản và MongoDB Cluster trên MongoDB Atlas.
* Chuẩn bị đầy đủ môi trường phát triển.
* Tải thành công mã nguồn Expense Tracker.
* Chuẩn bị các thông tin cấu hình cần thiết.
* Hoàn thành các điều kiện chuẩn bị trước khi chuyển sang chương tiếp theo.
