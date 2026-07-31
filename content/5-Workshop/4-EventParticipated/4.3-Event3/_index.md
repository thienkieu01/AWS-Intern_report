---
title: "Event 3"
date: 2024-07-25
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Event Report: "Agentic AI Build Week (AABW) – Demo Day"

## Event Objectives

- Showcase the achievements of project teams after an intensive AI Agent development week.
- Provide a platform for teams to demonstrate how AWS AI/ML technologies can solve real-world problems.
- Connect students with AWS experts, mentors, and industry professionals.
- Promote the "Build Week" spirit of learning through hands-on experience, transforming ideas into working products within a limited timeframe.

## Project Teams

- **3KA** – Huỳnh An Khương, Nguyễn Quốc Huy, Ngô Quang Khôi, Hoàng Lê Thành Đức, Đặng Nguyễn Phước Lộc, Đặng Trường Hưng
- **OneTeam** – Anh Duy, Tran Dong, Doan Trung, Minh Viet, Anshul Roy
- **Plan V** – Pham Tien Thuan Phat, Huynh Hoang Long, Le Minh Nghia, Tran Dai Vi, Nguyen An
- **Signal Scout** – Le Tan Luc, Do Hoang Hieu, Trieu Quoc Hao, Nguyen Van Duy Khiem, Nguyen Cong Minh, Nguyen Tran Minh Quan

## Key Highlights

### Team 3KA – S.H.E.P.H.E.R.D (Smart Human-flow Evaluation, Prediction, Hazard Detection, Response, and Dispatch)

- Originated from a Capstone Project and was rapidly prototyped during the hackathon for early validation.
- Addressed crowd monitoring challenges in public venues, including crowd density, queue management, and congestion detection.
- Built using **YOLO + ByteTrack** for people detection and tracking, **Amazon SageMaker** for model inference, **Amazon Bedrock AgentCore + Strands Agent** for the agentic AI layer, and a **React Monitoring Dashboard** for visualization.
- Implemented two AI agents:
  - **Autonomous Monitor:** Automatically detects congestion, predicts overcrowding, and generates proactive alerts.
  - **Operator Copilot:** Allows operators to ask questions in natural language and receive responses based on real-time data.
- Major technical challenges included maintaining stable video streaming, reducing inference latency, ensuring continuous object tracking, controlling infrastructure costs, and building explainable AI agents.

### Team OneTeam – KFC Bot Agent (AI-Powered Conversational Ordering)

- Inspired by McDonald's experience of suspending AI ordering trials in over 100 U.S. stores, highlighting that conversational ordering is a system design challenge rather than simply an AI problem.
- Solved the issue of customers leaving conversations to place orders through separate applications.
- Proposed a multi-channel conversational ordering agent supporting **Zalo OA**, **Facebook Messenger**, and future communication channels without requiring additional applications or accounts.
- Designed following the five-step agent workflow:
  **Goal → Plan → Tools → Act → Verify**, emphasizing that while language models provide understanding, tools determine factual execution.
- Followed a **Design Once, Deploy Everywhere** architecture where new channels, business functions, or capabilities can be added independently.
- Achieved impressive metrics:
  - Approximately **$0.006 per order**
  - Around **$88/month** infrastructure cost (approximately 75% from Amazon Bedrock)
  - **3–5 seconds** end-to-end latency
  - Reduced **60% of infrastructure code** using AgentCore.

### Team Plan V – Solution Architect Professional Native App

- Addressed the challenge faced by Solution Architects who spend significant time extracting requirements, designing architectures, drawing diagrams, and estimating AWS costs manually.
- Developed an AI-native assistant capable of:
  - Extracting structured project requirements from natural language.
  - Recommending enterprise-standard, hybrid-cloud-aware architectures.
  - Automatically generating Draw.io diagrams and official AWS architecture diagrams.
  - Estimating AWS costs for the **ap-southeast-1** region.
  - Identifying missing requirements and providing architectural recommendations.
  - Supporting iterative refinement through an interactive chat interface.
- Workflow:
  Users upload documents or describe requirements → Application Server coordinates the Knowledge Base, Amazon Bedrock, Draw.io MCP, and AWS Pricing MCP → Generates requirement catalogs, architecture proposals, diagrams, and cost estimates.
- Reduced the architecture design process from manually starting with a blank document to generating a complete architectural draft within minutes.

### Team Signal Scout – Enterprise Strategy Signal Detection

- Built an AI platform for collecting and validating publicly available information to detect early signals of organizational restructuring and strategic business changes.
- Value proposition:
  - Early identification of strategic changes.
  - Connecting fragmented signals into meaningful business insights.
  - Providing evidence-supported conclusions.
  - Supporting strategic decisions through **Maintain – Adapt – Accelerate** recommendations.
- Target users included enterprise strategy teams, risk management departments, competitive intelligence analysts, and B2B account managers.
- Implemented a multi-agent AWS architecture:
  - **Crawler Subagent:** Data collection using TinyFish and Apify.
  - **Analysis Subagent:** AI analysis with Amazon Bedrock Guardrails and Langfuse logging.
  - Communication followed the **Agent-to-Agent (A2A)** model through AgentCore Runtime Management.
  - Security and monitoring utilized AWS WAF, Amazon Cognito, CloudWatch, CloudTrail, Secrets Manager, and IAM.
- Optimized the architecture to reduce operational costs, with estimated monthly expenses ranging from **$81 to $359** depending on workload.
- Key lessons:
  - "Clear direction beats too many options."
  - "Execution matters more than perfection."
  - "Strong teamwork makes the difference."

## Knowledge Gained

### Technical Knowledge

- **Agentic AI Architecture on AWS:** Learned how Amazon Bedrock, AgentCore Runtime, Strands Agent, AgentCore Gateway, and AgentCore Memory work together to build autonomous AI agents capable of planning, tool usage, and self-verification.
- **Multi-Agent Orchestration:** Understood the Agent-to-Agent (A2A) collaboration model among specialized agents responsible for different tasks.
- **Real-Time Computer Vision:** Learned how object detection and tracking technologies such as YOLO and ByteTrack can be integrated with cloud inference services for operational monitoring.
- **Multi-Channel Conversational Commerce:** Explored scalable chatbot architectures that support multiple communication platforms.
- **AI-Assisted Solution Architecture:** Understood how AI can automate requirement analysis, architecture generation, diagram creation, and cloud cost estimation.

### Product Thinking

- Always begin with a **real business problem** rather than selecting technologies first, as demonstrated by the McDonald's ordering case study.
- Recognized that **software architecture is a collection of design decisions** that enable future scalability.
- Learned to balance rapid development within limited timeframes against system quality and AI explainability.
- Understood that operational cost should be considered from the earliest stages of system design.

### Teamwork

- Clearly defined roles and objectives help teams avoid unnecessary discussions during intensive development periods.
- Embraced the principle that **execution matters more than perfection**—a smaller but complete product delivers greater value than an unfinished ambitious idea.
- Discussions with mentors and other participating teams provided valuable learning experiences beyond the projects themselves.

## Applying the Knowledge

- Apply the **Goal → Plan → Tools → Act → Verify** agentic workflow when designing intelligent automation features.
- Experiment with **AgentCore** and **Strands Agent** for multi-step orchestration and specialized AI agents.
- Reference real-world infrastructure cost breakdowns when estimating budgets for future AI projects.
- Utilize AI-assisted architecture design to accelerate documentation, architecture proposals, and cloud cost estimation.
- Develop **multi-channel communication platforms** that provide seamless user experiences across different messaging services.

## Event Experience

Watching the four project demonstrations during **Agentic AI Build Week** was both inspiring and educational. The event clearly demonstrated that Agentic AI has evolved beyond theoretical concepts into practical solutions capable of solving diverse real-world problems within a short development period.

### Diverse Problems, Diverse Solutions

- Each team focused on a completely different application:
  - Crowd safety monitoring (3KA)
  - Multi-channel conversational ordering (OneTeam)
  - AI assistant for Solution Architects (Plan V)
  - Enterprise strategy signal detection (Signal Scout)
- Every project originated from a genuine business problem instead of simply showcasing AI technologies.

### Learning Modern AI Architectures

- Gained exposure to modern AWS AI services, including **Amazon Bedrock AgentCore**, **Strands Agent**, **AgentCore Gateway**, and **AgentCore Memory** through detailed architecture presentations.
- Better understood how teams addressed real-world engineering concerns such as latency, infrastructure cost, security (AWS WAF, Guardrails, IAM), and scalability.

### Inspiration from the Build Week Spirit

- Witnessed how teams balanced creativity and engineering under tight deadlines while continuously refining architectures and limiting project scope to deliver complete demonstrations.
- Honest discussions about challenges—including limited AI experience, learning AWS from scratch, debugging issues, and long development hours—revealed the real effort behind successful products.

### Lessons Learned

- Agentic AI is evolving from traditional chatbots into autonomous agents capable of planning, using tools, and verifying results before responding.
- Combining multiple AWS services such as Amazon Bedrock, AgentCore, SageMaker, Lambda, and DynamoDB within a well-designed architecture is essential for transforming hackathon ideas into deployable solutions.
- Cost optimization and AI explainability should be considered fundamental design requirements rather than post-development improvements.

### Event Photos

![](/images/4-Event/event3.jpg)

> Overall, the event provided not only valuable technical knowledge about Agentic AI on AWS but also demonstrated the importance of transforming ideas into practical solutions through thoughtful architecture and effective execution. It was an inspiring experience that strengthened my understanding of modern AI engineering while motivating me to continue exploring Agentic AI and AWS technologies.