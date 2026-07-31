---
title : "Monitoring with CloudWatch"
date : 2024-01-01
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

#### Overview

+ Once the application is running stably on EC2, the next step is **monitoring** — to know how the system is doing, whether CPU/RAM is overloaded, and whether the application has any error logs — instead of manually SSHing in to check each time.

+ **Amazon CloudWatch** allows collecting both types of data:
    + **Metrics**: system indicators such as CPU, memory, and disk.
    + **Logs**: application logs (e.g., Docker container logs), helping to look up errors without logging into EC2.

+ For EC2 to send data to CloudWatch, 2 things are needed:
    + **IAM Role**: grants EC2 permission to call the CloudWatch API to send logs/metrics.
    + **CloudWatch Agent**: software installed on EC2 that runs in the background, collecting and sending data to CloudWatch according to its defined configuration.

#### Content

1. [Create IAM Role for CloudWatch](5.7.1-create-IAM-role-for-EC2/)
2. [Install CloudWatch Agent](5.7.2-Install-CLoudWatch-agent/)