---
title : "Creating and Developing Amazon Bedrock and CloudWatch"
date : "2023-12-01T00:00:00Z"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

## Content
- [Setting up AWS Bedrock Model (2 Ways)](#setting-up-aws-bedrock-mode)
- [Legacy Way](#legacy-way)
- [Cross-Region Way](#cross-region-way)
- [Deploy Cloudwatch](#deploy-cloudwatch)

## Request Amazon Bedrock models

1. You will be using Bedrock Model and setting up using Claude Sonnet. 

2. There will be two ways to build the Bedrock Model based on how you intepret. 

- Implementing the servers using manual coding for a fallback server.
- Using cross-region to make a fallback server. 

---

## Legacy Way

1. Go to Amazon Bedrock and get for yourself the AI Model. In this case, it should be Claude Sonnet 2.5

2. Change AWS region to another region that is suitable → repeat Step 1 to enable Claude 3.5 Sonnet in that region. This provides a backup model in case of failure or latency.

3. In Amplify backend:

Modify backend.ts to add two data sources: one for primary and one for fallback with correct PolicyStatement.

Create bedrock.js under amplify/data → handle request/response logic for model invocation with fallback logic.

Update resource.ts to define askBedrock and askBedrockFallback GraphQL queries, attach to the right data source, and configure authentication.

---

## Cross-Region Way

To ensure high availability and performance, you can configure Claude models to work across AWS regions using cross-region inference profiles.

1. Go to Amazon Bedrock and select a Claude Sonnet 4 → click Next and confirm access.

2. Click Cross-region inference beside the model → copy the Inference profile ID and Model ID for each region you want to support.

3. In backend.ts, configure both Cross-Region and Fallback endpoints using addHttpDataSource() and grant model access with the correct ARN.

4. In bedrock.js, use the modelId dynamically in resourcePath, and define max_tokens, temperature, and other parameters as needed.

---

## Deploy Cloudwatch

To track model invocation and latency, set up a simple dashboard in AWS CloudWatch.

1. Go to CloudWatch → Metrics → All metrics, search for AWS Bedrock, then select Bedrock > By ModelID.

2. Choose metrics such as:

{{% notice note %}}
**Invocations (number of invoke calls)** and
**InvocationLatency (response time)**
{{% /notice %}}

3. Go to CloudWatch again to create dashboard.

4. Add a widget and equip the metrics.