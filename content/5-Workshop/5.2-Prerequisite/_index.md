---
title : "Prerequisites"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Account and Region

In this project, we will deploy in the **N. Virginia (us-east-1)** region.

Make sure the AWS account being used has full access to the following services: VPC, EC2, RDS, S3, IAM, Security Groups, CloudWatch.

#### Tools to Prepare

+ **VS Code** with the **Remote - SSH** extension — used to connect and code directly on EC2 after deployment.
+ **Django application source code** (`library-management`) already pushed to a Git repository, used to clone onto EC2 in the deployment step.
+ **Docker & Docker Compose** — no need to install on your personal machine, will be installed directly on EC2 in a later step.

#### Deployment Order

Unlike workshops that use CloudFormation to provision infrastructure in a single deployment, this project is deployed **manually, step by step through the AWS Console**, in order to clearly understand the role of each service in the architecture:

**VPC → Security Groups → IAM (User) → RDS → S3 → EC2 → Deploy (Docker) → IAM (Role) & CloudWatch**

Specifically, the steps performed:

1. Create a dedicated **VPC** (`library-vpc`, CIDR `10.0.0.0/16`), consisting of a Public Subnet and 2 Private Subnets (placed in 2 different Availability Zones to meet the RDS DB Subnet Group requirement), along with an Internet Gateway and Route Table for each subnet type.
2. Create 2 **Security Groups**: `library-ec2-sg` (opens SSH/HTTP/8000) and `library-rds-sg` (accepts PostgreSQL connections only from `library-ec2-sg`).
3. Create an **IAM User** (`library-app-user`) granted `AmazonS3FullAccess`, using an Access Key so the Django application can write data to S3.
4. Create an **RDS PostgreSQL** instance placed in the Private Subnet, no public access, attached to the `library-rds-sg` Security Group.
5. Create an **S3 Bucket** to store book cover images, configured with a Bucket Policy that allows public read access.
6. Create an **Elastic IP** and associate it with **EC2** (placed in the Public Subnet, attached to `library-ec2-sg`) to have a fixed IP address.
7. SSH into EC2, install **Docker & Docker Compose**, clone the code, configure the `.env` file (RDS + S3 connection), build and run the application.
8. Create an **IAM Role** (`library-ec2-cloudwatch-role`) with the `CloudWatchAgentServerPolicy` policy attached, assign it to EC2, and install the **CloudWatch Agent** to collect logs and monitor resources.