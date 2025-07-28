---
title : "Setting Up IAM Role for Lambda"
date : "2023-12-01T00:00:00Z"
weight : 13
chapter : false
pre : " <b> 13. </b> "
---

**Content:**
- [Create IAM Role](13.1-create-iam-role/)
- [Configure Role Permissions](13.2-configure-role-permissions/)
- [Add S3 Access Policy](13.3-add-s3-access-policy/)

AWS Identity and Access Management (IAM) roles provide secure access to AWS services. In this section, we'll create an IAM role that allows Lambda functions to access S3 storage and execute basic operations.

#### Create IAM Role

1. Navigate to the IAM console and access the Roles section.
2. Create a new role with AWS Service as trusted entity.
3. Select Lambda as the use case for the role.

#### Configure Role Permissions

1. Attach the **AWSLambdaBasicExecutionRole** policy for basic Lambda execution.
2. Name the role **LeftoverDataCollectionRole** for easy identification.
3. Complete the role creation process.

#### Add S3 Access Policy

1. Access the newly created role and add additional permissions.
2. Create an inline policy for S3 access permissions.
3. Configure JSON policy to allow S3 operations on the leftover-storage bucket.