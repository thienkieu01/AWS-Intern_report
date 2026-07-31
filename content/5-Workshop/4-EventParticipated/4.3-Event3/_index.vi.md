---
title: "Event 3"
date: 2024-07-25
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Bài thu hoạch "Agentic AI Build Week (AABW) – Demo Day 4 nhóm dự án"

### Mục Đích Của Sự Kiện

- Tổng kết và trình bày thành quả sau chuỗi ngày xây dựng sản phẩm AI Agentic
- Tạo sân chơi để các đội thi thể hiện năng lực ứng dụng AWS AI/ML vào bài toán thực tế
- Kết nối các bạn trẻ với chuyên gia, mentor trong hệ sinh thái AWS
- Lan tỏa tinh thần "Build Week" – học qua thực hành, từ ý tưởng đến sản phẩm hoàn chỉnh trong thời gian giới hạn

### Danh Sách Các Nhóm Trình Bày

- **3KA** – Huỳnh An Khương, Nguyễn Quốc Huy, Ngô Quang Khôi, Hoàng Lê Thành Đức, Đặng Nguyễn Phước Lộc, Đặng Trường Hưng
- **OneTeam** – Anh Duy, Tran Dong, Doan Trung, Minh Viet, Anshul Roy
- **Plan V** – Pham Tien Thuan Phat, Huynh Hoang Long, Le Minh Nghia, Tran Dai Vi, Nguyen An
- **Signal Scout** – Le Tan Luc, Do Hoang Hieu, Trieu Quoc Hao, Nguyen Van Duy Khiem, Nguyen Cong Minh, Nguyen Tran Minh Quan

### Nội Dung Nổi Bật

#### Nhóm 3KA – S.H.E.P.H.E.R.D (Smart Human-flow Evaluation, Prediction, Hazard Detection, Response, and Dispatch)

- Xuất phát từ ý tưởng Capstone project, được prototype hóa ngay trong hackathon để validate sớm
- Giải quyết bài toán giám sát đám đông tại các venue: mật độ, hàng chờ, tình trạng ùn tắc mà con người khó bao quát cùng lúc
- Kiến trúc kết hợp **YOLO + ByteTrack** để nhận diện/theo dõi người, **Amazon SageMaker** để inference, **Amazon Bedrock AgentCore + Strands Agent** cho tầng agentic AI, và **React Monitoring Dashboard** để hiển thị
- Hai lớp tác nhân AI: **Autonomous Monitor** (tự động theo dõi, phát hiện dấu hiệu tắc nghẽn, dự đoán quá tải, tạo cảnh báo chủ động) và **Operator Copilot** (cho phép nhân viên vận hành hỏi bằng ngôn ngữ tự nhiên và nhận câu trả lời dựa trên số liệu thời gian thực)
- Thách thức chính: duy trì luồng video ổn định, giảm độ trễ inference, giữ tracking liên tục giữa các khung hình, kiểm soát chi phí, và làm cho AI agent thực sự chủ động – có thể giải thích được

#### Nhóm OneTeam – KFC Bot Agent (AI-Powered Conversational Ordering)

- Điểm khởi phát ý tưởng: bài học từ việc McDonald's phải dừng thử nghiệm AI order tại hơn 100 cửa hàng ở Mỹ – cho thấy ordering bằng hội thoại là một bài toán hệ thống thực sự, không chỉ là "AI có tốt hay không"
- Vấn đề cốt lõi: người dùng đang chat thì có nhu cầu mua hàng, nhưng phải rời sang app khác → mất momentum, dễ "lost order"
- Giải pháp: agent đặt hàng hội thoại đa kênh (Zalo OA, Messenger, mở rộng thêm kênh mới), không cần tải app, không cần tạo tài khoản mới
- Nguyên lý thiết kế agent theo 5 bước: **Goal → Plan → Tools → Act → Verify** – "model hiểu, nhưng tools mới quyết định điều gì là thật"
- Kiến trúc hướng tới "Design Once, Deploy Everywhere": thêm kênh mới = thêm adapter, thêm nghiệp vụ = thêm connector, thêm năng lực = thêm tool
- Chỉ số ấn tượng: chi phí khoảng **$0.006/đơn hàng**, **~$88/tháng** hạ tầng (Bedrock chiếm ~75%), độ trễ đầu-cuối **3–5 giây**, giảm **60% infra code** nhờ AgentCore

#### Nhóm Plan V – Solution Architect Professional Native App

- Vấn đề: khách hàng yêu cầu thiết kế hệ thống AI cho tài liệu SOP và cần gấp, trong khi Solution Architect phải mất nhiều thời gian cho requirement extraction, vẽ kiến trúc, tạo diagram, ước tính chi phí thủ công
- Giải pháp: xây dựng ứng dụng AI-native hỗ trợ Solution Architect, có khả năng:
  - Phân tích ngôn ngữ tự nhiên và yêu cầu dự án có cấu trúc
  - Đề xuất kiến trúc cấp cao (hybrid-cloud aware), bám chuẩn công ty
  - Tự sinh diagram Draw.io và AWS diagram bằng icon chính thức của AWS
  - Ước tính chi phí AWS định hướng cho khu vực ap-southeast-1
  - Đưa ra khuyến nghị, giả định và các khoảng trống yêu cầu còn thiếu
  - Tinh chỉnh lặp lại qua chat sidebar với custom instruction theo từng dự án
- Workflow: người dùng nhập yêu cầu bằng ngôn ngữ tự nhiên/tài liệu → App Server điều phối giữa Knowledge Base, Amazon Bedrock model, Draw.io MCP, AWS Pricing MCP → xuất ra bản tóm tắt, requirement catalogue, kiến trúc, diagram và ước tính chi phí
- Tác động: từ việc đọc BRD/PRD thủ công, bắt đầu từ trang trắng mỗi lần, tạo IaC tay và đoán chi phí theo kinh nghiệm → chuyển sang "upload + chat" để có Requirements Catalogue trong vài phút, một bản nháp kiến trúc có căn cứ để phản hồi thay vì tạo từ đầu, tự động sinh IaC và ước tính AWS đi kèm

#### Nhóm Signal Scout – Phát hiện tín hiệu thay đổi chiến lược doanh nghiệp

- Sản phẩm giúp thu thập, xác thực bằng chứng công khai và phát hiện sớm các tín hiệu tái cấu trúc, thay đổi chiến lược của doanh nghiệp
- Value Proposition: phát hiện sớm thay đổi chiến lược, kết nối các tín hiệu rời rạc thành một câu chuyện rõ ràng, mọi kết luận đều có bằng chứng đi kèm, hỗ trợ quyết định theo hướng Maintain – Adapt – Accelerate
- Đối tượng phục vụ: đội ngũ chiến lược doanh nghiệp, quản trị rủi ro, competitive intelligence, quản lý tài khoản B2B doanh nghiệp
- Kiến trúc multi-agent trên AWS: **Crawler Subagent** (thu thập dữ liệu qua TinyFish, Apify) và **Analysis Subagent** (phân tích, áp Bedrock Guardrails, ghi log qua Langfuse), giao tiếp theo mô hình **A2A** thông qua AgentCore Runtime Management, cùng các thành phần bảo mật/giám sát chuẩn AWS (WAF, Cognito, CloudWatch, CloudTrail, Secrets Manager, IAM)
- Nhóm còn tối ưu lại kiến trúc theo hướng tiết kiệm chi phí hơn, ước tính tổng chi phí vận hành dao động khoảng **$81–$359/tháng** tùy mức sử dụng
- Bài học đúc kết: "Clear direction beats too many options", "Execution matters more than perfection", "Strong teamwork makes the difference"

### Những Gì Học Được

#### Về Kỹ Thuật

- **Kiến trúc Agentic AI trên AWS**: cách kết hợp Amazon Bedrock, AgentCore Runtime, Strands Agent, AgentCore Gateway/Memory để xây dựng agent có khả năng lập kế hoạch, dùng tool và tự xác minh kết quả
- **Multi-agent orchestration**: mô hình A2A (agent-to-agent) giữa các subagent chuyên biệt (crawler, analysis...) giúp phân tách trách nhiệm rõ ràng
- **Computer vision thời gian thực**: kết hợp object detection/tracking (YOLO, ByteTrack) với cloud inference để giải quyết bài toán vận hành thực tế
- **Multi-channel conversational commerce**: thiết kế hệ thống đặt hàng qua chat không phụ thuộc vào một kênh duy nhất, có thể mở rộng linh hoạt
- **AI-assisted architecture design**: dùng AI để tự động hóa một phần công việc của Solution Architect (requirement extraction, vẽ diagram, ước tính chi phí)

#### Về Tư Duy Sản Phẩm

- Luôn bắt đầu từ **vấn đề thực tế** (pain point) trước khi chọn công nghệ, như bài học từ case McDonald's
- **Kiến trúc là tập hợp các quyết định** giúp sản phẩm có thể mở rộng mà không phải xây lại từ đầu
- Cân bằng giữa **tốc độ xây dựng trong thời gian giới hạn** và **chất lượng, khả năng giải thích** của hệ thống AI
- Chi phí vận hành (cost) là một yếu tố thiết kế quan trọng ngay từ đầu, không phải chỉ tính sau khi sản phẩm đã chạy

#### Về Làm Việc Nhóm

- Vai trò rõ ràng và mục tiêu (goal) rõ ràng ngay từ đầu giúp tránh mất thời gian tranh luận không cần thiết trong lúc chạy nước rút
- Tinh thần "execution matters more than perfection" – một sản phẩm nhỏ nhưng hoàn chỉnh có giá trị hơn một ý tưởng lớn nhưng dang dở
- Việc gặp gỡ, trao đổi với mentor và các đội khác trong sự kiện mang lại giá trị không kém gì bản thân sản phẩm

### Ứng Dụng Vào Công Việc

- **Áp dụng mô hình agentic AI** (Goal → Plan → Tools → Act → Verify) khi thiết kế các tính năng tự động hóa cho hệ thống hiện tại
- **Thử nghiệm AgentCore/Strands Agent** cho các bài toán cần orchestration nhiều bước hoặc nhiều agent chuyên biệt
- **Tham khảo mô hình chi phí** (cost breakdown theo service) để ước tính ngân sách khi đề xuất giải pháp AI mới cho dự án
- **Ứng dụng AI hỗ trợ Solution Architect** vào quy trình làm đề xuất kiến trúc, giảm thời gian soạn tài liệu và ước tính chi phí ban đầu
- **Xây dựng kênh giao tiếp đa nền tảng** (multi-channel) cho các sản phẩm hướng người dùng cuối, tránh làm gián đoạn trải nghiệm khi chuyển kênh

### Trải nghiệm trong event

Được theo dõi phần trình bày của 4 đội thi trong khuôn khổ **Agentic AI Build Week** là một trải nghiệm rất thú vị và truyền cảm hứng, cho thấy AI Agentic không chỉ là khái niệm lý thuyết mà đã có thể ứng dụng vào nhiều lĩnh vực khác nhau chỉ trong thời gian ngắn.

#### Đa dạng bài toán, đa dạng cách tiếp cận

- Bốn đội lựa chọn bốn hướng đi hoàn toàn khác nhau: giám sát an toàn đám đông (3KA), đặt hàng hội thoại đa kênh (OneTeam), hỗ trợ Solution Architect (Plan V), và phát hiện tín hiệu chiến lược doanh nghiệp (Signal Scout) – cho thấy độ linh hoạt của nền tảng AWS AI/ML trong việc giải quyết các bài toán rất khác biệt.
- Mỗi đội đều xuất phát từ một **vấn đề thực tế cụ thể** thay vì chỉ chạy theo công nghệ, giúp phần trình bày có tính thuyết phục cao.

#### Học hỏi về kiến trúc và vận hành thực tế

- Được tiếp cận với các thành phần AWS AI mới như **Amazon Bedrock AgentCore**, **Strands Agent**, **AgentCore Gateway/Memory** thông qua các sơ đồ kiến trúc chi tiết mà các đội trình bày.
- Hiểu rõ hơn cách các đội xử lý những vấn đề vận hành thực tế: độ trễ, chi phí, bảo mật (WAF, Guardrails, IAM), và khả năng mở rộng hệ thống.

#### Cảm hứng từ tinh thần "build" trong thời gian giới hạn

- Nhìn thấy rõ áp lực và sự sáng tạo khi các đội phải hoàn thiện sản phẩm trong thời gian rất ngắn, từ việc chọn kiến trúc tối ưu chi phí đến việc tinh gọn phạm vi (scope) để kịp demo.
- Những chia sẻ thẳng thắn về khó khăn (thiếu nền tảng AI, lần đầu làm việc với AWS, code lỗi, thiếu ngủ...) giúp thấy được bức tranh chân thực đằng sau mỗi sản phẩm hoàn chỉnh.

#### Bài học rút ra

- AI Agentic đang chuyển dịch từ "chatbot trả lời" sang "agent hành động" – có khả năng lập kế hoạch, dùng công cụ, và tự xác minh kết quả trước khi trả lời.
- Việc kết hợp nhiều dịch vụ AWS (Bedrock, AgentCore, SageMaker, Lambda, DynamoDB...) theo một kiến trúc mạch lạc là yếu tố then chốt để đưa một ý tưởng từ hackathon thành sản phẩm có khả năng vận hành thực tế.
- Chi phí và khả năng giải thích (explainability) của AI agent cần được tính đến ngay từ giai đoạn thiết kế, không phải là một bước tối ưu sau cùng.

#### Một số hình ảnh khi tham gia sự kiện

![](/images/4-Event/event3.jpg)

> Tổng thể, sự kiện không chỉ mang đến kiến thức kỹ thuật về AI Agentic trên AWS mà còn cho thấy tinh thần "ý tưởng đi cùng thực thi" – từ một bài toán thực tế, đến kiến trúc hợp lý, và cuối cùng là một sản phẩm demo được trước đông đảo người tham dự.