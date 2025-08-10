---
title : "Creating S3 Bucket for Data Storage"
date : "2025-08-10T20:24:00Z"
weight : 12
chapter : false
pre : " <b> 12. </b> "
---

**Content:**
- [Navigate to S3 Console](12.1-navigate-to-s3-console/)
- [Configure Bucket Settings](12.2-configure-bucket-settings/)
- [Create the Bucket](12.3-create-the-bucket/)

Amazon S3 (Simple Storage Service) provides secure, durable, and scalable object storage. In this section, we'll create an S3 bucket to store application data with proper security and versioning configurations.

#### Navigate to S3 Console

1. Access the AWS Management Console and search for the S3 service.
2. Click **Create bucket** to begin the bucket creation process.
3. This opens the configuration page where you'll specify all bucket settings.

#### Configure Bucket Settings

1. Set the bucket name to `leftover-storage` (must be globally unique).
2. Select region `ap-southeast-1` to match your Amplify app location.
3. Keep all **Block Public Access** settings checked for security.
4. Enable **Bucket Versioning** for data integrity and recovery.
5. Enable **Default Encryption** with SSE-S3 for automatic data protection.

#### Create the Bucket

1. Review all configuration settings to ensure they match requirements.
2. Click **Create bucket** to finalize the creation process.
3. Verify the bucket appears successfully in your S3 console.
