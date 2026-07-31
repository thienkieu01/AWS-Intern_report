---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# TỰ ĐỘNG HÓA QUẢN LÝ DỮ LIỆU: TRIỂN KHAI HỆ THỐNG BACKUP & RESTORE TOÀN DIỆN TRÊN AWS

Trong các hệ thống hiện đại, việc sao lưu dữ liệu (Backup) là chưa đủ nếu không thể đảm bảo khả năng khôi phục (Restore) khi xảy ra sự cố. AWS cung cấp bộ dịch vụ **AWS Backup**, kết hợp với **Amazon SNS**, **AWS Lambda** và **Amazon EC2**, giúp tự động hóa toàn bộ quy trình sao lưu, kiểm tra khả năng phục hồi và tối ưu chi phí vận hành.

Các điểm chính cần nắm:

* AWS Backup cho phép xây dựng và quản lý tập trung các kế hoạch sao lưu cho nhiều dịch vụ như Amazon EC2, Amazon RDS, Amazon EBS và Amazon DynamoDB.
* Áp dụng các chỉ số **RPO (Recovery Point Objective)** và **RTO (Recovery Time Objective)** để xây dựng chiến lược bảo vệ dữ liệu phù hợp với từng hệ thống.
* Triển khai hạ tầng bằng **AWS CloudFormation (Infrastructure as Code)** giúp tự động tạo EC2, SNS, Lambda và các tài nguyên liên quan, giảm thiểu lỗi cấu hình thủ công.
* Sử dụng **Tag-based Backup** để tự động bảo vệ các tài nguyên có cùng nhãn mà không cần cấu hình riêng lẻ.
* Kết hợp **Amazon SNS** và **AWS Lambda** để tự động kiểm tra khả năng phục hồi sau mỗi lần sao lưu.
* Tự động thực hiện **Test Restore**, xác minh hệ thống hoạt động bình thường trước khi xóa tài nguyên phục hồi nhằm tối ưu chi phí.
* Theo dõi và xác minh trạng thái Backup thông qua **AWS CLI** và các thông báo từ Amazon SNS.
* Áp dụng các nguyên tắc **Automation**, **Infrastructure as Code** và **Least Privilege** để xây dựng hệ thống sao lưu an toàn, dễ mở rộng và phù hợp với môi trường Production.

Giải pháp này đặc biệt phù hợp với các hệ thống yêu cầu tính sẵn sàng cao, giúp doanh nghiệp tự động hóa quy trình sao lưu, giảm thiểu rủi ro mất dữ liệu và đảm bảo khả năng khôi phục nhanh chóng khi xảy ra sự cố.





## Hướng dẫn thực hiện

### Bước 1: Chuẩn bị hạ tầng

- Tạo S3 Bucket lưu trữ CloudFormation Template và mã nguồn Lambda.
- Chuẩn bị các tệp:
  - backup-lab.yaml
  - lambda_function.zip
- Triển khai Stack bằng AWS CloudFormation tại Region **ap-southeast-1 (Singapore)**.

### Bước 2: Tạo Backup Plan

- Tạo Backup Vault.
- Cấu hình Backup Rule theo lịch hằng ngày.
- Thiết lập Resource Assignment dựa trên Tag.
- Gán IAM Role cho AWS Backup.

### Bước 3: Cấu hình thông báo

- Tạo Amazon SNS Topic.
- Đăng ký Email nhận thông báo.
- Cấu hình Backup Vault Notification bằng AWS CLI.

### Bước 4: Tự động kiểm tra phục hồi

- Tạo AWS Lambda để thực hiện Test Restore.
- Cấu hình SNS kích hoạt Lambda khi Backup hoàn tất.
- Kiểm tra trạng thái Restore và xác thực ứng dụng hoạt động bình thường.

### Bước 5: Kiểm thử hệ thống

- Thực hiện Backup theo yêu cầu.
- Kiểm tra Email thông báo.
- Theo dõi quá trình Restore.
- Xác minh các tài nguyên phục hồi được tự động dọn dẹp sau khi kiểm tra thành công.

### Kết quả đạt được

- Tự động hóa toàn bộ quy trình Backup và Restore trên AWS.
- Kiểm tra khả năng khôi phục dữ liệu sau mỗi lần sao lưu.
- Giảm thiểu thao tác thủ công nhờ Infrastructure as Code.
- Nâng cao khả năng bảo vệ dữ liệu và tối ưu chi phí vận hành.

## Nguồn tham khảo

![AWS Backup & Restore](/images/3-Blogs/blog1.png)
- Workshop: https://000133.awsstudygroup.com/
📌 Bài viết trên AWS Study Group: https://www.facebook.com/share/p/1EEHwMujCD/