---
title: "Event 2"
date: 2026-06-20
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---
# Event Report: "Cloud Architect"

### Mục Đích Của Sự Kiện

- Mang lại sân chơi công nghệ mới mẻ dưới hình thức thi đấu trắc nghiệm kịch tính, giúp gắn kết các thành viên và duy trì tinh thần chủ động học hỏi.
- Hệ thống hóa các kiến thức cốt lõi về thiết kế kiến trúc hệ thống trên nền tảng AWS thông qua các câu hỏi tình huống thực tế.
- Rèn luyện tư duy quản trị rủi ro, khả năng đưa ra quyết định nhanh chóng dưới áp lực thời gian và nâng cao kỹ năng phối hợp đồng đội cho các đội thi.
- Tạo cơ hội giao lưu, kết nối giữa các nhóm thực tập và cộng đồng sinh viên đam mê Cloud.

### Danh Sách 8 Đội Thi Đấu Tham Gia

- **NGŨ ĐẠI HIỆP**
- **KTLT**
- **PrimeOps**
- **YoungFlame IT**
- **LOSERR**
- **GẶP PHẢI THẰNG LIỀU**
- **LIFE LONG LEARNER**
- **KLKAT**

### Nội Dung Nổi Bật

#### An ninh, Tuân thủ & Quản trị vận hành (Security, Compliance & Operations)

- **AWS Artifact:** Tra cứu các chứng chỉ tuân thủ quốc tế (ISO, PCI, SOC) phục vụ kiểm toán.
- **AWS WAF:** Cấu hình Rate-based Rule để ngăn chặn các cuộc tấn công Layer 7 và lượng truy cập bất thường mà vẫn đảm bảo trải nghiệm người dùng.
- **Amazon S3 Bucket Policy:** Quản lý quyền truy cập đối với dữ liệu lưu trữ tĩnh.
- **AWS Systems Manager Patch Manager:** Tự động hóa quy trình vá lỗi bằng Patch Groups và Patch Baselines thông qua EC2 Tags nhằm giảm chi phí vận hành.

#### AWS Well-Architected Framework

- Tìm hiểu các trụ cột trong **AWS Well-Architected Framework**.
- Tập trung vào **Performance Efficiency**, lựa chọn đúng loại tài nguyên và quy mô tài nguyên phù hợp với nhu cầu của hệ thống.

#### Cơ sở dữ liệu & Xử lý sự kiện (Database & Event Handling)

- **Amazon DynamoDB:** Lựa chọn phù hợp cho các ứng dụng mobile có lưu lượng truy cập lớn nhờ khả năng auto scaling và độ trễ thấp.
- **DynamoDB Streams + AWS Lambda:** Tự động kích hoạt xử lý khi dữ liệu thay đổi.
- Phân biệt vai trò của **DynamoDB Streams** và **DAX Cluster** trong từng bài toán thực tế.

#### Hạ tầng Cloud, Hybrid Architecture & Auto Scaling

- **AWS Storage Gateway (File Gateway):** Thiết kế Hybrid Cloud kết nối hệ thống On-Premises với AWS thông qua giao thức SMB.
- **Amazon S3 Lifecycle Rules:** Tự động chuyển dữ liệu sao lưu sang Amazon S3 Glacier để lưu trữ dài hạn và tối ưu chi phí.
- **AWS Pricing Calculator:** Ước tính chi phí triển khai hạ tầng Cloud trước khi thực hiện.
- **Amazon EC2 Auto Scaling:** Tự động mở rộng hoặc thu hẹp tài nguyên dựa trên lưu lượng truy cập.
- **Application Load Balancer (ALB):** Điều hướng lưu lượng bằng Path-based Routing và Host-based Routing.

#### Yếu tố chiến thuật trong cuộc thi

- **Rủi ro tối thiểu:** Chiến thuật lựa chọn đáp án an toàn nhằm hạn chế mất điểm khi chưa chắc chắn.
- **Ngôi sao hy vọng:** Lựa chọn thời điểm sử dụng thẻ nhân đôi điểm số để tạo lợi thế trong các câu hỏi quyết định.

### Những Gì Học Được

#### Tư Duy Thiết Kế

- **Risk Management & Trade-offs:** Biết đánh giá rủi ro và cân bằng giữa chi phí, hiệu năng và bảo mật khi thiết kế hệ thống.
- **System Modernization & Automation:** Hiểu cách kết hợp Serverless, Hybrid Storage và các công cụ quản trị tự động để tối ưu vận hành.

#### Kiến Trúc Kỹ Thuật

- Phân biệt rõ phạm vi sử dụng của các dịch vụ AWS như **WAF và NACL**, **DynamoDB Streams và DAX**, **ALB và NLB**, **Systems Manager và Custom Scripts**.
- Hiểu và vận dụng các nguyên tắc trong **AWS Well-Architected Framework** khi thiết kế hệ thống thực tế.

### Trải nghiệm trong event

Tham gia gameshow **“Cloud Architect”** với vai trò khán giả là một trải nghiệm thú vị, giúp tôi tiếp cận kiến thức AWS theo hình thức trực quan và sinh động hơn. Một số trải nghiệm nổi bật gồm:

#### Học hỏi qua các câu hỏi tình huống thực tế

- Các câu hỏi được xây dựng sát với những bài toán thường gặp trong doanh nghiệp, giúp tôi tự đánh giá mức độ hiểu biết của bản thân.
- Phần giải thích đáp án từ Ban Tổ chức giúp tôi hiểu rõ vì sao mỗi dịch vụ AWS lại phù hợp với từng tình huống cụ thể.

#### Không khí thi đấu sôi nổi

- Quan sát quá trình thảo luận và đưa ra quyết định của các đội thi giúp tôi hiểu rõ hơn cách phân tích yêu cầu và lựa chọn giải pháp phù hợp dưới áp lực thời gian.
- Sự cạnh tranh giữa tám đội thi tạo nên bầu không khí sôi động và truyền thêm động lực học tập.
- Các chiến thuật như **"Ngôi sao hy vọng"** và **"Rủi ro tối thiểu"** cho thấy tầm quan trọng của việc quản trị rủi ro và đưa ra quyết định đúng thời điểm.

#### Giao lưu và kết nối

- Sự kiện tạo cơ hội trao đổi với các bạn học viên có cùng đam mê về AWS và Cloud Computing.
- Qua các cuộc trao đổi, tôi học hỏi thêm nhiều kinh nghiệm học tập cũng như cách tiếp cận các bài toán kiến trúc Cloud.

#### Bài học rút ra

- Các câu hỏi tình huống giúp tôi củng cố kiến thức AWS một cách trực quan và dễ ghi nhớ hơn.
- Khi thiết kế hệ thống, cần cân nhắc đồng thời các yếu tố về chi phí, hiệu năng, bảo mật và khả năng mở rộng trước khi lựa chọn dịch vụ.
- Việc phân tích kỹ yêu cầu bài toán và hiểu rõ đặc điểm của từng dịch vụ AWS sẽ giúp đưa ra quyết định chính xác hơn trong các tình huống thực tế.

#### Một số hình ảnh khi tham gia sự kiện

![](/images/4-Event/event2.jpg)

> Tổng thể, gameshow **Cloud Architect** không chỉ giúp tôi ôn tập và củng cố kiến thức về các dịch vụ AWS mà còn rèn luyện tư duy phân tích, khả năng đánh giá nhiều phương án kiến trúc và cách đưa ra quyết định trong những tình huống thực tế. Đây là một trải nghiệm học tập bổ ích, tạo thêm động lực để tôi tiếp tục nghiên cứu và phát triển kỹ năng trong lĩnh vực Cloud Computing.