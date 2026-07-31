---
title : "Launch EC2 and Attach an Elastic IP"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.6.1 </b> "
---

EC2 is where the Django application runs in a Docker environment, placed in the Public Subnet created in section 5.3, attached to the `library-ec2-sg` Security Group created in section 5.4.

#### Step 1: Name the Instance and Choose an AMI

1. Go to **EC2 Console** → **Instances** → click **Launch an instance**.
2. In **Name and tags**, enter **Name**: `Library Management System`.
3. In **Application and OS Images (AMI)**, select **Ubuntu** (Ubuntu Server 26.04 LTS).

![name-and-ami](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/name-and-ami.png)

#### Step 2: Create a Key Pair

4. In **Key pair (login)**, click **Create new key pair**.

![create-key-pair-button](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/create-key-pair-button.png)

5. Enter:
   - **Key pair name**: `library-key`
   - **Key pair type**: RSA
   - **Private key file format**: .pem
6. Click **Create key pair** — the `.pem` file will download automatically.

![create-key-pair-form](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/create-key-pair-form.png)

{{% notice warning %}}
The `.pem` file can only be downloaded **once**. Save this file carefully — it will be needed to SSH into EC2 in a later step.
{{% /notice %}}

#### Step 3: Choose the Instance Type

7. Scroll down to **Instance type**, select `t3.small` (2 vCPU, 2 GiB Memory).

![select-instance-type](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/select-instance-type.png)

{{% notice note %}}
AWS suggests `t3.micro` (1 GiB RAM) by default, but in practice, when running Docker + CloudWatch Agent + SSH simultaneously, `t3.micro` easily runs out of RAM, causing connection loss errors. It's better to choose `t3.small` (2 GiB RAM) directly from the start to avoid having to change the instance type later on.
{{% /notice %}}

#### Step 4: Configure Network Settings

8. Scroll down to **Network settings**, click **Edit**, configure:
   - **VPC**: select `library-vpc (vpc-0686bd0330b6b622f)`
   - **Subnet**: select `public-subnet`
   - **Auto-assign public IP**: **Enable**
   - **Firewall (security groups)**: select **Select existing security group** → select `library-ec2-sg`

![network-settings](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/network-settings.png)

#### Step 5: Launch the Instance

9. Review the **Summary** (instance type `t3.small`, 8 GiB storage), click **Launch instance**.

---

#### Step 6: Create an Elastic IP

10. Go to **EC2 Console** → **Network & Security** → **Elastic IPs** → click **Allocate Elastic IP address**.

![elastic-ip-list](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/elastic-ip-list.png)

11. Keep the default (**Amazon's pool of IPv4 addresses**), click **Allocate**.

![allocate-elastic-ip](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/allocate-elastic-ip.png)

#### Step 7: Associate the Elastic IP with EC2

12. Once created successfully, select the IP address you just created, click **Actions** → **Associate Elastic IP address**.

![associate-elastic-ip-menu](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/associate-elastic-ip-menu.png)

13. In the **Instance** field, select the instance you just launched (`Library Management System`).
14. Click **Associate**.

![associate-elastic-ip-form](/images/5-Workshop/5.6-Application-deployment/5.6.1-Launch-EC2-and-attach-Elastic-IP/associate-elastic-ip-form.png)

{{% notice note %}}
An Elastic IP is a static IP address that doesn't change even if EC2 is stopped/started — avoiding the need to update `ALLOWED_HOSTS` in `.env` or the SSH connection info each time the instance is restarted.
{{% /notice %}}

After this step, EC2 is ready with a fixed IP address for SSH access and application deployment in the following steps.