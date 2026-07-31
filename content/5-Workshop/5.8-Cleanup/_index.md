---
title : "Resource Cleanup"
date : 2024-01-01
weight : 8
chapter : false
pre : " <b> 5.8. </b> "
---

#### Overview

+ After completing the workshop, it's recommended to delete the AWS resources created to avoid unwanted charges (especially RDS, Elastic IP, and EC2 if no longer within the free tier).

+ The deletion order **matters a lot** — some resources depend on each other (e.g., RDS's Security Group must be deleted before EC2's Security Group, and the VPC cannot be deleted while it still contains resources). Follow the order below to avoid errors.

{{% notice warning %}}
This action **cannot be undone**. All data in RDS, images in S3, and code on EC2 will be permanently lost after deletion. Only proceed once you're certain you no longer need them.
{{% /notice %}}

#### Step 1: Terminate the EC2 Instance

1. Go to **EC2 Console** → **Instances**, select the instance running the application.
2. **Instance state** → **Terminate (delete) instance**.

![terminate-ec2-menu](/images/5-Workshop/5.8-Cleanup/terminate-ec2-menu.png)

3. Confirm by clicking **Terminate (delete)**.

![terminate-ec2-confirm](/images/5-Workshop/5.8-Cleanup/terminate-ec2-confirm.png)

#### Step 2: Release the Elastic IP

An Elastic IP still incurs charges if it's not attached to a running instance — it must be released separately after terminating EC2:

4. Go to **EC2 Console** → **Elastic IPs**, select the IP address used (e.g., `54.82.167.72`).
5. If the IP still shows as attached (Associated instance ID), select **Actions** → **Disassociate Elastic IP address** first.

![disassociate-eip](/images/5-Workshop/5.8-Cleanup/disassociate-eip.png)

6. Then select **Actions** → **Release Elastic IP addresses**, click **Release** to confirm.

![release-eip-confirm](/images/5-Workshop/5.8-Cleanup/release-eip-confirm.png)

#### Step 3: Delete the RDS Database

7. Go to **RDS Console** → **Databases**, select `library-db`.
8. **Actions** → **Delete**.

![delete-rds-menu](/images/5-Workshop/5.8-Cleanup/delete-rds-menu.png)

9. Uncheck **Create final snapshot** (if you don't need to keep the data), type `delete me` in the confirmation field, then click **Delete**.

![delete-rds-confirm](/images/5-Workshop/5.8-Cleanup/delete-rds-confirm.png)

{{% notice note %}}
Deleting RDS may take a few minutes. Once RDS is fully deleted, the **DB Subnet Group** (linking the 2 Private Subnets) and RDS's **Security Group** (Step 7) can then be deleted.
{{% /notice %}}

#### Step 4: Delete the Data in the S3 Bucket

An S3 Bucket cannot be deleted if it still contains objects:

10. Go to **S3 Console**, select the `library-workshop-2026` bucket.
11. Click **Empty**, type `permanently delete` to confirm, and wait for the process to complete.

![empty-bucket-confirm](/images/5-Workshop/5.8-Cleanup/empty-bucket-confirm.png)

12. Once the bucket is empty, click **Delete**, and type the exact bucket name to confirm.

#### Step 5: Delete the IAM User and IAM Role

13. Go to **IAM Console** → **Users**, select `library-app-user`.
14. Go to the **Security credentials** tab, find **Access keys**, select the **Active** key → **Deactivate** → confirm, then **Delete** to permanently remove the key.

{{% notice warning %}}
The Access Key must be **deactivated and deleted first** — you cannot delete an IAM User directly while it still has an existing Access Key.
{{% /notice %}}

15. Once all Access Keys are deleted, go back to the **Users** page, select `library-app-user` → **Delete**, type `confirm` to confirm, and click **Delete user**.

![delete-iam-user-confirm](/images/5-Workshop/5.8-Cleanup/delete-iam-user-confirm.png)

16. Go to **IAM Console** → **Roles**, select `library-ec2-cloudwatch-role` → **Delete**.

#### Step 6: Delete the CloudWatch Log Group

17. Go to **CloudWatch Console** → **Log groups**, select `library-app-logs` → **Actions** → **Delete log group(s)**.

#### Step 7: Delete the Security Groups

EC2's Security Group (`library-ec2-sg`) is referenced in an inbound rule by RDS's Security Group (`library-rds-sg`), so **`library-rds-sg` must be deleted first**:

18. Go to **EC2 Console** → **Security Groups**, select `library-rds-sg` → **Actions** → **Delete security groups** → confirm.

![delete-rds-sg-confirm](/images/5-Workshop/5.8-Cleanup/delete-rds-sg-confirm.png)

19. Once `library-rds-sg` has been deleted, select `library-ec2-sg` → **Delete security groups** → confirm.

![delete-ec2-sg-confirm](/images/5-Workshop/5.8-Cleanup/delete-ec2-sg-confirm.png)

#### Step 8: Delete the VPC and Related Components

20. Go to **VPC Console** → **Your VPCs**, select `library-vpc`.
21. Click **Actions** → **Delete VPC**. AWS will display a full list of the child resources that will also be deleted, e.g.: `library-igw`, `public-rt`, `private-rt`, `public-subnet`, `private-subnet-1`...

![delete-vpc-confirm](/images/5-Workshop/5.8-Cleanup/delete-vpc-confirm.png)

22. Type `delete` in the confirmation field, click **Delete**.

{{% notice note %}}
If **Delete VPC** returns an error due to remaining dependent resources, go back and verify Steps 1–7 were completed in the correct order, especially RDS (Step 3) and the Security Groups (Step 7).
{{% /notice %}}