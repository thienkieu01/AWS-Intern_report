---
title : "Dọn dẹp tài nguyên"
date : 2024-01-01
weight : 8
chapter : false
pre : " <b> 5.8. </b> "
---

#### Tổng quan

+ Sau khi hoàn thành workshop, nên xóa các tài nguyên AWS đã tạo để tránh phát sinh chi phí ngoài ý muốn (đặc biệt là RDS, Elastic IP, và EC2 nếu không còn nằm trong free tier).

+ Thứ tự xóa **rất quan trọng** — một số tài nguyên phụ thuộc lẫn nhau (ví dụ Security Group của RDS phải xóa trước Security Group của EC2, VPC không thể xóa khi vẫn còn tài nguyên bên trong). Làm theo đúng thứ tự dưới đây để tránh lỗi.

{{% notice warning %}}
Đây là thao tác **không thể hoàn tác**. Toàn bộ dữ liệu trong RDS, ảnh trong S3, và code trên EC2 sẽ mất vĩnh viễn sau khi xóa. Chỉ thực hiện sau khi đã chắc chắn không cần dùng lại.
{{% /notice %}}

#### Bước 1: Terminate EC2 Instance

1. Vào **EC2 Console** → **Instances**, chọn instance đang chạy ứng dụng.
2. **Instance state** → **Terminate (delete) instance**.

![terminate-ec2-menu](/images/5-Workshop/5.8-Cleanup/terminate-ec2-menu.png)

3. Xác nhận bằng cách nhấn **Terminate (delete)**.

![terminate-ec2-confirm](/images/5-Workshop/5.8-Cleanup/terminate-ec2-confirm.png)

#### Bước 2: Release Elastic IP

Elastic IP vẫn bị tính phí nếu không gắn với instance đang chạy — cần release riêng sau khi terminate EC2:

4. Vào **EC2 Console** → **Elastic IPs**, chọn địa chỉ IP đã dùng (ví dụ `54.82.167.72`).
5. Nếu IP vẫn còn hiển thị đang gắn (Associated instance ID), chọn **Actions** → **Disassociate Elastic IP address** trước.

![disassociate-eip](/images/5-Workshop/5.8-Cleanup/disassociate-eip.png)

6. Sau đó chọn **Actions** → **Release Elastic IP addresses**, nhấn **Release** để xác nhận.

![release-eip-confirm](/images/5-Workshop/5.8-Cleanup/release-eip-confirm.png)

#### Bước 3: Xóa RDS Database

7. Vào **RDS Console** → **Databases**, chọn `library-db`.
8. **Actions** → **Delete**.

![delete-rds-menu](/images/5-Workshop/5.8-Cleanup/delete-rds-menu.png)

9. Bỏ tick **Create final snapshot** (nếu không cần lưu lại dữ liệu), gõ `delete me` vào ô xác nhận, rồi nhấn **Delete**.

![delete-rds-confirm](/images/5-Workshop/5.8-Cleanup/delete-rds-confirm.png)

{{% notice note %}}
Xóa RDS có thể mất vài phút. Sau khi RDS xóa xong, **DB Subnet Group** (liên kết 2 Private Subnet) và **Security Group của RDS** (Bước 7) mới có thể xóa được.
{{% /notice %}}

#### Bước 4: Xóa dữ liệu trong S3 Bucket

S3 Bucket không xóa được nếu bên trong còn object:

10. Vào **S3 Console**, chọn bucket `library-workshop-2026`.
11. Nhấn **Empty**, gõ `permanently delete` để xác nhận, đợi quá trình xóa hoàn tất.

![empty-bucket-confirm](/images/5-Workshop/5.8-Cleanup/empty-bucket-confirm.png)

12. Sau khi bucket đã trống, nhấn **Delete**, gõ đúng tên bucket để xác nhận.

#### Bước 5: Xóa IAM User và IAM Role

13. Vào **IAM Console** → **Users**, chọn `library-app-user`.
14. Vào tab **Security credentials**, tìm **Access keys**, chọn key đang **Active** → **Deactivate** → xác nhận, sau đó **Delete** để xóa hẳn key.

{{% notice warning %}}
Phải **deactivate và xóa Access Key trước**, không thể xóa IAM User trực tiếp khi vẫn còn Access Key đang tồn tại.
{{% /notice %}}

15. Sau khi đã xóa hết Access Key, quay lại trang **Users**, chọn `library-app-user` → **Delete**, gõ `confirm` để xác nhận, nhấn **Delete user**.

![delete-iam-user-confirm](/images/5-Workshop/5.8-Cleanup/delete-iam-user-confirm.png)

16. Vào **IAM Console** → **Roles**, chọn `library-ec2-cloudwatch-role` → **Delete**.

#### Bước 6: Xóa CloudWatch Log Group

17. Vào **CloudWatch Console** → **Log groups**, chọn `library-app-logs` → **Actions** → **Delete log group(s)**.

#### Bước 7: Xóa Security Groups

Security Group của EC2 (`library-ec2-sg`) đang được Security Group của RDS (`library-rds-sg`) tham chiếu tới trong rule inbound, nên phải xóa **`library-rds-sg` trước**:

18. Vào **EC2 Console** → **Security Groups**, chọn `library-rds-sg` → **Actions** → **Delete security groups** → xác nhận.

![delete-rds-sg-confirm](/images/5-Workshop/5.8-Cleanup/delete-rds-sg-confirm.png)

19. Sau khi `library-rds-sg` đã xóa xong, chọn tiếp `library-ec2-sg` → **Delete security groups** → xác nhận.

![delete-ec2-sg-confirm](/images/5-Workshop/5.8-Cleanup/delete-ec2-sg-confirm.png)

#### Bước 8: Xóa VPC và các thành phần liên quan

20. Vào **VPC Console** → **Your VPCs**, chọn `library-vpc`.
21. Nhấn **Actions** → **Delete VPC**. AWS sẽ hiển thị danh sách toàn bộ tài nguyên con sẽ bị xóa kèm theo, ví dụ: `library-igw`, `public-rt`, `private-rt`, `public-subnet`, `private-subnet-1`...
22. Gõ `delete` vào ô xác nhận, nhấn **Delete**.

{{% notice note %}}
Nếu **Delete VPC** báo lỗi do còn tài nguyên phụ thuộc chưa xóa hết, quay lại kiểm tra đã hoàn thành đúng thứ tự Bước 1–7 chưa, đặc biệt là RDS (Bước 3) và Security Groups (Bước 7).
{{% /notice %}}
