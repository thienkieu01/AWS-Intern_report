---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# AWS KMS – WHAT I LEARNED ABOUT AWS'S ENCRYPTION KEY MANAGEMENT SERVICE

AWS Key Management Service (AWS KMS) is AWS's managed encryption key management service that enables users to securely create, store, and control the use of cryptographic keys. When integrated with services such as Amazon S3, Amazon EBS, Amazon RDS, and Amazon DynamoDB, AWS KMS protects data at rest through encryption while providing centralized access control and key usage auditing via AWS CloudTrail.

The key concepts include:

* AWS KMS is a **Fully Managed** service for creating, storing, and managing encryption keys on AWS.
* Supports **Encryption at Rest** for multiple AWS services, including **Amazon S3, Amazon EBS, Amazon RDS**, and **Amazon DynamoDB**.
* Distinguishes between **Encryption in Transit** (encrypting data while it is being transmitted) and **Encryption at Rest** (encrypting stored data).
* Uses a combination of **Customer Master Keys (CMKs)** and **Data Keys** to securely and efficiently encrypt large amounts of data.
* Encryption keys are protected within **Hardware Security Modules (HSMs)** and cannot be directly extracted.
* Integrates with **AWS CloudTrail** to record all key usage activities for auditing and compliance purposes.
* Access to data stored in Amazon S3 and permission to use a KMS key are independent. Users must have permission to use the KMS key before they can decrypt encrypted data.

AWS KMS is particularly suitable for systems that require a high level of security, enabling organizations to centrally manage encryption keys, enforce access control, and protect data across multiple AWS services.


## Implementation Guide

### Step 1: Create an Encryption Key in AWS KMS

- Open the **AWS Key Management Service** console.
- Select **Create Key**.
- Configure the following settings:
  - Symmetric Key
  - Encrypt and Decrypt
  - Single Region
- Assign an Alias and configure the **Key Administrators** and **Key Users**.

### Step 2: Create an Amazon S3 Bucket

- Create a new Amazon S3 bucket.
- Enable **Default Encryption**.
- Select **Server-side encryption using AWS KMS (SSE-KMS)**.
- Specify the KMS key created in the previous step.

### Step 3: Upload Data to Amazon S3

- Upload any file to the bucket.
- Verify the **Properties** section to confirm that the object has been encrypted using the specified KMS key.

### Step 4: Verify Access Permissions

- Create an IAM user with only **Amazon S3 Full Access** permissions and attempt to download the encrypted object.
- Observe the **Access Denied** error because the user has not been granted permission to use the KMS key.
- Add the IAM user to the **Key Users** list of the KMS key.
- Test again and verify that the user can now access and decrypt the object successfully.

## Results Achieved

- Gained an understanding of the role of AWS KMS in managing encryption keys on AWS.
- Learned the difference between **Encryption in Transit** and **Encryption at Rest**.
- Understood how **Customer Master Keys (CMKs)** and **Data Keys** work together during the encryption process.
- Learned how to configure Amazon S3 encryption using **AWS KMS**.
- Understood the relationship between **AWS IAM**, **Amazon S3**, and **AWS KMS** in controlling access to encrypted data.
- Learned how to use **AWS CloudTrail** to monitor and audit encryption key usage.

## References

![AWS Backup & Restore](/images/3-Blogs/blog2.jpg)

- Workshop: https://000033.awsstudygroup.com/
- Tutorial Video: https://youtu.be/SCZpW-3b5G0?si=fM551VA4uu49_EWJ
- AWS Documentation: https://docs.aws.amazon.com/kms/
