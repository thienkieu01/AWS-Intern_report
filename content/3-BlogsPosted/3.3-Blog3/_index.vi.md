---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# AWS KMS – SAU KHI TÌM HIỂU, MÌNH HIỂU GÌ VỀ DỊCH VỤ QUẢN LÝ KHÓA MÃ HÓA CỦA AWS?

AWS Key Management Service (AWS KMS) là dịch vụ quản lý khóa mã hóa trên nền tảng AWS, giúp tạo, lưu trữ và kiểm soát việc sử dụng các khóa mã hóa một cách an toàn. Kết hợp với các dịch vụ như Amazon S3, Amazon EBS, Amazon RDS và DynamoDB, AWS KMS giúp bảo vệ dữ liệu lưu trữ (Encryption at Rest) đồng thời hỗ trợ quản lý quyền truy cập và theo dõi lịch sử sử dụng khóa thông qua AWS CloudTrail.

Các điểm chính cần nắm:

* AWS KMS là dịch vụ **Fully Managed** giúp tạo, lưu trữ và quản lý các khóa mã hóa (Encryption Keys) trên AWS.
* Hỗ trợ mã hóa dữ liệu lưu trữ (**Encryption at Rest**) cho nhiều dịch vụ như **Amazon S3, Amazon EBS, Amazon RDS** và **Amazon DynamoDB**.
* Phân biệt giữa **Encryption in Transit** (mã hóa khi truyền dữ liệu) và **Encryption at Rest** (mã hóa khi lưu trữ dữ liệu).
* Sử dụng mô hình **Customer Master Key (CMK)** kết hợp với **Data Key** để mã hóa dữ liệu có kích thước lớn một cách an toàn và hiệu quả.
* Các khóa mã hóa được bảo vệ bên trong **Hardware Security Module (HSM)** và không thể tải trực tiếp ra ngoài.
* Tích hợp với **AWS CloudTrail** để ghi lại toàn bộ lịch sử sử dụng khóa, hỗ trợ kiểm tra và truy vết hoạt động.
* Quyền truy cập dữ liệu trên Amazon S3 và quyền sử dụng khóa KMS là hai quyền độc lập; người dùng cần được cấp quyền sử dụng khóa mới có thể giải mã dữ liệu.

AWS KMS đặc biệt phù hợp với các hệ thống yêu cầu mức độ bảo mật cao, giúp doanh nghiệp quản lý tập trung các khóa mã hóa, kiểm soát quyền truy cập và bảo vệ dữ liệu trên nhiều dịch vụ AWS.


## Hướng dẫn thực hiện

### Bước 1: Tạo khóa mã hóa trong AWS KMS

- Truy cập dịch vụ **AWS Key Management Service**.
- Chọn **Create Key**.
- Cấu hình:
  - Symmetric Key.
  - Encrypt and Decrypt.
  - Single Region.
- Đặt Alias và cấu hình **Key Administrator**, **Key Users**.

### Bước 2: Tạo Amazon S3 Bucket

- Tạo một S3 Bucket mới.
- Chọn **Default Encryption**.
- Chọn **Server-side encryption using AWS KMS (SSE-KMS)**.
- Chỉ định khóa KMS vừa tạo.

### Bước 3: Tải dữ liệu lên S3

- Upload một tệp bất kỳ lên Bucket.
- Kiểm tra phần **Properties** để xác nhận dữ liệu đã được mã hóa bằng khóa KMS.

### Bước 4: Kiểm tra quyền truy cập

- Tạo IAM User chỉ có quyền **Amazon S3 Full Access** và thử tải tệp về.
- Quan sát lỗi **Access Denied** do chưa được cấp quyền sử dụng khóa KMS.
- Thêm IAM User vào danh sách **Key Users** của khóa KMS.
- Kiểm tra lại và xác nhận người dùng đã có thể truy cập dữ liệu.

### Kết quả đạt được

- Hiểu được vai trò của AWS KMS trong việc quản lý khóa mã hóa trên AWS.
- Phân biệt được **Encryption in Transit** và **Encryption at Rest**.
- Nắm được cơ chế hoạt động của **CMK** và **Data Key** trong quá trình mã hóa dữ liệu.
- Biết cách cấu hình mã hóa Amazon S3 bằng **AWS KMS**.
- Hiểu được mối quan hệ giữa **IAM**, **Amazon S3** và **AWS KMS** trong việc kiểm soát quyền truy cập dữ liệu.
- Biết cách sử dụng **AWS CloudTrail** để theo dõi lịch sử sử dụng khóa mã hóa.

## Nguồn tham khảo

![AWS Backup & Restore](/images/3-Blogs/blog2.jpg)

- Workshop: https://000033.awsstudygroup.com/
- Video hướng dẫn: https://youtu.be/SCZpW-3b5G0?si=fM551VA4uu49_EWJ
- AWS Documentation: https://docs.aws.amazon.com/kms/