---
title : "Database and Storage"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### Overview

+ In this section, you will deploy the 2 core services for the system's data storage: **Amazon RDS (PostgreSQL)** to store business data (books, users, borrow/return history), and **Amazon S3** to store static files (book cover images, documents uploaded by users).

+ Why separate the two types of storage:
    + **RDS** is suited for structured data that needs relational queries (query, join, transaction) — such as book information, accounts, and borrow/return status.
    + **S3** is suited for file-based data (object storage) — book cover images don't need relational queries, only durable storage and access via URL, independent of the EC2/RDS lifecycle.

+ Both services are placed in the correct security zone set up in the previous section: RDS resides in the **Private Subnet** (no public access, accepting connections only from `library-ec2-sg`), while S3 is a service outside the VPC, accessed by the application through the `library-app-user` Access Key.

#### Content

1. [Create RDS PostgreSQL](5.5.1-create-RDS-PostgreSQL/)
2. [Create S3 Bucket](5.5.2-create-S3-bucket/)