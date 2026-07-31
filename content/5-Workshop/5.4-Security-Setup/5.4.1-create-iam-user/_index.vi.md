---
title : "Tạo IAM User"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

IAM User được tạo để ứng dụng Django (chạy trên EC2) có quyền ghi dữ liệu lên S3 mà không cần dùng đến root account key — tuân theo nguyên tắc **least privilege** (chỉ cấp đúng quyền cần thiết).

#### Bước 1: Tạo User

1. Vào **IAM Console** → **IAM users** → click **Create user**.
2. Ở màn hình **Specify user details**:
   - **User name**: `library-app-user`
   - **Không tick** ô "Provide user access to the AWS Management Console" (user này chỉ cần truy cập lập trình qua Access Key, không cần đăng nhập Console)
3. Click **Next**.

![specify-user-details](/images/5-Workshop/5.4-Security-Setup/5.4.1-create-iam-user/specify-user-details.png)

#### Bước 2: Gán quyền

4. Ở màn hình **Set permissions**, chọn **Attach policies directly**.
5. Tìm và tick chọn policy **`AmazonS3FullAccess`**.
6. Click **Next**, sau đó **Create user** ở màn hình review.

![set-permissions](/images/5-Workshop/5.4-Security-Setup/5.4.1-create-iam-user/set-permissions.png)

{{% notice note %}}
Nếu với môi trường production thật, nên tạo custom policy chỉ cho phép thao tác trên đúng 1 bucket cụ thể thay vì cấp quyền trên toàn bộ S3.
{{% /notice %}}

#### Bước 3: Tạo Access Key

7. Sau khi tạo user xong, vào trang chi tiết `library-app-user`, ở mục **Access key 1**, click **Create access key**.

![create-access-key-button](/images/5-Workshop/5.4-Security-Setup/5.4.1-create-iam-user/create-access-key-button.png)

8. Ở bước chọn **Use case**, chọn **Application running on an AWS compute service** (vì ứng dụng sẽ chạy trên EC2), tick xác nhận khuyến nghị, click **Next**.

![select-use-case](/images/5-Workshop/5.4-Security-Setup/5.4.1-create-iam-user/select-use-case.png)

9. (Tuỳ chọn) Ở bước **Set description tag**, điền mô tả, ví dụ `library-app-key`, click **Create access key**.

![set-description-tag](/images/5-Workshop/5.4-Security-Setup/5.4.1-create-iam-user/set-description-tag.png)

10. Màn hình **Retrieve access keys** hiển thị **Access key ID** và **Secret access key**.

![retrieve-access-keys](/images/5-Workshop/5.4-Security-Setup/5.4.1-create-iam-user/retrieve-access-keys.png)

{{% notice warning %}}
**Secret access key chỉ hiển thị đúng 1 lần.** Bấm **Download .csv file** hoặc copy lại ngay 2 giá trị này vào nơi an toàn trước khi bấm **Done** — đóng trang này ra là không xem lại được, phải tạo access key mới nếu quên lưu.
{{% /notice %}}

Hai giá trị này sẽ được điền vào file `.env` của ứng dụng ở bước cấu hình sau:
```
AWS_ACCESS_KEY_ID=<access key vừa tạo>
AWS_SECRET_ACCESS_KEY=<secret key vừa tạo>
```