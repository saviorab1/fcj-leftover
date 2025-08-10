---
title : "Creating Lambda Function for Data Collection"
date : "2025-08-10T20:24:00Z"
weight : 14
chapter : false
pre : " <b> 14. </b> "
---

**Content:**
- [Create Lambda Function](14.1-create-lambda-function/)
- [Implement Data Collection Code](14.2-implement-data-collection-code/)

AWS Lambda allows you to run code without provisioning servers. In this section, we'll create a Lambda function that collects user input data and stores it in our S3 bucket with proper organization and metadata.

#### Create Lambda Function

1. Navigate to the Lambda console and start function creation.
2. Configure the function with Node.js runtime and existing IAM role.
3. Set up the function name and basic execution settings.

#### Implement Data Collection Code

1. Access the Lambda function code editor.
2. Replace the default code with data collection logic.
3. Configure S3 integration for organized data storage with partitioning.
