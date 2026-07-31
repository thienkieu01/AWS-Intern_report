---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# Library Management System
## AWS Cloud Solution for the Library Management System

### 1. Executive Summary

The Library Management System is designed to digitize the entire process of managing books, library members, and book borrowing and returning activities. The system supports three primary user groups: **Administrator**, **Librarian**, and **Reader**, helping improve management efficiency while minimizing manual operations.

The solution is deployed on the AWS Cloud using a Multi-tier Architecture, leveraging services such as Amazon EC2, Amazon RDS, Amazon S3, Application Load Balancer, Amazon CloudWatch, and AWS Backup to ensure high performance, scalability, high availability, and data security.

### 2. Problem Statement

#### *Current Challenges*

Many libraries still manage books and borrowing activities using on-premises systems or manual processes. This results in several limitations:

- Difficulty managing a large number of books and library members.
- High risk of data loss when the server encounters failures.
- Limited scalability as the number of users increases.
- Data backup and recovery are primarily performed manually.
- Lack of monitoring and alerting mechanisms when system failures occur.

#### *Proposed Solution*

The system is deployed on AWS Cloud using a multi-tier web application architecture.

Users access the system through an Application Load Balancer. The application is hosted on Amazon EC2, where all library management business logic is processed. Amazon RDS for MySQL stores the system data, while Amazon S3 stores book cover images, documents, and other uploaded files. Amazon CloudWatch monitors system resources, and AWS Backup ensures that data is backed up regularly.

The system supports the following functionalities:

- User Account Management
- Book and Category Management
- Author and Publisher Management
- Book Borrowing and Returning Management
- Fine Management
- Statistics and Reporting

#### *Benefits and Return on Investment (ROI)*

The solution significantly reduces manual management effort, improves data accuracy, and enhances the user experience. Deploying the system on AWS enables seamless scalability as the number of books or users grows without requiring architectural changes.

In addition, automated backup and monitoring services reduce operational costs, improve system reliability, and minimize recovery time in the event of failures.

### 3. Solution Architecture

The system is deployed using a multi-tier web application architecture on the AWS Cloud platform.

Users access the application through the Internet and an Application Load Balancer. Incoming requests are forwarded to Amazon EC2 instances where business logic is processed. System data is stored in Amazon RDS for MySQL, while book images and uploaded files are stored in Amazon S3. Amazon CloudWatch monitors system performance, and AWS Backup performs scheduled data backups.

![Library Management System AWS Architecture](/images/2-Proposal/library_management_aws_architecture.jpg)

### *AWS Services Used*

- **Amazon EC2:** Hosts the Library Management System application.
- **Application Load Balancer:** Distributes incoming traffic to the application servers.
- **Amazon RDS (MySQL):** Stores the system database.
- **Amazon S3:** Stores book cover images and supporting documents.
- **Amazon CloudWatch:** Monitors performance, logs, and system alerts.
- **AWS Backup:** Performs scheduled backups of Amazon RDS and Amazon S3.
- **AWS IAM:** Manages user identities and access permissions.
- **AWS Secrets Manager:** Securely stores database credentials.
- **GitHub Actions:** Automates application deployment to Amazon EC2.

### *Component Design*

- **Users:** Administrators, Librarians, and Readers access the system through a web browser.
- **Application Layer:** Amazon EC2 processes business operations such as authentication, book management, borrowing and returning management, and reporting.
- **Database Layer:** Amazon RDS stores all system data.
- **Storage Layer:** Amazon S3 stores book images and uploaded files.
- **Monitoring Layer:** Amazon CloudWatch collects logs, monitors system resources, and sends alerts when issues occur.
- **Backup Layer:** AWS Backup performs automated backups to ensure data recovery capability.

### 4. Technical Implementation

#### *Implementation Phases*

1. **Requirements Analysis and System Design:** Develop the Use Case Diagram, ERD, and AWS architecture.
2. **AWS Infrastructure Design:** Deploy the VPC, EC2, RDS, S3, IAM, and Security Groups.
3. **Application Development and Deployment:** Develop the backend and frontend, and deploy using GitHub Actions.
4. **Testing and Production Deployment:** Perform functional, performance, and security testing before deploying the production system.

#### *Technical Requirements*

- **Backend:** Spring Boot (or the technology currently used).
- **Frontend:** ReactJS/Thymeleaf (depending on the project).
- **Database:** MySQL on Amazon RDS.
- **Storage:** Amazon S3.
- **Operating System:** Amazon Linux 2023 or Ubuntu Server.
- **Deployment:** GitHub Actions integrated with Amazon EC2.

### 5. Project Roadmap & Milestones

- **Preparation Phase:** Requirements analysis and database design.
- **Development Phase:** Implement application features and deploy the AWS infrastructure.
- **Testing Phase:** Conduct functional and performance testing.
- **Deployment Phase:** Deploy the system to production and monitor it using Amazon CloudWatch.

### 6. Budget Estimation

#### *Infrastructure Costs*

- Amazon EC2 t3.micro
- Amazon RDS MySQL db.t3.micro
- Amazon S3 Standard
- Amazon CloudWatch
- AWS Backup
- Data Transfer

**Estimated total cost:** approximately **USD 25–35 per month**, depending on traffic volume and data storage requirements.

For educational environments such as the **AWS Academy Learner Lab**, these services can typically be deployed without incurring actual costs within the lab's allocated resources.

### 7. Risk Assessment

#### *Risk Matrix*

- EC2 instance failure.
- Database overload.
- Data loss caused by system failures.
- Unauthorized access.

#### *Mitigation Strategies*

- Perform automated backups using AWS Backup.
- Apply the Principle of Least Privilege through AWS IAM.
- Monitor the system using Amazon CloudWatch.
- Protect infrastructure using Security Groups and AWS Secrets Manager.

#### *Contingency Plan*

- Restore data from AWS Backup.
- Rebuild the infrastructure using Infrastructure as Code (CloudFormation or Terraform, if applicable).
- Replace the EC2 instance in the event of a critical failure.

### 8. Expected Outcomes

#### *Technical Improvements*

The system automates library management processes, reduces manual operations, and improves overall management efficiency. The AWS architecture provides scalability, high performance, and high availability.

#### *Long-term Value*

The solution establishes a reliable deployment platform for the Library Management System while allowing future expansion with features such as automated notifications, intelligent search, advanced analytics, and artificial intelligence integration.