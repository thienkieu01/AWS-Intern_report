---
title: "Hình Minh Họa"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 8. </b> "
---


# Hình minh họa hệ thống

## 1. Use Case Diagram

Use Case Diagram mô tả các tác nhân (Actors) và các chức năng chính của hệ thống Quản lý thư viện. Sơ đồ giúp thể hiện mối quan hệ giữa người dùng và các chức năng mà hệ thống cung cấp.

![Use Case Diagram](/images/8-Figures/use_case_diagram.jpg)

> **Hình 1.** Use Case Diagram của hệ thống Library Management System.


## 2. Entity Relationship Diagram (ERD)

Entity Relationship Diagram (ERD) mô tả cấu trúc cơ sở dữ liệu của hệ thống, bao gồm các bảng dữ liệu và mối quan hệ giữa chúng. Đây là cơ sở để triển khai cơ sở dữ liệu PostgreSQL.

![Entity Relationship Diagram](/images/8-Figures/ERD_diagram.jpg)

> **Hình 2.** Entity Relationship Diagram (ERD) của hệ thống.


## 3. Giao diện đăng ký

Giao diện đăng ký cho phép người dùng tạo tài khoản mới trước khi sử dụng hệ thống. Người dùng cần nhập đầy đủ các thông tin cần thiết để hoàn tất quá trình đăng ký.

![Sign In Page](/images/8-Figures/signin.png)

> **Hình 3.** Giao diện đăng ký tài khoản.


## 4. Giao diện đăng nhập

Giao diện đăng nhập cho phép người dùng xác thực tài khoản trước khi truy cập vào hệ thống Quản lý thư viện. Sau khi đăng nhập thành công, người dùng sẽ được chuyển đến trang chức năng tương ứng với quyền được cấp.

![Login Page](/images/8-Figures/login.png)

> **Hình 4.** Giao diện đăng nhập hệ thống.


## 5. Giao diện menu chính

Giao diện menu chính cung cấp quyền truy cập nhanh đến các chức năng chính của hệ thống Quản lý thư viện, giúp người dùng dễ dàng điều hướng và sử dụng các chức năng theo quyền hạn của mình.

![Main Menu](/images/8-Figures/main_menu.png)

> **Hình 5.** Giao diện menu chính.


## 6. Trang Dashboard của Thủ thư

Trang Dashboard hiển thị tổng quan các thông tin quan trọng như số lượng sách, độc giả, phiếu mượn và các thống kê cần thiết, giúp thủ thư dễ dàng theo dõi tình trạng hoạt động của thư viện.

![Dashboard](/images/8-Figures/dashboard_librarian.png)

> **Hình 6.** Giao diện Dashboard của Thủ thư.


## 7. Quản lý thông tin sách

Chức năng quản lý thông tin sách cho phép thủ thư xem và quản lý chi tiết các đầu sách, bao gồm tên sách, tác giả, nhà xuất bản, thể loại, số lượng và hình ảnh bìa sách.

![Book Information](/images/8-Figures/thong_tin_sach.png)

> **Hình 7.** Giao diện quản lý thông tin sách.


## 8. Cập nhật thông tin sách

Giao diện này cho phép người dùng chỉnh sửa và cập nhật thông tin của sách, bao gồm các thông tin chi tiết, thể loại, nhà xuất bản và hình ảnh bìa sách.

![Edit Book Information](/images/8-Figures/thay_doi_thong_tin_sach.png)

> **Hình 8.** Giao diện cập nhật thông tin sách.


## 9. Quản lý mượn – trả sách

Chức năng quản lý mượn – trả sách cho phép thủ thư lập phiếu mượn, xử lý trả sách, cập nhật trạng thái mượn và quản lý các giao dịch mượn – trả một cách hiệu quả.

![Borrow Return Management](/images/8-Figures/quan_ly_muon_tra.png)

> **Hình 9.** Giao diện quản lý mượn – trả sách.


## 10. Lịch sử mượn sách

Trang lịch sử mượn hiển thị toàn bộ các giao dịch mượn sách của độc giả, giúp dễ dàng tra cứu lịch sử và theo dõi quá trình mượn sách.

![Borrowing History](/images/8-Figures/lich_su_muon.png)

> **Hình 10.** Giao diện lịch sử mượn sách.


## 11. Quản lý tài khoản người dùng

Chức năng quản lý tài khoản cho phép quản trị viên tạo mới, cập nhật, quản lý và phân quyền các tài khoản người dùng trong hệ thống.

![User Account Management](/images/8-Figures/quan_ly_acc.png)

> **Hình 11.** Giao diện quản lý tài khoản người dùng.


## 12. Quản lý tiền phạt

Chức năng quản lý tiền phạt giúp thủ thư theo dõi, cập nhật mức tiền phạt quá hạn và quản lý trạng thái thanh toán của độc giả.

![Fine Management](/images/8-Figures/quan_ly_tien_phat.png)

> **Hình 12.** Giao diện quản lý tiền phạt.