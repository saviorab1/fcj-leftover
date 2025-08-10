---
title : "Create Lambda Function"
date : "2025-08-10T20:24:00Z"
weight : 1
chapter : false
pre : " <b> 14.1 </b> "
---

#### Access Lambda Console

To create a Lambda function for data collection, you need to navigate to the Lambda service within the AWS Management Console.

#### Navigate to Lambda Console

1. Go to the AWS Management Console and search for **Lambda** in the services search bar.
2. Click on **Lambda** to access the Lambda console.
3. Click **Create function** to start the function creation process.

![Lambda Console](/images/14/14-1.png?featherlight=false&width=90pc)

#### Configure Function Settings

Set up the basic configuration for your Lambda function:

**Function name**: `leftover-data-collector`
- Use a descriptive name that identifies the function's purpose

**Runtime**: `Node.js 22.x`
- Select the latest Node.js runtime for optimal performance

**Architecture**: `x86_64`
- Choose the standard x86_64 architecture

![Function Configuration](/images/14/14-2.png?featherlight=false&width=90pc)

#### Configure Execution Role

**Execution role**: 
1. Select **Use an existing role** option.
2. Choose **LeftoverDataCollectionRole** from the dropdown.
3. This role provides the necessary permissions for S3 access and basic execution.

![Execution Role](/images/14/14-3.png?featherlight=false&width=90pc)

{{% notice info %}}
Using the existing role ensures your Lambda function has the proper permissions to write data to the S3 bucket and execute with CloudWatch logging.
{{% /notice %}}

#### Create the Function

1. Review all configuration settings to ensure they match the requirements.
2. Click **Create function** to finalize the creation process.

![Create Function](/images/14/14-4.png?featherlight=false&width=90pc)

#### Result

Your Lambda function `leftover-data-collector` is now created and ready for code implementation in the next step.
