---
title : "Cài Docker và Clone code"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.6.2 </b> "
---

Sau khi EC2 đã có Elastic IP, bước tiếp theo là kết nối vào instance qua VS Code, cài Docker, và tải mã nguồn ứng dụng về.

#### Bước 1: Lấy lại Elastic IP của EC2

1. Vào **EC2 Console** → **Elastic IPs**, chọn địa chỉ IP đã gán cho instance.
2. Copy giá trị **Allocated IPv4 address** (ví dụ: `54.82.167.72`) — dùng để kết nối SSH ở bước sau.

![get-elastic-ip](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/get-elastic-ip.png)

#### Bước 2: Kết nối VS Code vào EC2 qua Remote-SSH

3. Mở VS Code, nhấn `Ctrl+Shift+P` (hoặc `F1`) để mở **Command Palette**.

![open-command-palette](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/open-command-palette.png)

4. Gõ `Remote-SSH`, chọn **Remote-SSH: Connect to Host...**.

![select-remote-ssh-connect](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/select-remote-ssh-connect.png)

5. Chọn **+ Add New SSH Host...** (nếu chưa từng kết nối tới host này trước đó).

![add-new-ssh-host](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/add-new-ssh-host.png)

6. Nhập lệnh SSH đầy đủ, gồm đường dẫn tới file `.pem` và địa chỉ Elastic IP: `ssh -i "C:\Users\Tran\Downloads\library-key.pem" ubuntu@54.82.167.72`

![enter-ssh-command](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/enter-ssh-command.png)

{{% notice note %}}
Thay đường dẫn `.pem` và địa chỉ IP đúng theo máy và Elastic IP thật của bạn. Trên Windows, cần để đường dẫn trong dấu ngoặc kép nếu có khoảng trắng.
{{% /notice %}}

7. Chọn file cấu hình SSH để lưu (thường là `C:\Users\<tên-máy>\.ssh\config`).

![select-ssh-config-file](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/select-ssh-config-file.png)

8. Mở lại **Remote-SSH: Connect to Host...**, lần này sẽ thấy địa chỉ IP đã lưu xuất hiện trong danh sách — chọn nó.

![select-saved-host](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/select-saved-host.png)

9. Khi được hỏi **"Select the platform of the remote host"**, chọn **Linux**.

![select-platform-linux](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/select-platform-linux.png)

10. VS Code sẽ mở cửa sổ mới, kết nối vào EC2. Khi thấy góc dưới trái hiển thị **"SSH: 54.82.167.72"** là đã kết nối thành công.

#### Bước 3: Cài đặt Docker và Docker Compose

Mở **Terminal** trong VS Code (đang chạy trên EC2), chạy lần lượt:

1. Cập nhật danh sách gói:

```bash
sudo apt update -y
```

2. Cài đặt Docker và Docker Compose:

```bash
sudo apt install -y docker.io docker-compose-v2
```

3. Khởi động Docker:

```bash
sudo systemctl start docker
```

4. Cho phép Docker tự khởi động cùng hệ thống:

```bash
sudo systemctl enable docker
```

5. Thêm user `ubuntu` vào group `docker` (để chạy docker không cần sudo):

```bash
sudo usermod -aG docker ubuntu
```

6. Cập nhật quyền ngay lập tức, không cần logout/login lại:

```bash
newgrp docker
```

{{% notice note %}}
Vì EC2 dùng **Ubuntu AMI**, user mặc định là `ubuntu` (không phải `ec2-user` như Amazon Linux), và dùng `apt` thay vì `dnf`/`yum`.
{{% /notice %}}

#### Bước 4: Cài Git và Clone code

1. Cài Git:

```bash
sudo apt install -y git
```

2. Clone repository:

```bash
git clone https://github.com/BuiNgoc2005/library-management-system.git
```

3. Vào thư mục project:

```bash
cd library-management-system
```

#### Bước 5: Tạo và cấu hình file `.env`

```bash
nano .env
```

Điền đầy đủ các biến sau:

```dotenv
# Django Settings
SECRET_KEY=very-secret-key
DEBUG=False
DJANGO_ALLOWED_HOSTS=*

# Database RDS PostgreSQL Settings
POSTGRES_DB=library_db
POSTGRES_USER=postgres
POSTGRES_PASSWORD=LibraryWorkshop2026!
POSTGRES_HOST=library-db.cep2gas62m70.us-east-1.rds.amazonaws.com
POSTGRES_PORT=5432

# AWS S3 Settings
AWS_ACCESS_KEY_ID=YOUR_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY=YOUR_SECRET_ACCESS_KEY
AWS_STORAGE_BUCKET_NAME=library-workshop-2026
AWS_S3_REGION_NAME=us-east-1
```

{{% notice warning %}}
Tên biến (`DB_HOST`, `DB_NAME`...) phải khớp chính xác với tên biến mà file settings Django (`config/settings/...`) đang đọc qua `os.environ.get(...)`. Nếu file settings dùng tên khác (ví dụ `POSTGRES_HOST` thay vì `DB_HOST`), cần sửa lại cho khớp, nếu không ứng dụng sẽ không kết nối được RDS dù `.env` đã điền đủ giá trị.
{{% /notice %}}
