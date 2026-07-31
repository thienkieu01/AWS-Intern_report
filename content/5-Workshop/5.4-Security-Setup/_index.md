---
title : "Security Setup"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Overview

+ In this section, you will set up the security layer for the system: creating an **IAM User** so the application can safely interact with S3, and creating **Security Groups** to control traffic in and out between EC2 and RDS.

+ Why a dedicated **IAM User** is needed for the application:
    + Instead of using the root account key (which has full privileges and is very dangerous if leaked), the application should use a separate IAM User granted only the exact permissions it needs (e.g., only S3 access) — following the **least privilege** principle.

+ Why separate **Security Groups** are needed for EC2 and RDS:
    + A Security Group acts as a virtual firewall at the instance level, controlling inbound/outbound traffic based on specific rules.
    + Instead of opening all traffic, the system only allows: EC2 to receive traffic from the Internet on the necessary ports (SSH, HTTP, 8000), while RDS **only accepts connections from EC2's Security Group** — not exposed to the Internet, minimizing the attack surface.

#### Content

1. [Create IAM User](5.4.1-create-iam-user/)
2. [Create Security Groups](5.4.2-create-security-groups/)