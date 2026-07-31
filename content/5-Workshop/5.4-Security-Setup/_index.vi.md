---
title : "Thiết lập bảo mật"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Tổng quan

+ Trong phần này, bạn sẽ thiết lập lớp bảo mật cho hệ thống: tạo **IAM User** để ứng dụng có quyền thao tác với S3 một cách an toàn, và tạo **Security Groups** để kiểm soát traffic ra/vào giữa EC2 và RDS.

+ Vì sao cần **IAM User** riêng cho ứng dụng:
    + Thay vì dùng root account key (có toàn quyền, rất nguy hiểm nếu lộ), ứng dụng nên dùng một IAM User riêng, chỉ được cấp đúng quyền cần thiết (ví dụ: chỉ thao tác S3) — đúng nguyên tắc **least privilege**.

+ Vì sao cần **Security Groups** riêng cho EC2 và RDS:
    + Security Group hoạt động như một tường lửa ảo (virtual firewall) ở cấp độ instance, kiểm soát traffic ra/vào theo từng rule cụ thể.
    + Thay vì mở toàn bộ traffic, hệ thống chỉ cho phép: EC2 nhận traffic từ Internet ở các cổng cần thiết (SSH, HTTP, 8000), còn RDS **chỉ chấp nhận kết nối từ đúng Security Group của EC2** — không mở ra Internet, giảm tối đa bề mặt tấn công (attack surface).

#### Nội dung

1. [Tạo IAM User](5.4.1-create-iam-user/)
2. [Tạo Security Groups](5.4.2-create-security-groups/)