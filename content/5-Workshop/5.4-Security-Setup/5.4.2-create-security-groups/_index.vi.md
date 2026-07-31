---
title : "Tạo Security Groups"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

Security Group hoạt động như một tường lửa ảo (virtual firewall) ở cấp độ instance, kiểm soát traffic ra/vào. Trong phần này, bạn sẽ tạo 2 Security Group: một cho EC2 (mở các cổng cần thiết để truy cập ứng dụng), một cho RDS (chỉ chấp nhận kết nối từ đúng EC2, không mở ra Internet).

#### Bước 1: Tạo Security Group cho EC2

1. Vào **EC2 Console** → **Security Groups** → click **Create security group**.
2. Ở phần **Basic details**, cấu hình:
   - **Security group name**: `library-ec2-sg`
   - **Description**: `SG for EC2 - web server`
   - **VPC**: chọn `vpc-0686bd0330b6b622f (library-vpc)`
3. Ở phần **Inbound rules**, thêm 3 rule:

| Type | Protocol | Port range | Source |
|---|---|---|---|
| SSH | TCP | 22 | My IP |
| HTTP | TCP | 80 | Anywhere-IPv4 (0.0.0.0/0) |
| Custom TCP | TCP | 8000 | Anywhere-IPv4 (0.0.0.0/0) |

4. Giữ nguyên **Outbound rules** mặc định (All traffic).
5. Kéo xuống cuối, click **Create security group**.

![create-ec2-sg](/images/5-Workshop/5.4-Security-Setup/5.4.2-create-security-groups/create-ec2-sg.png)

#### Bước 2: Tạo Security Group cho RDS

6. Vẫn ở **Security Groups**, click **Create security group**.
7. Ở phần **Basic details**, cấu hình:
   - **Security group name**: `library-rds-sg`
   - **Description**: `SG for RDS - database`
   - **VPC**: chọn `vpc-0686bd0330b6b622f (library-vpc)` (giống hệt)

![basic-details-rds-sg](/images/5-Workshop/5.4-Security-Setup/5.4.2-create-security-groups/basic-details-rds-sg.png)

8. Ở phần **Inbound rules**, thêm 1 rule:
   - **Type**: PostgreSQL
   - **Protocol/Port**: TCP / 5432 (tự động điền)
   - **Source**: chọn **Custom**, gõ vào ô tìm kiếm và chọn Security Group **`library-ec2-sg`** (không phải địa chỉ IP)
9. Click **Create security group**.

![inbound-rule-rds-sg](/images/5-Workshop/5.4-Security-Setup/5.4.2-create-security-groups/inbound-rule-rds-sg.png)