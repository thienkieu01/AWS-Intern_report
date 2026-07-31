---
title : "Launch EC2 và gán Elastic IP"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.6.1 </b> "
---

EC2 là nơi chạy ứng dụng Django trong môi trường Docker, đặt tại Public Subnet đã tạo ở mục 5.3, gắn Security Group `library-ec2-sg` đã tạo ở mục 5.4.

#### Bước 1: Đặt tên và chọn AMI

1. Vào **EC2 Console** → **Instances** → click **Launch an instance**.
2. Ở phần **Name and tags**, điền **Name**: `Library Management System`.
3. Ở phần **Application and OS Images (AMI)**, chọn **Ubuntu** (Ubuntu Server 26.04 LTS).

![name-and-ami](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/name-and-ami.png)

#### Bước 2: Tạo Key Pair

4. Ở phần **Key pair (login)**, click **Create new key pair**.

![create-key-pair-button](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/create-key-pair-button.png)

5. Điền:
   - **Key pair name**: `library-key`
   - **Key pair type**: RSA
   - **Private key file format**: .pem
6. Click **Create key pair** — file `.pem` sẽ tự động tải về máy.

![create-key-pair-form](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/create-key-pair-form.png)

{{% notice warning %}}
File `.pem` chỉ tải về được **1 lần duy nhất**. Lưu file này cẩn thận — sẽ cần dùng để SSH vào EC2 ở bước sau.
{{% /notice %}}

#### Bước 3: Chọn Instance type

7. Kéo xuống phần **Instance type**, chọn `t3.small` (2 vCPU, 2 GiB Memory).

![select-instance-type](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/select-instance-type.png)

{{% notice note %}}
AWS mặc định gợi ý `t3.micro` (1 GiB RAM), nhưng thực tế khi chạy đồng thời Docker + CloudWatch Agent + SSH, `t3.micro` dễ hết RAM gây lỗi mất kết nối. Nên chọn thẳng `t3.small` (2 GiB RAM) ngay từ đầu để tránh phải đổi lại instance type sau này.
{{% /notice %}}

#### Bước 4: Cấu hình Network settings

8. Kéo xuống phần **Network settings**, click **Edit**, cấu hình:
   - **VPC**: chọn `library-vpc (vpc-0686bd0330b6b622f)`
   - **Subnet**: chọn `public-subnet`
   - **Auto-assign public IP**: **Enable**
   - **Firewall (security groups)**: chọn **Select existing security group** → chọn `library-ec2-sg`

![network-settings](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/network-settings.png)

#### Bước 5: Launch instance

9. Kiểm tra lại **Summary** (instance type `t3.small`, storage 8 GiB), click **Launch instance**.

---

#### Bước 6: Tạo Elastic IP

10. Vào **EC2 Console** → **Network & Security** → **Elastic IPs** → click **Allocate Elastic IP address**.

![elastic-ip-list](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/elastic-ip-list.png)

11. Giữ nguyên mặc định (**Amazon's pool of IPv4 addresses**), click **Allocate**.

![allocate-elastic-ip](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/allocate-elastic-ip.png)

#### Bước 7: Gán Elastic IP vào EC2

12. Sau khi tạo thành công, chọn địa chỉ IP vừa tạo, click **Actions** → **Associate Elastic IP address**.

![associate-elastic-ip-menu](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/associate-elastic-ip-menu.png)

13. Ở phần **Instance**, chọn instance vừa launch (`Library Management System`).
14. Click **Associate**.

![associate-elastic-ip-form](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/associate-elastic-ip-form.png)

{{% notice note %}}
Elastic IP là địa chỉ IP tĩnh, không đổi dù EC2 bị stop/start lại — tránh việc phải cập nhật lại `ALLOWED_HOSTS` trong `.env` hoặc thông tin SSH mỗi lần restart instance.
{{% /notice %}}

Sau bước này, EC2 đã sẵn sàng với 1 địa chỉ IP cố định để SSH vào và triển khai ứng dụng ở các bước tiếp theo.