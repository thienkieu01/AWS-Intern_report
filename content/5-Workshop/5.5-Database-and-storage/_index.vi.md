---
title : "Cơ sở dữ liệu và lưu trữ"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### Tổng quan

+ Trong phần này, bạn sẽ triển khai 2 dịch vụ cốt lõi cho việc lưu trữ dữ liệu của hệ thống: **Amazon RDS (PostgreSQL)** để lưu dữ liệu nghiệp vụ (sách, người dùng, lịch sử mượn trả), và **Amazon S3** để lưu file tĩnh (ảnh bìa sách, tài liệu do người dùng tải lên).

+ Vì sao tách riêng 2 loại lưu trữ:
    + **RDS** phù hợp cho dữ liệu có cấu trúc, cần truy vấn quan hệ (query, join, transaction) — ví dụ thông tin sách, tài khoản, trạng thái mượn/trả.
    + **S3** phù hợp cho dữ liệu dạng file (object storage) — ảnh bìa sách không cần truy vấn quan hệ, chỉ cần lưu bền vững và truy cập qua URL, tách biệt khỏi vòng đời của EC2/RDS.

+ Cả 2 dịch vụ đều được đặt trong đúng vùng bảo mật đã thiết lập ở mục trước: RDS nằm trong **Private Subnet** (không public access, chỉ nhận kết nối từ `library-ec2-sg`), còn S3 là dịch vụ ở tầng ngoài VPC, được ứng dụng truy cập qua Access Key của `library-app-user`.

#### Nội dung

1. [Tạo RDS PostgreSQL](5.5.1-create-RDS-PostgreSQL/)
2. [Tạo S3 Bucket](5.5.2-create-S3-bucket/)