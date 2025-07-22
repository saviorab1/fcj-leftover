---
title : "Creating S3 Bucket for Data Storage"
date : "2023-12-01T00:00:00Z"
weight : 12
chapter : false
pre : " <b> 12. </b> "
---

**Content:**
- [Navigate to S3 Console](#navigate-to-s3-console)
- [Configure bucket settings](#configure-bucket-settings)
- [Create the bucket](#create-the-bucket)

#### Navigate to S3 Console

1. Go to the AWS Management Console and navigate to the **S3 service**.
2. Click **Create bucket** to start the bucket creation process.

![S3 Console](/images/12/0001.png?featherlight=false&width=90pc)

#### Configure bucket settings

Configure the following settings for your S3 bucket:

**Basic Configuration:**
- **Bucket name**: `leftover-storage` (must be globally unique)
- **Region**: `ap-southeast-1` (same as your Amplify app)

**Security Settings:**
- **Block Public Access**: Keep all settings checked (data should remain private)

**Advanced Features:**
- **Bucket Versioning**: Enable (for data integrity)
- **Default encryption**: Enable with SSE-S3

![Bucket Configuration](/images/12/0002.png?featherlight=false&width=90pc)

{{% notice info %}}
Ensure the bucket name is globally unique across all AWS accounts. If "leftover-storage" is taken, append a unique identifier like your initials or numbers.
{{% /notice %}}

#### Create the bucket

After configuring all settings:

1. Review your configuration settings to ensure they match the requirements.
2. Click **Create bucket** to finalize the creation.

![Create Bucket](/images/12/0003.png?featherlight=false&width=90pc)

3. Your S3 bucket will be created successfully and appear in your S3 console.

![Bucket Created](/images/12/0004.png?featherlight=false&width=90pc)

{{% notice note %}}
The bucket is now ready to store your application data securely with versioning enabled and public access blocked by default.
{{% /notice %}}
