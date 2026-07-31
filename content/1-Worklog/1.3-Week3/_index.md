---
title: "Week 3 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Learn about AWS database services such as Amazon RDS and Amazon ElastiCache.
* Analyze the data structure and data flow of the Library Management Website system.
* Identify the data requirements needed for building the SRS document.
* Prepare for the detailed database model design phase.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- |------------|-----------------| --- |
| 2 | - Study **Database Essentials with Amazon RDS**. <br>&emsp;+ Learn about Amazon RDS and database engines such as PostgreSQL and MySQL. <br>&emsp;+ Learn the concepts of Multi-AZ, Read Replica, and their use cases. <br>&emsp;+ Learn basic RDS configurations such as Parameter Group and Storage Auto Scaling. | 22/06/2026 | 22/06/2026      | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Continue practicing Amazon RDS topics. <br>&emsp;+ Learn how to create and configure an RDS Instance. <br>&emsp;+ Learn about Amazon ElastiCache (Redis) and the role of caching in speeding up queries. <br>&emsp;+ Learn about backup and recovery mechanisms on Amazon RDS. | 23/06/2026 | 23/06/2026      | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Learn how to store images and documents using Amazon S3. <br>&emsp;+ Study how to store file paths in the database instead of storing the data directly. <br>&emsp;+ Learn how to manage S3 access permissions through IAM. | 24/06/2026 | 24/06/2026      | https://cloudjourney.awsstudygroup.com/ |
| 5 | - Join the team meeting to analyze the data of the Library Management Website system. <br>&emsp;+ Identify the attributes of Books, Readers, Borrow/Return Records, Authors, and Categories. <br>&emsp;+ Discuss the primary keys, foreign keys, and required data constraints. <br>&emsp;+ Identify the user groups that will interact with the system's data. | 25/06/2026 | 25/06/2026      | Team Discussion |
| 6 | - Contribute to building the data requirements section of the SRS document. <br>&emsp;+ Propose requirements for data integrity and query performance. <br>&emsp;+ Hold a team meeting to review the data tables and prepare for the detailed Use Case Diagram and ERD design. | 26/06/2026 | 26/06/2026      | Team Discussion |

### Week 3 Achievements:

* **Knowledge gained:**
  * Understood the role of Amazon RDS in building and managing relational databases on AWS.
  * Grasped the concepts of Multi-AZ and Read Replica, and learned when to use these features.
  * Understood the role of Amazon ElastiCache (Redis) in reducing database load under heavy read query traffic.
  * Learned how to combine Amazon S3 with a database to store the system's images and documents.

* **Contribution to the project:**
  * Worked with the team to analyze data entities and the relationships between tables in the library management system.
  * Contributed ideas on designing primary keys, foreign keys, and data constraints to ensure database consistency.
  * Helped build the **Data Requirements** section of the SRS document, forming the foundation for designing the ERD and database model in the following weeks.