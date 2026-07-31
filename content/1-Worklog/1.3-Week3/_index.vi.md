---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3

* Tìm hiểu các dịch vụ cơ sở dữ liệu trên AWS như Amazon RDS và Amazon ElastiCache.
* Phân tích cấu trúc dữ liệu và luồng dữ liệu của hệ thống Website Quản lý thư viện.
* Xác định các yêu cầu về dữ liệu để phục vụ cho việc xây dựng tài liệu SRS.
* Chuẩn bị cho giai đoạn thiết kế mô hình cơ sở dữ liệu chi tiết.

### Các công việc đã thực hiện

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- |--------------|-----------------| --- |
| 2 | - Học bài **Database Essentials with Amazon RDS**. <br>&emsp;+ Tìm hiểu Amazon RDS và các hệ quản trị cơ sở dữ liệu như PostgreSQL, MySQL. <br>&emsp;+ Tìm hiểu khái niệm Multi-AZ, Read Replica và trường hợp sử dụng. <br>&emsp;+ Tìm hiểu một số cấu hình cơ bản của RDS như Parameter Group và Storage Auto Scaling. | 22/06/2026   | 22/06/2026      | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Tiếp tục thực hành các nội dung về Amazon RDS. <br>&emsp;+ Tìm hiểu cách tạo và cấu hình một RDS Instance. <br>&emsp;+ Tìm hiểu Amazon ElastiCache (Redis) và vai trò của bộ nhớ đệm trong việc tăng tốc truy vấn. <br>&emsp;+ Tìm hiểu cơ chế sao lưu dữ liệu và khôi phục trên Amazon RDS. | 23/06/2026   | 23/06/2026      | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Tìm hiểu cách lưu trữ hình ảnh và tài liệu bằng Amazon S3. <br>&emsp;+ Nghiên cứu cách lưu đường dẫn của file trong cơ sở dữ liệu thay vì lưu trực tiếp dữ liệu. <br>&emsp;+ Tìm hiểu cách phân quyền truy cập S3 thông qua IAM. | 24/07/2026   | 24/07/2026      | https://cloudjourney.awsstudygroup.com/ |
| 5 | - Tham gia họp nhóm và phân tích dữ liệu của hệ thống Website Quản lý thư viện. <br>&emsp;+ Xác định các thuộc tính của Sách, Độc giả, Phiếu mượn/trả, Tác giả và Thể loại. <br>&emsp;+ Thảo luận về khóa chính, khóa ngoại và các ràng buộc dữ liệu cần có. <br>&emsp;+ Xác định các nhóm người dùng sẽ tương tác với dữ liệu của hệ thống. | 25/06/2026   | 25/06/2026      | Team Discussion |
| 6 | - Tham gia xây dựng phần yêu cầu dữ liệu trong tài liệu SRS. <br>&emsp;+ Đề xuất các yêu cầu về tính toàn vẹn dữ liệu và hiệu năng truy vấn. <br>&emsp;+ Họp nhóm để rà soát lại các bảng dữ liệu và chuẩn bị cho bước thiết kế Use Case Diagram và ERD chi tiết. | 26/06/2026   | 26/06/2026      | Team Discussion |

### Kết quả đạt được tuần 3

* **Về kiến thức:**
  * Hiểu được vai trò của Amazon RDS trong việc xây dựng và quản lý cơ sở dữ liệu quan hệ trên AWS.
  * Nắm được khái niệm về Multi-AZ, Read Replica và biết được khi nào nên sử dụng các tính năng này.
  * Hiểu vai trò của Amazon ElastiCache (Redis) trong việc giảm tải cho cơ sở dữ liệu khi có nhiều truy vấn đọc.
  * Biết cách kết hợp Amazon S3 với cơ sở dữ liệu để lưu trữ hình ảnh và tài liệu của hệ thống.

* **Về đóng góp cho dự án:**
  * Tham gia cùng nhóm phân tích các thực thể dữ liệu và mối quan hệ giữa các bảng trong hệ thống quản lý thư viện.
  * Đóng góp ý kiến về việc thiết kế khóa chính, khóa ngoại và các ràng buộc dữ liệu để đảm bảo tính nhất quán của cơ sở dữ liệu.
  * Hỗ trợ xây dựng phần **Data Requirements** trong tài liệu SRS, làm cơ sở cho việc thiết kế mô hình ERD và cơ sở dữ liệu ở các tuần tiếp theo.