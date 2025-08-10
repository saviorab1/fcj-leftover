---
title : "Configure Role Permissions"
date : "2025-08-10T20:24:00Z"
weight : 2
chapter : false
pre : " <b> 13.2 </b> "
---

#### Add Basic Lambda Permissions

Configure the essential permissions required for Lambda function execution.

#### Select Permission Policies

1. In the permissions step, search for **AWSLambdaBasicExecutionRole**.
2. Select the checkbox next to **AWSLambdaBasicExecutionRole** policy.
3. This policy provides basic execution permissions for Lambda functions.

![Permission Policies](/images/13/13-4.png?featherlight=false&width=90pc)

{{% notice info %}}
The AWSLambdaBasicExecutionRole policy allows Lambda to write logs to CloudWatch Logs, which is essential for debugging and monitoring.
{{% /notice %}}

#### Name the Role

1. Provide a descriptive name for the role: **LeftoverDataCollectionRole**.
2. Optionally, add a description explaining the role's purpose.
3. Review the selected policies and trusted entities.

![Role Name](/images/13/13-5.png?featherlight=false&width=90pc)

#### Create the Role

1. Click **Create role** to finalize the role creation.
2. The role will be created and appear in your IAM roles list.

![Role Created](/images/13/13-6.png?featherlight=false&width=90pc)

#### Result

Your IAM role **LeftoverDataCollectionRole** is now created with basic Lambda execution permissions. The next step will add S3 access permissions.
