---
title : "Tạo S3 Bucket"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.5.2 </b> "
---

Amazon S3 dùng để lưu trữ hình ảnh bìa sách và các tệp tài liệu do người dùng tải lên, tách biệt khỏi vòng đời của EC2 để đảm bảo dữ liệu bền vững.

#### Bước 1: Tạo Bucket

1. Vào **S3 Console** → **Buckets** → click **Create bucket**.
2. Ở phần **General configuration**:
   - **AWS Region**: US East (N. Virginia) us-east-1 (khớp với EC2/RDS)
   - **Bucket type**: General purpose
   - **Bucket name**: `library-workshop-2026` (tên phải **unique toàn cầu**, đổi thành tên riêng của bạn nếu bị trùng)

![create-bucket-name](/images/5-Workshop/5.5-Database-and-storage/5.5.2-create-S3-bucket/create-bucket-name.png)

#### Bước 2: Cấu hình Block Public Access

3. Kéo xuống phần **Block Public Access settings for this bucket**, **bỏ tick** ô **Block all public access**.
4. Tick vào ô xác nhận **"I acknowledge that the current settings might result in this bucket and the objects within becoming public."**

![block-public-access](/images/5-Workshop/5.5-Database-and-storage/5.5.2-create-S3-bucket/block-public-access.png)

{{% notice note %}}
Bỏ Block Public Access để cho phép ảnh bìa sách hiển thị công khai qua URL trên giao diện web. Đây là lựa chọn phù hợp cho đồ án/demo — với hệ thống production thật, nên cân nhắc dùng CloudFront + Signed URL thay vì mở public trực tiếp.
{{% /notice %}}

#### Bước 3: Cấu hình Encryption và tạo Bucket

5. Ở phần **Default encryption**, giữ nguyên **Server-side encryption with Amazon S3 managed keys (SSE-S3)**.
6. Các phần khác (Versioning, Tags, Advanced settings) giữ nguyên mặc định.
7. Kéo xuống cuối, click **Create bucket**.

![create-bucket-button](/images/5-Workshop/5.5-Database-and-storage/5.5.2-create-S3-bucket/create-bucket-button.png)

#### Bước 4: Cấu hình Bucket Policy để cho phép đọc công khai

8. Sau khi bucket được tạo, vào bucket `library-workshop-2026` → tab **Permissions**.
9. Kéo xuống mục **Bucket policy** → click **Edit**.

![permissions-tab](/images/5-Workshop/5.5-Database-and-storage/5.5.2-create-S3-bucket/permissions-tab.png)

10. Dán vào đoạn policy sau (nhớ thay `library-workshop-2026` bằng đúng tên bucket của bạn):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::library-workshop-2026/*"
    }
  ]
}
```

11. Click **Save changes**.

![save-bucket-policy](/images/5-Workshop/5.5-Database-and-storage/5.5.2-create-S3-bucket/save-bucket-policy.png)

{{% notice note %}}
Bucket Policy này cho phép **bất kỳ ai** đọc (GetObject) các file trong bucket qua URL trực tiếp, phục vụ việc hiển thị ảnh bìa sách trên trang web. Chỉ có quyền **đọc**, không cho phép ghi/xóa từ bên ngoài — việc ghi file vẫn chỉ thực hiện được qua ứng dụng, dùng Access Key của `library-app-user`.
{{% /notice %}}

Sau bước này, bucket của bạn đã sẵn sàng để ứng dụng Django ghi và hiển thị ảnh bìa sách. Thông tin cần dùng ở bước cấu hình `.env` sau:
```
AWS_STORAGE_BUCKET_NAME=library-workshop-2026
AWS_S3_REGION_NAME=us-east-1
```