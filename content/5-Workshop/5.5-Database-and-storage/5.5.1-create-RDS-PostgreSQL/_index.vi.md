---
title : "Tạo RDS PostgreSQL"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.5.1 </b> "
---

RDS PostgreSQL dùng để lưu trữ toàn bộ dữ liệu nghiệp vụ của hệ thống (sách, người dùng, lịch sử mượn trả), được đặt trong Private Subnet để không thể truy cập trực tiếp từ Internet.

#### Bước 1: Chọn phương thức tạo database

1. Vào **RDS Console** → **Databases** → click **Create database**.
2. Ở dropdown hiện ra, chọn **Full configuration** (cho phép cấu hình chi tiết VPC, Subnet Group, Security Group — thay vì để AWS tự chọn như Express configuration).

![select-full-configuration](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/select-full-configuration.png)

#### Bước 2: Chọn Engine

3. Ở phần **Engine options**, chọn **PostgreSQL**.
4. Ở phần **Choose a database creation method**, giữ nguyên **Full configuration**.

![choose-engine-postgresql](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/choose-engine-postgresql.png)

#### Bước 3: Chọn Template và Deployment option

5. Ở phần **Templates**, chọn **Dev/Test** (phù hợp cho đồ án/workshop, không cần tối ưu chi phí như Production).
6. Ở phần **Availability and durability**, chọn **Single-AZ DB instance deployment (1 instance)** — chỉ tạo 1 instance chính, không có standby, phù hợp vì đây là môi trường học tập, không cần tính sẵn sàng cao.

![template-and-deployment](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/template-and-deployment.png)

#### Bước 4: Cấu hình Settings

7. Ở phần **Settings**, điền:
   - **DB instance identifier**: `library-db`
   - **Master username**: `postgres`
   - **Credentials management**: chọn **Self managed**
   - **Master password**: đặt password mạnh, **ghi lại cẩn thận**
   - **Confirm master password**: nhập lại

![settings-credentials](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/settings-credentials.png)

#### Bước 5: Cấu hình Instance và Storage

8. Ở phần **Instance configuration**:
   - Chọn **Burstable classes (includes t classes)**
   - **Instance type**: `db.t3.micro` (free tier)
9. Ở phần **Storage**:
   - **Storage type**: General Purpose SSD (gp3)
   - **Allocated storage**: `20` GiB

![instance-and-storage](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/instance-and-storage.png)

#### Bước 6: Cấu hình Connectivity

10. Ở phần **Connectivity**:
    - **Virtual private cloud (VPC)**: chọn `library-vpc (vpc-0686bd0330b6b622f)`
    - **DB subnet group**: chọn **Create new DB Subnet Group**
    - **Public access**: chọn **No**
    - **VPC security group (firewall)**: chọn **Choose existing** → chọn `library-rds-sg`

![connectivity-settings](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/connectivity-settings.png)

{{% notice note %}}
**Public access = No** đảm bảo RDS không được gán địa chỉ IP công khai — chỉ tài nguyên nằm trong VPC (cụ thể là EC2 mang Security Group `library-ec2-sg`) mới kết nối được tới database.
{{% /notice %}}

#### Bước 7: Cấu hình Additional configuration

11. Kéo xuống phần **Additional configuration** → **Database options**, điền:
    - **Initial database name**: `library_db`

{{% notice warning %}}
Đây là tên database quan trọng — phải khớp chính xác với biến `POSTGRES_DB` trong file `.env` ở bước cấu hình ứng dụng sau này, nếu không Django sẽ báo lỗi không tìm thấy database.
{{% /notice %}}

![initial-database-name](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/initial-database-name.png)

12. Các phần còn lại (Backup, Encryption, Monitoring...) giữ nguyên mặc định.

#### Bước 8: Tạo database

13. Kéo xuống cuối trang, xem lại **Estimated monthly costs**, click **Create database**.

![create-database-button](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/create-database-button.png)

14. Chờ khoảng 5–10 phút để trạng thái chuyển từ **Creating** → **Available**.

#### Bước 9: Lấy Endpoint để cấu hình ứng dụng

15. Sau khi Available, chọn `library-db` → tab **Connectivity & security**. Ở mục **Connection steps**, dòng `export RDSHOST="..."` chính là **Endpoint** của database.

16. Copy giá trị này lại — sẽ dùng làm `POSTGRES_HOST`/`DB_HOST` trong file `.env` ở bước cấu hình ứng dụng sau.

![rds-endpoint](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/rds-endpoint.png)
