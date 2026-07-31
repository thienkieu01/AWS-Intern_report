---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# Library Management System
## Giải pháp AWS Cloud cho hệ thống quản lý thư viện

### 1. Tóm tắt điều hành

Library Management System là hệ thống quản lý thư viện được xây dựng nhằm số hóa quy trình quản lý sách, độc giả và hoạt động mượn – trả sách. Hệ thống hỗ trợ ba nhóm người dùng chính gồm **Quản trị viên (Administrator), Thủ thư (Librarian)** và **Độc giả (Reader)**, giúp nâng cao hiệu quả quản lý, giảm thiểu các thao tác thủ công và tăng tính chính xác trong quá trình vận hành.

Giải pháp được phát triển bằng **Django**, sử dụng **PostgreSQL** làm hệ quản trị cơ sở dữ liệu và **Docker** để đóng gói ứng dụng. Hệ thống dự kiến triển khai trên nền tảng **AWS Cloud** với các dịch vụ như **Amazon EC2, Amazon RDS PostgreSQL, Amazon S3, Amazon CloudWatch và AWS IAM**, nhằm đảm bảo khả năng mở rộng, tính ổn định, bảo mật và thuận tiện trong quá trình triển khai cũng như vận hành.


### 2. Tuyên bố vấn đề

#### *Vấn đề hiện tại*

Các thư viện hiện nay vẫn chủ yếu quản lý thông tin sách và hoạt động mượn – trả bằng sổ sách hoặc các phần mềm cài đặt cục bộ. Điều này dẫn đến nhiều hạn chế:

- Khó quản lý số lượng lớn đầu sách và độc giả.
- Dữ liệu dễ bị thất lạc hoặc mất khi xảy ra sự cố.
- Khó mở rộng hệ thống khi số lượng người dùng tăng.
- Việc triển khai và bảo trì phụ thuộc nhiều vào từng môi trường cài đặt.
- Thiếu cơ chế giám sát và theo dõi tình trạng hoạt động của hệ thống.

#### *Giải pháp*

Hệ thống được triển khai trên nền tảng AWS Cloud theo mô hình Web Application.

Người dùng truy cập hệ thống thông qua trình duyệt Web. Ứng dụng **Django** được triển khai trên **Amazon EC2** và chạy trong môi trường **Docker** để xử lý toàn bộ nghiệp vụ quản lý thư viện. **Amazon RDS PostgreSQL** lưu trữ dữ liệu của hệ thống, trong khi **Amazon S3** lưu trữ hình ảnh bìa sách và các tệp đính kèm. **Amazon CloudWatch** được sử dụng để theo dõi hoạt động của hệ thống và **AWS IAM** quản lý quyền truy cập vào các tài nguyên AWS.

Hệ thống hỗ trợ các chức năng:

- Quản lý tài khoản người dùng.
- Quản lý sách và danh mục.
- Quản lý tác giả và nhà xuất bản.
- Quản lý độc giả.
- Quản lý mượn và trả sách.
- Thống kê và báo cáo.

#### *Lợi ích và hoàn vốn đầu tư (ROI)*

Giải pháp giúp giảm đáng kể thời gian quản lý thủ công, nâng cao độ chính xác của dữ liệu và cải thiện trải nghiệm sử dụng cho người quản trị cũng như thủ thư.

Việc triển khai trên AWS giúp hệ thống dễ dàng mở rộng khi nhu cầu sử dụng tăng lên mà không cần thay đổi kiến trúc. Docker giúp chuẩn hóa môi trường triển khai, giảm thời gian cấu hình và thuận tiện trong quá trình bảo trì. Hệ thống cũng tạo nền tảng để mở rộng thêm các tính năng mới trong tương lai.


### 3. Kiến trúc giải pháp

Hệ thống được triển khai theo kiến trúc Web Application nhiều tầng trên nền tảng AWS Cloud.

Người dùng truy cập hệ thống thông qua Internet. Các yêu cầu được chuyển tới máy chủ ứng dụng **Amazon EC2**, nơi chạy ứng dụng **Django** trong môi trường **Docker**. Dữ liệu được lưu trữ trên **Amazon RDS PostgreSQL**, trong khi hình ảnh sách và các tệp đính kèm được lưu trên **Amazon S3**. **Amazon CloudWatch** giám sát hoạt động của hệ thống và hỗ trợ theo dõi log cũng như hiệu năng của máy chủ.

![Library Management System AWS Architecture](/images/2-Proposal/library_management_aws_architecture.jpg)

### *Dịch vụ AWS sử dụng*

- **Amazon EC2:** Triển khai ứng dụng Django.
- **Amazon RDS (PostgreSQL):** Lưu trữ dữ liệu của hệ thống.
- **Amazon S3:** Lưu trữ hình ảnh bìa sách và tài liệu.
- **Amazon CloudWatch:** Theo dõi hiệu năng, log và cảnh báo.
- **AWS IAM:** Quản lý người dùng và phân quyền truy cập.
- **Amazon VPC:** Thiết lập hạ tầng mạng riêng cho hệ thống.
- **Security Groups:** Kiểm soát truy cập tới EC2 và RDS.

### *Thiết kế thành phần*

- **Người dùng:** Administrator, Librarian và Reader truy cập hệ thống thông qua trình duyệt Web.
- **Application Layer:** Amazon EC2 chạy ứng dụng Django trong môi trường Docker, thực hiện xác thực, quản lý sách, quản lý mượn trả và các nghiệp vụ của hệ thống.
- **Database Layer:** Amazon RDS PostgreSQL lưu trữ toàn bộ dữ liệu của hệ thống.
- **Storage Layer:** Amazon S3 lưu trữ hình ảnh sách và các tệp tải lên.
- **Monitoring Layer:** Amazon CloudWatch thu thập log, theo dõi tài nguyên và gửi cảnh báo khi hệ thống gặp sự cố.


### 4. Triển khai kỹ thuật

#### *Các giai đoạn triển khai*

1. **Phân tích yêu cầu và thiết kế hệ thống:** Xây dựng Use Case Diagram, ERD và kiến trúc AWS.
2. **Thiết kế hạ tầng AWS:** Triển khai VPC, EC2, RDS PostgreSQL, S3, IAM và Security Groups.
3. **Phát triển và triển khai ứng dụng:** Xây dựng Backend bằng Django, kết nối PostgreSQL, đóng gói ứng dụng bằng Docker và triển khai lên Amazon EC2.
4. **Kiểm thử và đưa vào vận hành:** Kiểm thử chức năng, hiệu năng, bảo mật và triển khai chính thức.

#### *Yêu cầu kỹ thuật*

- **Backend:** Django, Django REST Framework.
- **Database:** PostgreSQL trên Amazon RDS.
- **Container:** Docker, Docker Compose.
- **Storage:** Amazon S3.
- **Operating System:** Ubuntu Server.
- **Cloud Platform:** Amazon EC2, Amazon RDS, Amazon S3, Amazon CloudWatch.
- **Development Tools:** Git, GitHub, Visual Studio Code.


### 5. Lộ trình & Mốc triển khai

- **Giai đoạn chuẩn bị:** Phân tích yêu cầu và thiết kế cơ sở dữ liệu.
- **Giai đoạn phát triển:** Xây dựng chức năng và triển khai hạ tầng AWS.
- **Giai đoạn kiểm thử:** Kiểm thử chức năng và hiệu năng hệ thống.
- **Giai đoạn triển khai:** Đưa hệ thống vào vận hành và theo dõi bằng Amazon CloudWatch.


### 6. Ước tính ngân sách

#### *Chi phí hạ tầng*

- Amazon EC2 t3.micro.
- Amazon RDS PostgreSQL db.t3.micro.
- Amazon S3 Standard.
- Amazon CloudWatch.
- Data Transfer.

**Tổng chi phí ước tính:** khoảng **20–30 USD/tháng** (tùy theo lưu lượng truy cập và dung lượng dữ liệu).

Đối với môi trường học tập (AWS Academy Learner Lab hoặc AWS Free Tier), các dịch vụ này có thể được triển khai mà không phát sinh chi phí thực tế trong giới hạn của phòng lab.



### 7. Đánh giá rủi ro

#### *Ma trận rủi ro*

- Máy chủ EC2 gặp sự cố.
- Cơ sở dữ liệu quá tải.
- Mất dữ liệu do lỗi hệ thống.
- Truy cập trái phép.

#### *Chiến lược giảm thiểu*

- Sao lưu cơ sở dữ liệu PostgreSQL định kỳ.
- Phân quyền IAM theo nguyên tắc Least Privilege.
- Giám sát bằng Amazon CloudWatch.
- Sử dụng Security Groups để bảo vệ hệ thống.

#### *Kế hoạch dự phòng*

- Khôi phục dữ liệu từ bản sao lưu PostgreSQL.
- Triển khai lại ứng dụng bằng Docker Compose.
- Thay thế EC2 khi xảy ra sự cố nghiêm trọng.


### 8. Kết quả kỳ vọng

#### *Cải tiến kỹ thuật*

Hệ thống giúp tự động hóa quy trình quản lý thư viện, giảm thao tác thủ công và nâng cao hiệu quả quản lý. Kiến trúc AWS kết hợp Docker giúp hệ thống có khả năng mở rộng, dễ triển khai và thuận tiện trong quá trình bảo trì.

#### *Giá trị dài hạn*

Giải pháp tạo nền tảng triển khai ổn định cho hệ thống quản lý thư viện, đồng thời giúp áp dụng các kiến thức đã học trong chương trình **First Cloud AI Journey** vào thực tế. Trong tương lai, hệ thống có thể mở rộng với các tính năng như thông báo sách quá hạn, thống kê nâng cao, tìm kiếm thông minh hoặc tích hợp các công nghệ AI.