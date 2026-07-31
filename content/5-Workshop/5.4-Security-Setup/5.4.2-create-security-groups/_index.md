---
title : "Create Security Groups"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

A Security Group acts as a virtual firewall at the instance level, controlling inbound/outbound traffic. In this section, you will create 2 Security Groups: one for EC2 (opening the ports needed to access the application), and one for RDS (accepting connections only from EC2, not exposed to the Internet).

#### Step 1: Create the Security Group for EC2

1. Go to **EC2 Console** → **Security Groups** → click **Create security group**.
2. In the **Basic details** section, configure:
   - **Security group name**: `library-ec2-sg`
   - **Description**: `SG for EC2 - web server`
   - **VPC**: select `vpc-0686bd0330b6b622f (library-vpc)`
3. In the **Inbound rules** section, add 3 rules:

| Type | Protocol | Port range | Source |
|---|---|---|---|
| SSH | TCP | 22 | My IP |
| HTTP | TCP | 80 | Anywhere-IPv4 (0.0.0.0/0) |
| Custom TCP | TCP | 8000 | Anywhere-IPv4 (0.0.0.0/0) |

4. Keep the default **Outbound rules** (All traffic).
5. Scroll to the bottom, click **Create security group**.

![create-ec2-sg](/images/5-Workshop/5.4-Security-Setup/5.4.2-create-security-groups/create-ec2-sg.png)

#### Step 2: Create the Security Group for RDS

6. Still in **Security Groups**, click **Create security group**.
7. In the **Basic details** section, configure:
   - **Security group name**: `library-rds-sg`
   - **Description**: `SG for RDS - database`
   - **VPC**: select `vpc-0686bd0330b6b622f (library-vpc)` (same as before)

![basic-details-rds-sg](/images/5-Workshop/5.4-Security-Setup/5.4.2-create-security-groups/basic-details-rds-sg.png)

8. In the **Inbound rules** section, add 1 rule:
   - **Type**: PostgreSQL
   - **Protocol/Port**: TCP / 5432 (auto-filled)
   - **Source**: select **Custom**, type in the search box and select the **`library-ec2-sg`** Security Group (not an IP address)
9. Click **Create security group**.

![inbound-rule-rds-sg](/images/5-Workshop/5.4-Security-Setup/5.4.2-create-security-groups/inbound-rule-rds-sg.png)