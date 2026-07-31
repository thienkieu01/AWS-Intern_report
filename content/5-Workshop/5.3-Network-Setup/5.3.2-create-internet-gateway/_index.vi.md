---
title : "Tạo Internet Gateway"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

Internet Gateway (IGW) là thành phần cho phép các tài nguyên trong public subnet (như EC2) giao tiếp được với Internet.

#### Bước 1: Tạo Internet Gateway

1. Trong thanh điều hướng của VPC console, chọn **Internet Gateways**, click **Create internet gateway**.
2. Cấu hình:
   - **Name tag**: `library-igw`
3. Click **Create internet gateway**.

![create-igw](/images/5-Workshop/5.3-network-setup/5.3.2-create-internet-gateway/create-igw.png)

4. Sau khi tạo thành công, chọn `library-igw` vừa tạo, click **Actions** → **Attach to VPC**.

![select-attach-to-vpc](/images/5-Workshop/5.3-network-setup/5.3.2-create-internet-gateway/select-attach-to-vpc.png)

#### Bước 2: Gắn Internet Gateway vào VPC

5. Trong màn hình **Attach to VPC**, ở phần **Available VPCs**, nhập/chọn VPC `vpc-0686bd0330b6b622f` (`library-vpc`).
6. Click **Attach internet gateway**.

![attach-igw-confirm](/images/5-Workshop/5.3-network-setup/5.3.2-create-internet-gateway/attach-igw-confirm.png)

{{% notice note %}}
Mỗi VPC chỉ có thể gắn với **duy nhất 1** Internet Gateway tại một thời điểm. Sau khi attach thành công, trạng thái của `library-igw` sẽ chuyển từ `Detached` sang `Attached`.
{{% /notice %}}