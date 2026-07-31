---
title : "Giám sát ứng dụng với CloudWatch"
date : 2024-01-01
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

#### Tổng quan

+ Sau khi ứng dụng đã chạy ổn định trên EC2, việc tiếp theo là **giám sát** để biết hệ thống đang hoạt động ra sao — CPU, RAM có quá tải không, ứng dụng có log lỗi gì không — thay vì phải SSH vào kiểm tra thủ công mỗi lần.

+ **Amazon CloudWatch** cho phép thu thập cả hai loại dữ liệu:
    + **Metrics**: các chỉ số hệ thống như CPU, memory, disk.
    + **Logs**: log ứng dụng (ví dụ log của container Docker), giúp tra cứu lỗi mà không cần đăng nhập vào EC2.

+ Để EC2 gửi được dữ liệu lên CloudWatch, cần 2 việc:
    + **IAM Role**: cấp quyền cho EC2 được phép gọi CloudWatch API để gửi log/metrics.
    + **CloudWatch Agent**: phần mềm cài trên EC2, chạy nền và thực hiện việc thu thập, gửi dữ liệu lên CloudWatch theo cấu hình đã định.

#### Nội dung

1. [Tạo IAM Role cho CloudWatch](5.7.1-create-IAM-role-for-EC2/)
2. [Cài đặt CloudWatch Agent](5.7.2-Install-CLoudWatch-agent/)