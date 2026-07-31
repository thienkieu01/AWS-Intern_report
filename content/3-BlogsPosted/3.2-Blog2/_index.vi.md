---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---
# AMAZON DYNAMODB – DỊCH VỤ CƠ SỞ DỮ LIỆU NOSQL CỦA AWS DÀNH CHO ỨNG DỤNG HIỆN ĐẠI

Amazon DynamoDB là dịch vụ cơ sở dữ liệu **NoSQL** được quản lý hoàn toàn (Fully Managed) trên nền tảng AWS, được thiết kế để đáp ứng các ứng dụng hiện đại yêu cầu hiệu năng cao, khả năng mở rộng linh hoạt và độ trễ thấp. Thay vì quản lý máy chủ hay hạ tầng cơ sở dữ liệu, người dùng chỉ cần tập trung vào việc thiết kế dữ liệu và phát triển ứng dụng, trong khi AWS đảm nhiệm toàn bộ việc vận hành, bảo trì và mở rộng hệ thống.

Các điểm chính cần nắm:

* Amazon DynamoDB là dịch vụ cơ sở dữ liệu **NoSQL Fully Managed**, giúp người dùng không cần quản lý máy chủ hay hạ tầng cơ sở dữ liệu.
* Hỗ trợ hiệu năng cao với **Single-digit Millisecond Latency**, duy trì tốc độ phản hồi ổn định ngay cả khi hệ thống có hàng triệu người dùng.
* Tự động mở rộng (Auto Scaling) theo lưu lượng truy cập mà không cần cấu hình hay nâng cấp hạ tầng thủ công.
* Áp dụng mô hình **Pay-as-you-go**, chỉ thanh toán theo dung lượng lưu trữ và số lượng request thực tế, phù hợp cho cả học tập và triển khai thực tế.
* Khuyến khích thiết kế dữ liệu dựa trên **Access Pattern**, tối ưu cho cách ứng dụng truy vấn dữ liệu thay vì sử dụng nhiều bảng và phép JOIN như cơ sở dữ liệu quan hệ.
* Dễ dàng tích hợp với các dịch vụ AWS khác như **IAM**, **Amazon CloudWatch**, **AWS Backup**, **AWS Lambda** và nhiều dịch vụ Serverless khác.
* Phù hợp để xây dựng các ứng dụng Web, Mobile, IoT, Gaming và Serverless yêu cầu khả năng mở rộng cao và độ sẵn sàng lớn.

DynamoDB đặc biệt phù hợp với các hệ thống có lưu lượng truy cập lớn, yêu cầu khả năng mở rộng tự động và độ trễ thấp, đồng thời giúp giảm đáng kể chi phí quản trị cơ sở dữ liệu so với các hệ quản trị truyền thống.




## Hướng dẫn thực hiện

### Bước 1: Tạo bảng (Table)

- Đăng nhập AWS Management Console.
- Truy cập dịch vụ **Amazon DynamoDB**.
- Chọn **Create Table**.
- Cấu hình:
  - Table Name.
  - Partition Key.
  - Sort Key (nếu cần).

### Bước 2: Cấu hình bảng

- Chọn chế độ Capacity phù hợp (On-demand hoặc Provisioned).
- Thiết lập Auto Scaling (nếu sử dụng Provisioned).
- Hoàn tất quá trình tạo Table.

### Bước 3: Thao tác với dữ liệu

- Thêm dữ liệu (Create Item).
- Truy vấn dữ liệu (Query).
- Cập nhật dữ liệu (Update Item).
- Xóa dữ liệu (Delete Item).

### Bước 4: Theo dõi và quản lý

- Theo dõi hiệu năng bằng **Amazon CloudWatch**.
- Phân quyền truy cập thông qua **AWS IAM**.
- Thiết lập Backup để bảo vệ dữ liệu khi cần thiết.

### Kết quả đạt được

- Hiểu được mô hình hoạt động của cơ sở dữ liệu NoSQL trên AWS.
- Biết cách tạo và quản lý bảng trong Amazon DynamoDB.
- Nắm được tư duy thiết kế dữ liệu theo Access Pattern thay vì sử dụng JOIN như cơ sở dữ liệu quan hệ.
- Hiểu được khả năng mở rộng tự động và hiệu năng cao của DynamoDB trong các ứng dụng hiện đại.

## Nguồn tham khảo

![AWS Backup & Restore](/images/3-Blogs/blog3.jpg)

- Workshop: https://000060.awsstudygroup.com/
