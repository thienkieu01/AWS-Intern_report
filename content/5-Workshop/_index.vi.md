---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai hệ thống Quản lý Thư viện an toàn trên AWS

#### Tổng quan

Hệ thống **Quản lý Thư viện (Library Management System)** là ứng dụng web xây dựng trên nền tảng **Django**, được triển khai trên hạ tầng **AWS** nhằm đảm bảo tính bảo mật, khả năng mở rộng và dễ dàng vận hành.

Trong workshop này, chúng ta sẽ học cách xây dựng một hạ tầng AWS hoàn chỉnh cho ứng dụng web, từ việc thiết lập mạng riêng (VPC), cấu hình bảo mật (Security Groups, IAM), đến triển khai cơ sở dữ liệu, lưu trữ, ứng dụng và giám sát hệ thống.

Hệ thống sử dụng các dịch vụ AWS chính sau, mỗi dịch vụ đóng một vai trò riêng biệt trong kiến trúc:
+ **Amazon VPC** - Thiết lập hạ tầng mạng riêng, tách biệt Public Subnet (chứa ứng dụng) và Private Subnet (chứa cơ sở dữ liệu) để tăng tính bảo mật.
+ **Security Groups** - Kiểm soát lưu lượng truy cập ở tầng mạng, giới hạn EC2 chỉ mở các cổng cần thiết và RDS chỉ nhận kết nối từ đúng nguồn được phép.
+ **AWS IAM** - Quản lý người dùng và phân quyền truy cập, cho phép ứng dụng thao tác với S3 và EC2 gửi log lên CloudWatch mà không cần lưu key thủ công.
+ **Amazon RDS (PostgreSQL)** - Lưu trữ toàn bộ dữ liệu nghiệp vụ của hệ thống, đặt trong Private Subnet để không thể truy cập trực tiếp từ Internet.
+ **Amazon S3** - Lưu trữ hình ảnh bìa sách và tài liệu do người dùng tải lên.
+ **Amazon EC2** - Chạy ứng dụng Django trong môi trường Docker, xử lý toàn bộ nghiệp vụ của hệ thống.
+ **Amazon CloudWatch** - Thu thập log, giám sát tài nguyên và trạng thái hoạt động của hệ thống.

#### Nội dung

1. [Giới thiệu](5.1-Introduction/)
2. [Các bước chuẩn bị](5.2-Prerequisites/)
3. [Thiết lập mạng (VPC)](5.3-Network-setup/)
4. [Thiết lập bảo mật (Security Groups & IAM)](5.4-Security-setup/)
5. [Triển khai cơ sở dữ liệu và lưu trữ (RDS & S3)](5.5-Database-and-storage/)
6. [Triển khai ứng dụng trên EC2](5.6-Application-deployment/)
7. [Giám sát hệ thống (CloudWatch)](5.7-Monitoring/)
8. [Dọn dẹp tài nguyên](5.8-Cleanup/)