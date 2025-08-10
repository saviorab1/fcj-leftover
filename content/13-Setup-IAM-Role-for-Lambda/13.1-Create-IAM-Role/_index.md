---
title : "Create IAM Role"
date : "2025-08-10T20:24:00Z"
weight : 1
chapter : false
pre : " <b> 13.1 </b> "
---

#### Access IAM Console

To create an IAM role for Lambda functions, you need to navigate to the IAM service within the AWS Management Console.

#### Navigate to IAM Roles

1. Go to the AWS Management Console and search for **IAM** in the services search bar.
2. Click on **IAM** to access the Identity and Access Management console.
3. In the left navigation panel, click on **Roles**.

![IAM Console](/images/13/13-1.png?featherlight=false&width=90pc)

#### Start Role Creation

1. Click **Create role** to begin the role creation process.
2. This will open the role configuration wizard.

![Create Role](/images/13/13-2.png?featherlight=false&width=90pc)

#### Select Trusted Entity

1. Choose **AWS Service** as the trusted entity type.
2. Select **Lambda** from the use case options.
3. This configuration allows Lambda functions to assume this role.

![Select Service](/images/13/13-3.png?featherlight=false&width=90pc)

#### Result

You have successfully configured the basic role settings and are ready to add permissions in the next step.
