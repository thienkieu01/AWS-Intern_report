---
title : "Triển khai ứng dụng trên EC2"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### Tổng quan

+ Trong phần này, bạn sẽ triển khai ứng dụng Django lên **Amazon EC2** — nơi thực sự xử lý xác thực, quản lý sách và các nghiệp vụ của hệ thống. EC2 được đặt trong Public Subnet đã thiết lập ở mục 5.3, kết nối tới RDS và S3 thông qua Security Group và IAM đã cấu hình ở các mục trước.

+ Ứng dụng được đóng gói và chạy bằng **Docker**, giúp môi trường chạy nhất quán, dễ triển khai và không phụ thuộc vào việc cài đặt thủ công từng gói phần mềm trên EC2.

+ Vì sao cần gán **Elastic IP** cho EC2:
    + Mặc định, địa chỉ IP công khai của EC2 sẽ **thay đổi** mỗi khi instance bị stop/start. Elastic IP là địa chỉ IP tĩnh, giữ nguyên dù instance khởi động lại — tránh phải sửa lại cấu hình (`ALLOWED_HOSTS`, DNS...) mỗi lần.

#### Nội dung

1. [Launch EC2 và gán Elastic IP](5.6.1-Launch-EC2-and-attach-Elastic-IP/)
2. [Cài Docker, Clone code](5.6.2-Install-Docker-clone-code/)
3. [Build và chạy ứng dụng](5.6.3-Build-and-run-the-application/)