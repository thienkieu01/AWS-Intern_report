---
title : "Build và chạy ứng dụng"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.6.3 </b> "
---

Sau khi đã cài Docker và cấu hình `.env`, bước cuối cùng là sửa cấu hình `docker-compose.yml`, build container, và khởi tạo dữ liệu cho ứng dụng.

#### Bước 1: Sửa `DJANGO_SETTINGS_MODULE` trong `docker-compose.yml`

Mở file `docker/docker-compose.yml`:

```bash
nano docker/docker-compose.yml
```

Tìm dòng `DJANGO_SETTINGS_MODULE`, đảm bảo trỏ đến `production` thay vì `local`:

```yaml
environment:
  DJANGO_SETTINGS_MODULE: config.settings.production
```

{{% notice warning %}}
Nếu để `config.settings.local`, ứng dụng sẽ không đọc đúng cấu hình S3 và ảnh bìa sách sẽ không upload lên được — đây là lỗi thực tế đã gặp trong quá trình triển khai.
{{% /notice %}}

#### Bước 2: Build và chạy container

```bash
docker compose -f docker/docker-compose.yml up -d --build
```

Lệnh này vừa build image vừa chạy container ở chế độ nền (`-d`).

Kiểm tra container đang chạy:

```bash
docker compose -f docker/docker-compose.yml ps
```

Nếu cần xem log để debug lỗi:

```bash
docker compose -f docker/docker-compose.yml logs -f
```

Nhấn `Ctrl+C` để thoát khỏi chế độ theo dõi log.

#### Bước 3: Tạo migration, migrate database, tạo superuser và import dữ liệu

1. Tạo migration:

```bash
docker compose -f docker/docker-compose.yml exec web python manage.py makemigrations
```

2. Migrate database:

```bash
docker compose -f docker/docker-compose.yml exec web python manage.py migrate
```

3. Tạo superuser:

```bash
docker compose -f docker/docker-compose.yml exec web python manage.py createsuperuser
```

4. Import dữ liệu mẫu (flush dữ liệu cũ trước khi import):

```bash
docker compose -f docker/docker-compose.yml exec web python manage.py import_legacy_csv --flush
```

{{% notice note %}}
Đảm bảo chạy các lệnh này sau khi đã sửa `DJANGO_SETTINGS_MODULE` sang `production` — nếu chạy khi còn dùng `local`, superuser/dữ liệu sẽ được tạo trên database khác (Docker volume), không phải RDS thật.
{{% /notice %}}

#### Bước 4: Xử lý lỗi `ERR_SSL_PROTOCOL_ERROR`

Nếu truy cập bằng `http://` mà trình duyệt tự chuyển sang `https://` và báo lỗi SSL, nguyên nhân do `SECURE_SSL_REDIRECT=True` trong `production.py` ép HTTPS trong khi EC2 chưa có SSL certificate.

Mở file settings production:

```bash
nano config/settings/production.py
```

Tìm và sửa các dòng sau về `False` / `0`:

```python
SECURE_SSL_REDIRECT = False
SESSION_COOKIE_SECURE = False
CSRF_COOKIE_SECURE = False
SECURE_HSTS_SECONDS = 0
```

Rebuild lại container để áp dụng thay đổi:

```bash
docker compose -f docker/docker-compose.yml up -d --build
```

{{% notice warning %}}
Nếu trình duyệt từng bị redirect sang HTTPS trước đó, cần xóa cache HSTS: mở `chrome://net-internals/#hsts`, nhập domain/IP vào ô "Delete domain security policies" rồi xóa, sau đó thử lại.
{{% /notice %}}

#### Bước 5: Truy cập ứng dụng

Mở trình duyệt, truy cập:

```
http://54.82.167.72:8000
```

Nếu thấy giao diện đăng nhập của ứng dụng Library Management System là đã triển khai thành công.