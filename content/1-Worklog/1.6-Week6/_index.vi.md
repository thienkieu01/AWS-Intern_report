---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6

* Tìm hiểu các nội dung nâng cao về PostgreSQL trên AWS và quy trình di chuyển cơ sở dữ liệu bằng AWS DMS và AWS SCT.
* Tìm hiểu cách xây dựng cơ sở dữ liệu vật lý từ mô hình đã thiết kế.
* Hỗ trợ chuẩn bị dữ liệu và cấu trúc cơ sở dữ liệu để phục vụ quá trình phát triển dự án.
* Tham gia thảo luận, thống nhất công nghệ và phân công công việc cho giai đoạn triển khai.

### Các công việc đã thực hiện

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- |--------------|-----------------| --- |
| 2 | - Học nội dung **Advanced PostgreSQL on AWS**. <br>&emsp;+ Tìm hiểu một số kiến thức nâng cao về PostgreSQL như Connection Pooling, WAL Logs và Memory Tuning. <br>&emsp;+ Tìm hiểu cách sử dụng `EXPLAIN ANALYZE` và các loại Index để cải thiện hiệu năng truy vấn. | 13/07/2026   | 13/07/2026      | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Tìm hiểu cách xây dựng cơ sở dữ liệu trên PostgreSQL. <br>&emsp;+ Thực hành tạo các bảng dữ liệu bằng các câu lệnh SQL như `CREATE TABLE`, `ALTER TABLE` và thiết lập khóa, ràng buộc dữ liệu. <br>&emsp;+ Tìm hiểu cơ chế sao lưu dữ liệu và Snapshot trên Amazon RDS. | 14/07/2026   | 14/07/2026      | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Tìm hiểu quy trình di chuyển cơ sở dữ liệu bằng AWS Schema Conversion Tool (SCT) và AWS Database Migration Service (DMS). <br>&emsp;+ Thực hành chuyển đổi một số cấu trúc dữ liệu mẫu. <br>&emsp;+ Tham gia phác thảo thành phần cơ sở dữ liệu trong kiến trúc tổng thể của hệ thống. | 15/07/2026   | 15/07/2026      | https://cloudjourney.awsstudygroup.com/ |
| 5 | - Tham gia họp nhóm để trao đổi về cấu trúc dữ liệu phục vụ Backend. <br>&emsp;+ Hỗ trợ xác định dữ liệu đầu vào và đầu ra cho một số API của hệ thống. <br>&emsp;+ Chuẩn bị dữ liệu mẫu để hỗ trợ việc kiểm thử trong quá trình phát triển. | 16/07/2026   | 16/07/2026      | Team Discussion |
| 6 | - Tham gia họp nhóm để thống nhất công nghệ sử dụng cho dự án. <br>&emsp;+ Thảo luận về việc sử dụng PostgreSQL, Amazon RDS và Amazon S3 trong hệ thống. <br>&emsp;+ Tiếp nhận các công việc liên quan đến cơ sở dữ liệu để chuẩn bị cho giai đoạn triển khai tiếp theo. | 17/07/2026   | 17/07/2026      | Team Discussion |

### Kết quả đạt được tuần 6

* **Về kiến thức:**
  * Hiểu thêm các kiến thức nâng cao của PostgreSQL, đặc biệt là tối ưu truy vấn và sử dụng chỉ mục để cải thiện hiệu năng.
  * Tìm hiểu quy trình di chuyển cơ sở dữ liệu bằng AWS SCT và AWS DMS, đồng thời hiểu được vai trò của hai dịch vụ này trong quá trình chuyển đổi dữ liệu.
  * Biết thêm về cách xây dựng cơ sở dữ liệu vật lý từ mô hình đã thiết kế và cách tổ chức các câu lệnh SQL để tạo bảng và thiết lập ràng buộc.

* **Về đóng góp cho dự án:**
  * Hỗ trợ xây dựng các câu lệnh SQL để tạo bảng và các ràng buộc dữ liệu dựa trên sơ đồ ERD của hệ thống.
  * Tham gia trao đổi với nhóm Backend về cấu trúc dữ liệu và dữ liệu trao đổi giữa API và cơ sở dữ liệu.
  * Chuẩn bị dữ liệu mẫu phục vụ cho việc kiểm thử và cùng nhóm thống nhất các công nghệ sẽ sử dụng trong giai đoạn phát triển dự án.