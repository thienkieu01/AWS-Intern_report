---
title : "Create IAM User"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

An IAM User is created so the Django application (running on EC2) has permission to write data to S3 without needing the root account key — following the **least privilege** principle (granting only the permissions needed).

#### Step 1: Create the User

1. Go to **IAM Console** → **IAM users** → click **Create user**.
2. On the **Specify user details** screen:
   - **User name**: `library-app-user`
   - **Do not check** "Provide user access to the AWS Management Console" (this user only needs programmatic access via an Access Key, no Console login required)
3. Click **Next**.

![specify-user-details](/images/5-Workshop/5.4-Security-Setup/5.4.1-create-iam-user/specify-user-details.png)

#### Step 2: Grant Permissions

4. On the **Set permissions** screen, select **Attach policies directly**.
5. Search for and check the **`AmazonS3FullAccess`** policy.
6. Click **Next**, then **Create user** on the review screen.

![set-permissions](/images/5-Workshop/5.4-Security-Setup/5.4.1-create-iam-user/set-permissions.png)

{{% notice note %}}
For a real production environment, it's better to create a custom policy that allows actions on only one specific bucket instead of granting permissions across all of S3.
{{% /notice %}}

#### Step 3: Create an Access Key

7. After the user is created, go to the `library-app-user` details page, in the **Access key 1** section, click **Create access key**.

![create-access-key-button](/images/5-Workshop/5.4-Security-Setup/5.4.1-create-iam-user/create-access-key-button.png)

8. In the **Use case** step, select **Application running on an AWS compute service** (since the application will run on EC2), check the recommendation confirmation box, click **Next**.

![select-use-case](/images/5-Workshop/5.4-Security-Setup/5.4.1-create-iam-user/select-use-case.png)

9. (Optional) In the **Set description tag** step, enter a description, e.g. `library-app-key`, click **Create access key**.

![set-description-tag](/images/5-Workshop/5.4-Security-Setup/5.4.1-create-iam-user/set-description-tag.png)

10. The **Retrieve access keys** screen displays the **Access key ID** and **Secret access key**.

![retrieve-access-keys](/images/5-Workshop/5.4-Security-Setup/5.4.1-create-iam-user/retrieve-access-keys.png)

{{% notice warning %}}
**The Secret access key is only shown once.** Click **Download .csv file** or copy both values immediately to a safe location before clicking **Done** — once you leave this page, you cannot view it again, and you'll need to create a new access key if you forget to save it.
{{% /notice %}}

These two values will be entered into the application's `.env` file in a later configuration step:
```
AWS_ACCESS_KEY_ID=<the access key you just created>
AWS_SECRET_ACCESS_KEY=<the secret key you just created>
```