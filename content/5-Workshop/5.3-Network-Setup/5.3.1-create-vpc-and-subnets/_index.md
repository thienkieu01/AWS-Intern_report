---
title : "Create VPC and Subnets"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

#### Step 1: Create the VPC

1. Open the [Amazon VPC console]
2. In the navigation pane, select **Your VPCs**, click **Create VPC**.
3. On the **Create VPC** screen, configure as follows:
   - **Resources to create**: select **VPC only**
   - **Name tag**: `library-vpc`
   - **IPv4 CIDR block**: `10.0.0.0/16`
   - **IPv6 CIDR block**: No IPv6 CIDR block
   - **Tenancy**: Default

![create-vpc](/images/5-Workshop/5.3-Network-setup/5.3.1-create-vpc-and-subnets/create-vpc.png)

{{% notice note %}}
The CIDR range `10.0.0.0/16` allows up to 65,536 IP addresses in the VPC — enough to be split into multiple smaller subnets for public and private use.
{{% /notice %}}

4. Scroll to the bottom of the page, review the information (Name tag, IPv4 CIDR), then click **Create VPC**.

![create-vpc-confirm](/images/5-Workshop/5.3-Network-setup/5.3.1-create-vpc-and-subnets/create-vpc-confirm.png)

5. After it's created successfully, you'll receive a **VPC ID** (e.g., `vpc-0686bd0330b6b622f`) — note this ID down for use in later steps.

---

#### Step 2: Enable DNS Settings for the VPC

{{% notice warning %}}
This is a step that's easy to miss but **required** — if not enabled, RDS and other internal services within the VPC may not resolve domain names correctly, causing connection errors that are hard to diagnose later.
{{% /notice %}}

6. In the **VPC Console**, select the `library-vpc` you just created.
7. Click **Actions** → **Edit VPC settings**.
8. In the **DNS settings** section, check both boxes:
   - **Enable DNS resolution**
   - **Enable DNS hostnames**
9. Click **Save**.

![vpc-dns-settings](/images/5-Workshop/5.3-Network-setup/5.3.1-create-vpc-and-subnets/vpc-dns-settings.png)

{{% notice note %}}
- **Enable DNS resolution**: allows instances in the VPC to use Amazon's internal DNS server to resolve domain names.
- **Enable DNS hostnames**: allows instances with a public IP address to also be assigned a corresponding DNS hostname.

Both of these settings are required for the RDS endpoint (in the form `library-db.xxxxx.rds.amazonaws.com`) to correctly resolve to an internal IP address when EC2 connects to it.
{{% /notice %}}

---

#### Step 3: Create Subnets

In this section, you will create 3 subnets within `library-vpc`:

| Subnet | CIDR | Availability Zone | Type |
|---|---|---|---|
| public-subnet | 10.0.1.0/24 | us-east-1a | Public |
| private-subnet-1 | 10.0.2.0/24 | us-east-1a | Private |
| private-subnet-2 | 10.0.3.0/24 | us-east-1b | Private |

{{% notice tip %}}
Create the 2 private subnets in 2 different Availability Zones (us-east-1a and us-east-1b) to ensure high availability (Multi-AZ) when RDS is deployed later.
{{% /notice %}}

10. In the navigation pane, select **Subnets**, click **Create subnet**.
11. In the **VPC** field, select `vpc-0686bd0330b6b622f (library-vpc)`.

![select-vpc](/images/5-Workshop/5.3-Network-setup/5.3.1-create-vpc-and-subnets/select-vpc.png)

**Create public-subnet:**

12. Enter the details:
    - **Subnet name**: `public-subnet`
    - **Availability Zone**: `us-east-1a`
    - **IPv4 subnet CIDR block**: `10.0.1.0/24`
13. Click **Create subnet**.

![public-subnet](/images/5-Workshop/5.3-Network-setup/5.3.1-create-vpc-and-subnets/public-subnet.png)

**Create private-subnet-1:**

14. Click **Add new subnet**, enter:
    - **Subnet name**: `private-subnet-1`
    - **Availability Zone**: `us-east-1a`
    - **IPv4 subnet CIDR block**: `10.0.2.0/24`
15. Click **Create subnet**.

![private-subnet-1](/images/5-Workshop/5.3-Network-setup/5.3.1-create-vpc-and-subnets/private-subnet-1.png)

**Create private-subnet-2:**

16. Click **Add new subnet**, enter:
    - **Subnet name**: `private-subnet-2`
    - **Availability Zone**: `us-east-1b`
    - **IPv4 subnet CIDR block**: `10.0.3.0/24`
17. Click **Create subnet**.

![private-subnet-2](/images/5-Workshop/5.3-Network-setup/5.3.1-create-vpc-and-subnets/private-subnet-2.png)

{{% notice note %}}
Once complete, you'll have 1 VPC (`library-vpc`) with DNS resolution/hostnames enabled, containing 3 subnets: 1 public subnet for EC2, and 2 private subnets for RDS (Multi-AZ).
{{% /notice %}}