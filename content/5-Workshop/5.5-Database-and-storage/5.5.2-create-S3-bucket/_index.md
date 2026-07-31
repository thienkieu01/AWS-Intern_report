---
title : "Create S3 Bucket"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.5.2 </b> "
---

Amazon S3 is used to store book cover images and documents uploaded by users, separate from EC2's lifecycle to ensure durable data storage.

#### Step 1: Create the Bucket

1. Go to **S3 Console** → **Buckets** → click **Create bucket**.
2. In **General configuration**:
   - **AWS Region**: US East (N. Virginia) us-east-1 (matching EC2/RDS)
   - **Bucket type**: General purpose
   - **Bucket name**: `library-workshop-2026` (name must be **globally unique**, change it to your own name if it's taken)

![create-bucket-name](/images/5-Workshop/5.5-Database-and-storage/5.5.2-create-S3-bucket/create-bucket-name.png)

#### Step 2: Configure Block Public Access

3. Scroll down to **Block Public Access settings for this bucket**, **uncheck** the **Block all public access** box.
4. Check the confirmation box **"I acknowledge that the current settings might result in this bucket and the objects within becoming public."**

![block-public-access](/images/5-Workshop/5.5-Database-and-storage/5.5.2-create-S3-bucket/block-public-access.png)

{{% notice note %}}
Turning off Block Public Access allows book cover images to be displayed publicly via URL on the web interface. This is a suitable choice for a project/demo — for a real production system, consider using CloudFront + Signed URLs instead of exposing the bucket directly to the public.
{{% /notice %}}

#### Step 3: Configure Encryption and Create the Bucket

5. In the **Default encryption** section, keep **Server-side encryption with Amazon S3 managed keys (SSE-S3)**.
6. Keep the other sections (Versioning, Tags, Advanced settings) at their defaults.
7. Scroll to the bottom, click **Create bucket**.

![create-bucket-button](/images/5-Workshop/5.5-Database-and-storage/5.5.2-create-S3-bucket/create-bucket-button.png)

#### Step 4: Configure a Bucket Policy to Allow Public Read

8. After the bucket is created, go to the `library-workshop-2026` bucket → the **Permissions** tab.
9. Scroll down to **Bucket policy** → click **Edit**.

![permissions-tab](/images/5-Workshop/5.5-Database-and-storage/5.5.2-create-S3-bucket/permissions-tab.png)

10. Paste in the following policy (remember to replace `library-workshop-2026` with your actual bucket name):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::library-workshop-2026/*"
    }
  ]
}
```

11. Click **Save changes**.

![save-bucket-policy](/images/5-Workshop/5.5-Database-and-storage/5.5.2-create-S3-bucket/save-bucket-policy.png)

{{% notice note %}}
This Bucket Policy allows **anyone** to read (GetObject) files in the bucket via a direct URL, for the purpose of displaying book cover images on the website. It only grants **read** access, not write/delete from outside — writing files is still only possible through the application, using the `library-app-user` Access Key.
{{% /notice %}}

After this step, your bucket is ready for the Django application to write and display book cover images. The information needed for the `.env` configuration step is:
```
AWS_STORAGE_BUCKET_NAME=library-workshop-2026
AWS_S3_REGION_NAME=us-east-1
```