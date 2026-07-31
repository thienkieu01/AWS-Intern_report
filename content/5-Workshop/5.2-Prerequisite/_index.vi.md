---
title : "Các bước chuẩn bị"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Tài khoản và region

Trong đồ án này, chúng ta sẽ triển khai trên region **N. Virginia (us-east-1)**.

Đảm bảo tài khoản AWS đang dùng có quyền truy cập đầy đủ tới các dịch vụ: VPC, EC2, RDS, S3, IAM, Security Groups, CloudWatch.

#### Công cụ cần chuẩn bị

+ **VS Code** kèm extension **Remote - SSH** — dùng để kết nối và code trực tiếp trên EC2 sau khi triển khai.
+ **Source code** ứng dụng Django (`library-management`) đã đẩy lên Git repository, dùng để clone về EC2 ở bước deploy.
+ **Docker & Docker Compose** — không cần cài trên máy cá nhân, sẽ được cài trực tiếp trên EC2 ở bước sau.

#### Thứ tự triển khai

Khác với các workshop dùng CloudFormation để dựng sẵn hạ tầng chỉ trong một lần deploy, đồ án này được triển khai **thủ công từng bước qua AWS Console**, nhằm hiểu rõ vai trò của từng dịch vụ trong kiến trúc:

**VPC → Security Groups → IAM (User) → RDS → S3 → EC2 → Deploy (Docker) → IAM (Role) & CloudWatch**

Cụ thể các bước đã thực hiện:

1. Tạo **VPC** riêng (`library-vpc`, CIDR `10.0.0.0/16`), gồm Public Subnet và 2 Private Subnet (đặt ở 2 Availability Zone khác nhau để đáp ứng yêu cầu của RDS DB Subnet Group), kèm Internet Gateway và Route Table tương ứng cho từng loại subnet.
2. Tạo 2 **Security Group**: `library-ec2-sg` (mở SSH/HTTP/8000) và `library-rds-sg` (chỉ nhận kết nối PostgreSQL từ `library-ec2-sg`).
3. Tạo **IAM User** (`library-app-user`) cấp quyền `AmazonS3FullAccess`, dùng Access Key để ứng dụng Django ghi dữ liệu lên S3.
4. Tạo **RDS PostgreSQL** đặt trong Private Subnet, không public access, gắn Security Group `library-rds-sg`.
5. Tạo **S3 Bucket** lưu ảnh bìa sách, cấu hình Bucket Policy cho phép đọc công khai.
6. Tạo **Elastic IP** và gán vào **EC2** (đặt tại Public Subnet, gắn `library-ec2-sg`) để có địa chỉ IP cố định.
7. SSH vào EC2, cài **Docker & Docker Compose**, clone code, cấu hình file `.env` (kết nối RDS + S3), build và chạy ứng dụng.
8. Tạo **IAM Role** (`library-ec2-cloudwatch-role`) gắn policy `CloudWatchAgentServerPolicy`, gán vào EC2, cài đặt **CloudWatch Agent** để thu thập log và giám sát tài nguyên.

