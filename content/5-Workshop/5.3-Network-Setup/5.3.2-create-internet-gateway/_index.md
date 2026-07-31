---
title : "Create Internet Gateway"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

An Internet Gateway (IGW) is the component that allows resources in the public subnet (such as EC2) to communicate with the Internet.

#### Step 1: Create the Internet Gateway

1. In the VPC console navigation pane, select **Internet Gateways**, click **Create internet gateway**.
2. Configure:
   - **Name tag**: `library-igw`
3. Click **Create internet gateway**.

![create-igw](/images/5-Workshop/5.3-Network-setup/5.3.2-create-internet-gateway/create-igw.png)

4. Once created successfully, select the `library-igw` you just created, click **Actions** → **Attach to VPC**.

![select-attach-to-vpc](/images/5-Workshop/5.3-Network-setup/5.3.2-create-internet-gateway/select-attach-to-vpc.png)

#### Step 2: Attach the Internet Gateway to the VPC

5. On the **Attach to VPC** screen, under **Available VPCs**, enter/select the VPC `vpc-0686bd0330b6b622f` (`library-vpc`).
6. Click **Attach internet gateway**.

![attach-igw-confirm](/images/5-Workshop/5.3-Network-setup/5.3.2-create-internet-gateway/attach-igw-confirm.png)

{{% notice note %}}
Each VPC can only have **exactly 1** Internet Gateway attached at a time. After a successful attachment, the state of `library-igw` will change from `Detached` to `Attached`.
{{% /notice %}}