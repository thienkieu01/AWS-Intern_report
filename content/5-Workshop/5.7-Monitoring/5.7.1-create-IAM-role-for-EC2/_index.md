---
title : "Create IAM Role for CloudWatch"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.7.1 </b> "
---

For EC2 to be able to send logs and metrics to CloudWatch, the instance needs to have an IAM Role attached with the appropriate permissions. By default EC2 has no role attached, so the first step is to create a new role in the IAM Console, then attach it to the instance.

#### Step 1: Create a New Role in the IAM Console

1. Go to **IAM Console** → **Roles**, click **Create role**.

![iam-roles-create-role](/images/5-Workshop/5.7-Monitoring/5.7.1-create-IAM-role-for-EC2/iam-roles-create-role.png)

2. In **Service or use case**, select/type **EC2**.
3. In **Use case**, select **EC2** (Allows EC2 instances to call AWS services on your behalf), then click **Next**.

![select-ec2-use-case](/images/5-Workshop/5.7-Monitoring/5.7.1-create-IAM-role-for-EC2/select-ec2-use-case.png)

4. In **Permissions policies**, search for `CloudWatchAgentServerPolicy`.
5. Check this policy, then click **Next**.

![attach-cloudwatch-agent-policy](/images/5-Workshop/5.7-Monitoring/5.7.1-create-IAM-role-for-EC2/attach-cloudwatch-agent-policy.png)

{{% notice note %}}
`CloudWatchAgentServerPolicy` is an AWS-managed policy that grants the permissions needed for the CloudWatch Agent on EC2 to send logs and metrics to CloudWatch.
{{% /notice %}}

6. Enter a role name, e.g.: `library-ec2-cloudwatch-role`.
7. Enter a short description, e.g.: *"Allows EC2 instances to call AWS services on your behalf"*.
8. Review the **Trust policy** (EC2 is already allowed to assume this role by default), then scroll down and click **Create role**.

![name-and-create-role](/images/5-Workshop/5.7-Monitoring/5.7.1-create-IAM-role-for-EC2/name-and-create-role.png)

#### Step 2: Attach the New Role to the EC2 Instance

9. Go to **EC2 Console** → **Instances**, select the instance running the application.
10. Click **Actions** → **Security** → **Modify IAM role**.

![modify-iam-role](/images/5-Workshop/5.7-Monitoring/5.7.1-create-IAM-role-for-EC2/modify-iam-role.png)

11. In the **IAM role** field, select the `library-ec2-cloudwatch-role` you just created.
12. Click **Update IAM role** to confirm.

![update-iam-role](/images/5-Workshop/5.7-Monitoring/5.7.1-create-IAM-role-for-EC2/update-iam-role.png)

After this step, EC2 has sufficient permissions to run the CloudWatch Agent. The next step (5.7.2) will install and configure the Agent on the instance.