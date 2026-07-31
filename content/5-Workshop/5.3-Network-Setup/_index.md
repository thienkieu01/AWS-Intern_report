---
title : "Network Setup (VPC)"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Overview

In this section, you will build the networking foundation for the library management system on AWS by creating a dedicated **VPC (Virtual Private Cloud)**. The VPC acts as an isolated virtual network, letting you fully control the application's network environment: the IP address range, public/private subnets, and how resources communicate with each other and with the Internet.

Designing the VPC properly is an important foundational step, directly affecting the security, scalability, and performance of the entire system later on (EC2, RDS, S3...).

In this section, you will perform the following in order:

- Create the VPC along with public and private subnets
- Create an Internet Gateway to connect the VPC to the Internet
- Configure route tables to properly route network traffic for each subnet type

#### Content

- [Create VPC and Subnets](5.3.1-create-vpc-and-subnets/)
- [Create Internet Gateway](5.3.2-create-internet-gateway/)
- [Configure Route Tables](5.3.3-configure-route-tables/)