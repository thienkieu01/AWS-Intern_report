---
title : "Introduction"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 1. </b> "
---

#### Project introduction

+ The Library Management System is a web application built on the **Django** framework, allowing management of books, users (Administrator, Librarian, Reader), and borrowing/returning operations through a Web browser.
+ The application is deployed entirely on **AWS** infrastructure, leveraging cloud computing services to ensure security, scalability, and ease of operation, instead of deploying on traditional physical servers.

#### System overview

In this project, the system is built on the following core AWS services:

+ **Amazon VPC**: sets up a dedicated network infrastructure (`library-vpc`), consisting of a **Public Subnet** (hosting the EC2 instance running the application) and a **Private Subnet** (hosting RDS, isolated from the Internet to ensure data security).
+ **AWS IAM**: manages users and access permissions — including an **IAM User** (`library-app-user`) granting the application permission to write data to S3, and an **IAM Role** attached to EC2 to send logs to CloudWatch without storing access keys.
+ **Security Groups**: control traffic at the network layer, restricting EC2 to open only the necessary ports (SSH, HTTP, 8000) and allowing RDS to accept connections only from the EC2 Security Group.
+ **Amazon RDS (PostgreSQL)**: stores all business data of the system (books, users, borrowing/returning history), placed in the Private Subnet, not directly accessible from the Internet.
+ **Amazon S3**: stores book cover images and document files uploaded by users.
+ **Amazon EC2**: runs the Django application inside a **Docker** environment, handling authentication, book management, and other system operations.
+ **Amazon CloudWatch**: collects logs, monitors resources, and tracks the operational status of EC2 throughout the system's runtime.

The entire deployment process follows this order: **VPC → IAM → Security Groups → RDS → S3 → EC2 → Deploy → CloudWatch**, ensuring the network and security infrastructure is fully established before deploying the application and configuring monitoring.

![overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.jpg)