---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Deploying a Secure Library Management System on AWS

#### Overview

The **Library Management System** is a web application built on **Django**, deployed on **AWS** infrastructure to ensure security, scalability, and ease of operation.

In this workshop, we will learn how to build a complete AWS infrastructure for a web application — from setting up a private network (VPC) and configuring security (Security Groups, IAM), to deploying the database, storage, application, and system monitoring.

The system uses the following core AWS services, each playing a distinct role in the architecture:
+ **Amazon VPC** - Sets up a private network infrastructure, separating the Public Subnet (hosting the application) from the Private Subnet (hosting the database) to increase security.
+ **Security Groups** - Control traffic at the network layer, restricting EC2 to open only the necessary ports and allowing RDS to accept connections only from the correct source.
+ **AWS IAM** - Manages users and access permissions, allowing the application to interact with S3 and EC2 to send logs to CloudWatch without manually storing keys.
+ **Amazon RDS (PostgreSQL)** - Stores all of the system's business data, placed in a Private Subnet so it cannot be accessed directly from the Internet.
+ **Amazon S3** - Stores book cover images and documents uploaded by users.
+ **Amazon EC2** - Runs the Django application in a Docker environment, handling all of the system's business logic.
+ **Amazon CloudWatch** - Collects logs and monitors the resources and operational status of the system.

#### Content

1. [Introduction](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequisite/)
3. [Network Setup (VPC)](5.3-Network-Setup/)
4. [Security Setup (Security Groups & IAM)](5.4-Security-Setup/)
5. [Database and Storage Deployment (RDS & S3)](5.5-Database-and-storage/)
6. [Application Deployment on EC2](5.6-Application-deployment/)
7. [System Monitoring (CloudWatch)](5.7-Monitoring/)
8. [Resource Cleanup](5.8-Cleanup/)