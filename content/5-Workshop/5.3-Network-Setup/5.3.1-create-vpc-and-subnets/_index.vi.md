---
title : "Tạo VPC và các Subnet"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

#### Bước 1: Tạo VPC

1. Mở [Amazon VPC console]
2. Trong thanh điều hướng, chọn **Your VPCs**, click **Create VPC**.
3. Trong màn hình **Create VPC**, cấu hình như sau:
   - **Resources to create**: chọn **VPC only**
   - **Name tag**: `library-vpc`
   - **IPv4 CIDR block**: `10.0.0.0/16`
   - **IPv6 CIDR block**: No IPv6 CIDR block
   - **Tenancy**: Default

![create-vpc](/images/5-Workshop/5.3-Network-Setup/5.3.1-create-vpc-and-subnets/create-vpc.png)

{{% notice note %}}
Dải CIDR `10.0.0.0/16` cho phép tối đa 65,536 địa chỉ IP trong VPC, đủ để chia thành nhiều subnet nhỏ cho public và private.
{{% /notice %}}

4. Kéo xuống cuối trang, kiểm tra lại thông tin (Name tag, IPv4 CIDR) rồi click **Create VPC**.

![create-vpc-confirm](/images/5-Workshop/5.3-Network-Setup/5.3.1-create-vpc-and-subnets/create-vpc-confirm.png)

5. Sau khi tạo thành công, bạn sẽ nhận được **VPC ID** (ví dụ: `vpc-0686bd0330b6b622f`) — ghi nhớ ID này để dùng cho các bước tiếp theo.

---

#### Bước 2: Bật DNS settings cho VPC

{{% notice warning %}}
Đây là bước dễ bị bỏ sót nhưng **bắt buộc** — nếu không bật, RDS và các dịch vụ nội bộ khác trong VPC có thể không phân giải được tên miền đúng cách, gây lỗi kết nối khó chẩn đoán về sau.
{{% /notice %}}

6. Trong **VPC Console**, chọn VPC `library-vpc` vừa tạo.
7. Click **Actions** → **Edit VPC settings**.
8. Ở phần **DNS settings**, tick chọn cả 2 ô:
   - **Enable DNS resolution**
   - **Enable DNS hostnames**
9. Click **Save**.

![vpc-dns-settings](/images/5-Workshop/5.3-Network-Setup/5.3.1-create-vpc-and-subnets/vpc-dns-settings.png)

{{% notice note %}}
- **Enable DNS resolution**: cho phép các instance trong VPC sử dụng DNS server nội bộ của Amazon để phân giải tên miền.
- **Enable DNS hostnames**: cho phép instance có địa chỉ IP public được gán thêm 1 DNS hostname tương ứng.

Cả 2 cài đặt này cần thiết để RDS endpoint (dạng `library-db.xxxxx.rds.amazonaws.com`) phân giải đúng thành địa chỉ IP nội bộ khi EC2 kết nối tới.
{{% /notice %}}

---

#### Bước 3: Tạo Subnet

Trong phần này, bạn sẽ tạo 3 subnet trong `library-vpc`:

| Subnet | CIDR | Availability Zone | Loại |
|---|---|---|---|
| public-subnet | 10.0.1.0/24 | us-east-1a | Public |
| private-subnet-1 | 10.0.2.0/24 | us-east-1a | Private |
| private-subnet-2 | 10.0.3.0/24 | us-east-1b | Private |

{{% notice tip %}}
Tạo 2 private subnet ở 2 Availability Zone khác nhau (us-east-1a và us-east-1b) để đảm bảo tính sẵn sàng cao (Multi-AZ) khi sau này triển khai RDS.
{{% /notice %}}

10. Trong thanh điều hướng, chọn **Subnets**, click **Create subnet**.
11. Ở phần **VPC**, chọn `vpc-0686bd0330b6b622f (library-vpc)`.

![select-vpc](/images/5-Workshop/5.3-Network-Setup/5.3.1-create-vpc-and-subnets/select-vpc.png)

**Tạo public-subnet:**

12. Nhập thông tin:
    - **Subnet name**: `public-subnet`
    - **Availability Zone**: `us-east-1a`
    - **IPv4 subnet CIDR block**: `10.0.1.0/24`
13. Click **Create subnet**.

![public-subnet](/images/5-Workshop/5.3-Network-Setup/5.3.1-create-vpc-and-subnets/public-subnet.png)

**Tạo private-subnet-1:**

14. Click **Add new subnet**, nhập:
    - **Subnet name**: `private-subnet-1`
    - **Availability Zone**: `us-east-1a`
    - **IPv4 subnet CIDR block**: `10.0.2.0/24`
15. Click **Create subnet**.

![private-subnet-1](/images/5-Workshop/5.3-Network-Setup/5.3.1-create-vpc-and-subnets/private-subnet-1.png)

**Tạo private-subnet-2:**

16. Click **Add new subnet**, nhập:
    - **Subnet name**: `private-subnet-2`
    - **Availability Zone**: `us-east-1b`
    - **IPv4 subnet CIDR block**: `10.0.3.0/24`
17. Click **Create subnet**.

![private-subnet-2](/images/5-Workshop/5.3-Network-Setup/5.3.1-create-vpc-and-subnets/private-subnet-2.png)

{{% notice note %}}
Sau khi hoàn tất, bạn sẽ có 1 VPC (`library-vpc`) đã bật DNS resolution/hostnames, chứa 3 subnet: 1 public subnet dùng cho EC2, 2 private subnet dùng cho RDS (Multi-AZ).
{{% /notice %}}