---
title : "Thiết lập hệ thống mạng (VPC)"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Tổng quan

Trong phần này, bạn sẽ xây dựng nền tảng hạ tầng mạng (networking) cho hệ thống quản lý thư viện trên AWS bằng cách tạo một **VPC (Virtual Private Cloud)** riêng biệt. VPC đóng vai trò như một mạng ảo cô lập, giúp bạn kiểm soát toàn bộ môi trường mạng của ứng dụng: dải địa chỉ IP, subnet công khai/riêng tư, cách các tài nguyên giao tiếp với nhau và với Internet.

Việc thiết kế VPC hợp lý là bước nền tảng quan trọng, ảnh hưởng trực tiếp đến tính bảo mật, khả năng mở rộng và hiệu năng của toàn bộ hệ thống sau này (EC2, RDS, S3...).

Trong phần này, bạn sẽ lần lượt thực hiện:

- Tạo VPC cùng các subnet công khai (public) và riêng tư (private)
- Tạo Internet Gateway để kết nối VPC với Internet
- Cấu hình route table để định tuyến lưu lượng mạng phù hợp cho từng loại subnet

#### Nội dung

- [Tạo VPC và các subnet](5.3.1-create-vpc-and-subnets/)
- [Tạo Internet Gateway](5.3.2-create-internet-gateway/)
- [Cấu hình route table](5.3.3-configure-route-tables/)