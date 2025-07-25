---
title : "Setting up AWS Bedrock (Cross-Region)"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

## Content
- [Request an AWS Bedrock Model](#request-an-aws-bedrock-model)
- [Choosing the AI Model inside Bedrock](#choosing-the-ai-model-inside-bedrock)
- [Make a fallback server](#make-a-fallback-server)
- [Request an AWS Bedrock Model](#request-an-aws-bedrock-model)

## Request an AWS Bedrock Model

Same as the Legacy Way, you will need to get to Amazon Bedrock and click on Model Catalog. 

You will be greeted by one of those two pages. In either way, click on the mark part of the image.

 ![IAM Frontpage](/images/3/8-0.png?featherlight=false&width=90pc)

 ![IAM Frontpage](/images/3/8-0-1.png?featherlight=false&width=90pc)

Afterward, click on the AI model and click on Modify Access.

 ![IAM Frontpage](/images/3/8-1.png?featherlight=false&width=90pc)

## Choosing the AI Model inside Bedrock

In this case, we will choose Claude 4 Sonnet as it is readily available at ap-southeast-1 region and **it has cross-region**. 

First, you will need to choose to modify the Model Access. There are two scenarios:

This is the scenario where you have not modfiy any model access into Amazon Bedrock. If you are in this case, choose **Modify model access**.

 ![IAM Frontpage](/images/3/8-2.png?featherlight=false&width=90pc)

This is the scenario where you have modfiy any model access into Amazon Bedrock. If you are in this case, choose **Enable Specific Model**.

 ![IAM Frontpage](/images/3/8-3.png?featherlight=false&width=90pc)

After that, choose the model that you want, and in this case, it is Claude Sonnet 4.

 ![IAM Frontpage](/images/3/8-4-Alternate.png?featherlight=false&width=90pc)

Hit Submit after, nothing much will need to be changed. You will need to wait for a while for the model to finish setting up. You should see this screen.

 ![IAM Frontpage](/images/3/8-5-Alternate.png?featherlight=false&width=90pc)