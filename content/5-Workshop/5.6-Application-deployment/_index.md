---
title : "Application Deployment on EC2"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### Overview

+ In this section, you will deploy the Django application onto **Amazon EC2** — where authentication, book management, and the system's business logic are actually handled. EC2 is placed in the Public Subnet set up in section 5.3, and connects to RDS and S3 through the Security Group and IAM configured in previous sections.

+ The application is packaged and run using **Docker**, providing a consistent runtime environment, easy deployment, and no dependence on manually installing individual software packages on EC2.

+ Why an **Elastic IP** is needed for EC2:
    + By default, EC2's public IP address **changes** each time the instance is stopped/started. An Elastic IP is a static IP address that stays the same even after the instance restarts — avoiding the need to update configuration (`ALLOWED_HOSTS`, DNS...) each time.

#### Content

1. [Launch EC2 and Attach an Elastic IP](5.6.1-Launch-EC2-and-attach-Elastic-IP/)
2. [Install Docker, Clone the Code](5.6.2-Install-Docker-clone-code/)
3. [Build and Run the Application](5.6.3-Build-and-run-the-application/)