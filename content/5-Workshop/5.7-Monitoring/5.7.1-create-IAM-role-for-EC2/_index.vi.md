---
title : "Tạo IAM Role cho CloudWatch"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.7.1 </b> "
---

Để EC2 có thể gửi log và metrics lên CloudWatch, instance cần được gắn một IAM Role có quyền tương ứng. Mặc định EC2 chưa có role nào, nên bước đầu tiên là tạo role mới trong IAM Console, sau đó gắn vào instance.

#### Bước 1: Tạo Role mới trong IAM Console

1. Vào **IAM Console** → **Roles**, nhấn **Create role**.

![iam-roles-create-role](/images/5-Workshop/5.7-Monitoring/5.7.1-create-IAM-role-for-EC2/iam-roles-create-role.png)

2. Ở mục **Service or use case**, chọn/gõ **EC2**.
3. Ở phần **Use case**, chọn **EC2** (Allows EC2 instances to call AWS services on your behalf), rồi nhấn **Next**.

![select-ec2-use-case](/images/5-Workshop/5.7-Monitoring/5.7.1-create-IAM-role-for-EC2/select-ec2-use-case.png)

4. Ở mục **Permissions policies**, tìm `CloudWatchAgentServerPolicy`.
5. Tick chọn policy này, rồi nhấn **Next**.

![attach-cloudwatch-agent-policy](/images/5-Workshop/5.7-Monitoring/5.7.1-create-IAM-role-for-EC2/attach-cloudwatch-agent-policy.png)

{{% notice note %}}
`CloudWatchAgentServerPolicy` là policy do AWS quản lý, cấp đủ quyền cần thiết để CloudWatch Agent trên EC2 gửi log và metrics lên CloudWatch.
{{% /notice %}}

6. Nhập tên Role, ví dụ: `library-ec2-cloudwatch-role`.
7. Điền mô tả ngắn gọn, ví dụ: *"Allows EC2 instances to call AWS services on your behalf"*.
8. Kiểm tra lại **Trust policy** (mặc định đã cho phép EC2 assume role này), sau đó cuộn xuống và nhấn **Create role**.

![name-and-create-role](/images/5-Workshop/5.7-Monitoring/5.7.1-create-IAM-role-for-EC2/name-and-create-role.png)

#### Bước 2: Gắn Role vừa tạo vào EC2 Instance

9. Vào **EC2 Console** → **Instances**, chọn instance đang chạy ứng dụng.
10. Nhấn **Actions** → **Security** → **Modify IAM role**.

![modify-iam-role](/images/5-Workshop/5.7-Monitoring/5.7.1-create-IAM-role-for-EC2/modify-iam-role.png)

11. Ở mục **IAM role**, chọn `library-ec2-cloudwatch-role` vừa tạo.
12. Nhấn **Update IAM role** để xác nhận.

![update-iam-role](/images/5-Workshop/5.7-Monitoring/5.7.1-create-IAM-role-for-EC2/update-iam-role.png)

Sau bước này, EC2 đã có đủ quyền để chạy CloudWatch Agent. Bước tiếp theo (5.7.2) sẽ cài đặt và cấu hình Agent trên instance.