---
title : "Giới thiệu"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Giới thiệu về đề tài

+ Hệ thống quản lý thư viện (Library Management System) là ứng dụng web được xây dựng trên nền tảng **Django**, cho phép quản lý sách, người dùng (Administrator, Librarian, Reader), và các nghiệp vụ mượn/trả sách thông qua trình duyệt Web.
+ Ứng dụng được triển khai hoàn toàn trên hạ tầng **AWS**, tận dụng các dịch vụ điện toán đám mây để đảm bảo tính bảo mật, khả năng mở rộng và dễ dàng vận hành, thay vì triển khai trên máy chủ vật lý truyền thống.

#### Tổng quan về hệ thống

Trong đồ án này, hệ thống được xây dựng dựa trên các dịch vụ chính của AWS:

+ **Amazon VPC**: thiết lập hạ tầng mạng riêng biệt (`library-vpc`), gồm **Public Subnet** (chứa EC2 chạy ứng dụng) và **Private Subnet** (chứa RDS, cách ly khỏi Internet để đảm bảo an toàn dữ liệu).
+ **AWS IAM**: quản lý người dùng và phân quyền truy cập — bao gồm **IAM User** (`library-app-user`) cấp quyền cho ứng dụng ghi dữ liệu lên S3, và **IAM Role** gán cho EC2 để gửi log lên CloudWatch mà không cần lưu access key.
+ **Security Groups**: kiểm soát lưu lượng truy cập ở tầng mạng, giới hạn EC2 chỉ mở các cổng cần thiết (SSH, HTTP, 8000) và RDS chỉ nhận kết nối từ đúng Security Group của EC2.
+ **Amazon RDS (PostgreSQL)**: lưu trữ toàn bộ dữ liệu nghiệp vụ của hệ thống (sách, người dùng, lịch sử mượn trả), được đặt trong Private Subnet, không truy cập trực tiếp được từ Internet.
+ **Amazon S3**: lưu trữ hình ảnh bìa sách và các tệp tài liệu được người dùng tải lên.
+ **Amazon EC2**: chạy ứng dụng Django trong môi trường **Docker**, xử lý xác thực, quản lý sách và các nghiệp vụ của hệ thống.
+ **Amazon CloudWatch**: thu thập log, giám sát tài nguyên và trạng thái hoạt động của EC2 trong suốt quá trình vận hành.

Toàn bộ quá trình triển khai được thực hiện theo thứ tự: **VPC → IAM → Security Groups → RDS → S3 → EC2 → Deploy → CloudWatch**, đảm bảo hạ tầng mạng và bảo mật được thiết lập đầy đủ trước khi triển khai ứng dụng và cấu hình giám sát.

![overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.jpg)