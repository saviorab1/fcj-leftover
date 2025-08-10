---
title : "Create the Bucket"
date : "2025-08-10T20:24:00Z"
weight : 3
chapter : false
pre : " <b> 12.3 </b> "
---

#### Review and Create

After configuring all the necessary settings, it's time to review and create your S3 bucket.

#### Final Review

Before creating the bucket:

1. Review all your configuration settings to ensure they match the requirements:
   - Bucket name: `leftover-storage`
   - Region: `ap-southeast-1`
   - Public access: Blocked
   - Versioning: Enabled
   - Encryption: SSE-S3 enabled

![Review Settings](/images/12/12-6.PNG?featherlight=false&width=90pc)

#### Create the Bucket

1. Scroll down to the bottom of the configuration page.
2. Click **Create bucket** to finalize the creation process.

![Create Bucket](/images/12/12-7.png?featherlight=false&width=90pc)

#### Successful Creation

Once the bucket is created successfully:

1. You will see a confirmation message indicating the bucket was created.
2. Your new S3 bucket will appear in the S3 console bucket list.

![Bucket Created](/images/12/12-7.png?featherlight=false&width=90pc)

#### Result

Your S3 bucket `leftover-storage` is now ready to store your application data securely with:
- Versioning enabled for data integrity
- Public access blocked for security
- Default encryption for data protection

{{% notice note %}}
The bucket is now ready to integrate with your application for secure data storage.
{{% /notice %}}
