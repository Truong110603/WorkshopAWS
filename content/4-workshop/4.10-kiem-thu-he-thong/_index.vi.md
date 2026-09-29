---
title: "Kiểm thử hệ thống"
weight: 10
pre: " <b> 4.10 </b> "
---

## Mục tiêu

Đánh giá toàn diện hoạt động của dự án từ đầu cuối (End-to-End). Kiểm chứng khả năng hoạt động của các chức năng đăng ký, đăng nhập, quản lý giao dịch, thống kê dữ liệu và đặc biệt là kiểm tra luồng tự động hóa sử dụng AWS Lambda và Amazon EventBridge.

Ngoài ra, kiểm tra khả năng phân tách dữ liệu giữa các tài khoản người dùng thông qua cơ chế xác thực JWT và `userId`.

## Tổng quan

Để đảm bảo mỗi người dùng chỉ có thể truy cập dữ liệu giao dịch của chính mình, dự án sử dụng cơ chế xác thực bằng JSON Web Token (JWT).

Khi người dùng đăng ký tài khoản, thông tin người dùng được lưu vào MongoDB Atlas và mật khẩu được mã hóa bằng bcrypt.

Sau khi đăng nhập thành công, Backend tạo một JWT chứa thông tin định danh của người dùng. Token được lưu tại LocalStorage trên trình duyệt và được gửi kèm trong Header của các request cần xác thực.

Khi người dùng thực hiện các thao tác với giao dịch, Backend kiểm tra JWT và sử dụng `userId` để truy vấn dữ liệu tương ứng trong MongoDB Atlas. Nhờ đó, các tài khoản khác nhau không thể truy cập trực tiếp vào dữ liệu giao dịch của nhau.

Bên cạnh đó, AWS Lambda được sử dụng để thực hiện thống kê dữ liệu chi tiêu theo từng người dùng. Amazon EventBridge Scheduler tự động kích hoạt Lambda theo lịch đã cấu hình và kết quả thống kê được lưu vào collection `statistics` trong MongoDB Atlas.

## Kết quả mong đợi

* Người dùng có thể đăng ký tài khoản mới thành công.
* Người dùng có thể đăng nhập và nhận được JWT hợp lệ.
* Người dùng đã đăng nhập có thể thêm, xem, sửa và xóa giao dịch.
* Dữ liệu giao dịch của các tài khoản khác nhau được phân tách thông qua `userId`.
* Người dùng chưa đăng nhập không thể truy cập các API quản lý giao dịch.
* Dashboard hiển thị chính xác tổng thu nhập, tổng chi tiêu và số dư.
* AWS Lambda thực hiện thống kê dữ liệu thành công.
* Kết quả thống kê của Lambda được lưu vào MongoDB Atlas.
* Amazon EventBridge có thể tự động kích hoạt Lambda theo lịch đã cấu hình.
* Nhật ký thực thi Lambda được ghi nhận trên Amazon CloudWatch.

---

## Các bước kiểm thử chi tiết

### Bước 1: Kiểm tra trạng thái Backend

1. Truy cập máy chủ Amazon EC2 bằng SSH.

```bash
ssh -i "expense-tracker.pem" ubuntu@<PUBLIC-IP>
