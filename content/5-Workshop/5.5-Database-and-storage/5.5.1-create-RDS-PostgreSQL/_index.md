---
title : "Create RDS PostgreSQL"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.5.1 </b> "
---

RDS PostgreSQL is used to store all of the system's business data (books, users, borrow/return history), placed in the Private Subnet so it cannot be accessed directly from the Internet.

#### Step 1: Choose the Database Creation Method

1. Go to **RDS Console** → **Databases** → click **Create database**.
2. From the dropdown that appears, select **Full configuration** (allows detailed configuration of VPC, Subnet Group, Security Group — instead of letting AWS choose automatically like Express configuration).

![select-full-configuration](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/select-full-configuration.png)

#### Step 2: Choose the Engine

3. In **Engine options**, select **PostgreSQL**.
4. In **Choose a database creation method**, keep **Full configuration**.

![choose-engine-postgresql](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/choose-engine-postgresql.png)

#### Step 3: Choose the Template and Deployment Option

5. In **Templates**, select **Dev/Test** (suitable for a project/workshop, no need to optimize cost like Production).
6. In **Availability and durability**, select **Single-AZ DB instance deployment (1 instance)** — creates only 1 primary instance with no standby, appropriate since this is a learning environment that doesn't need high availability.

![template-and-deployment](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/template-and-deployment.png)

#### Step 4: Configure Settings

7. In the **Settings** section, enter:
   - **DB instance identifier**: `library-db`
   - **Master username**: `postgres`
   - **Credentials management**: select **Self managed**
   - **Master password**: set a strong password, **record it carefully**
   - **Confirm master password**: re-enter it

![settings-credentials](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/settings-credentials.png)

#### Step 5: Configure Instance and Storage

8. In **Instance configuration**:
   - Select **Burstable classes (includes t classes)**
   - **Instance type**: `db.t3.micro` (free tier)
9. In **Storage**:
   - **Storage type**: General Purpose SSD (gp3)
   - **Allocated storage**: `20` GiB

![instance-and-storage](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/instance-and-storage.png)

#### Step 6: Configure Connectivity

10. In **Connectivity**:
    - **Virtual private cloud (VPC)**: select `library-vpc (vpc-0686bd0330b6b622f)`
    - **DB subnet group**: select **Create new DB Subnet Group**
    - **Public access**: select **No**
    - **VPC security group (firewall)**: select **Choose existing** → select `library-rds-sg`

![connectivity-settings](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/connectivity-settings.png)

{{% notice note %}}
**Public access = No** ensures RDS is not assigned a public IP address — only resources within the VPC (specifically EC2 with the `library-ec2-sg` Security Group) can connect to the database.
{{% /notice %}}

#### Step 7: Configure Additional Configuration

11. Scroll down to **Additional configuration** → **Database options**, enter:
    - **Initial database name**: `library_db`

{{% notice warning %}}
This is an important database name — it must match exactly with the `POSTGRES_DB` variable in the `.env` file during the later application configuration step, otherwise Django will report that it cannot find the database.
{{% /notice %}}

![initial-database-name](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/initial-database-name.png)

12. Keep the remaining sections (Backup, Encryption, Monitoring...) at their defaults.

#### Step 8: Create the Database

13. Scroll to the bottom of the page, review the **Estimated monthly costs**, click **Create database**.

![create-database-button](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/create-database-button.png)

14. Wait about 5–10 minutes for the status to change from **Creating** → **Available**.

#### Step 9: Get the Endpoint to Configure the Application

15. Once **Available**, select `library-db` → the **Connectivity & security** tab. In the **Connection steps** section, the line `export RDSHOST="..."` shows the database's **Endpoint**.

16. Copy this value — it will be used as `POSTGRES_HOST`/`DB_HOST` in the `.env` file in a later application configuration step.

![rds-endpoint](/images/5-Workshop/5.5-Database-and-storage/5.5.1-create-RDS-PostgreSQL/rds-endpoint.png)