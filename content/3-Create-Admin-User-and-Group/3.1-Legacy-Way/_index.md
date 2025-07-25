---
title : "Setting up AWS Bedrock (Legacy)"
date : "2023-12-01T00:00:00Z"
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---

## Content



## Request an AWS Bedrock Model

You will need to get to Amazon Bedrock and click on Model Catalog. 

You will be greeted by one of those two pages. In either way, click on the mark part of the image.

 ![IAM Frontpage](/images/3/8-0.png?featherlight=false&width=90pc)

 ![IAM Frontpage](/images/3/8-0-1.png?featherlight=false&width=90pc)

Afterward, click on the AI model and click on Modify Access.

 ![IAM Frontpage](/images/3/8-1.png?featherlight=false&width=90pc)


## Using CloudShell to set up the management

In this case, we will choose Claude 3.5 Sonnet as it is readily available at ap-southeast-1 region. You can check the availability of AI models within each region via this link: https://docs.aws.amazon.com/bedrock/latest/userguide/models-regions.html

First, you will need to choose to modify the Model Access. There are two scenarios:

This is the scenario where you have not modfiy any model access into Amazon Bedrock. If you are in this case, choose **Modify model access**.

 ![IAM Frontpage](/images/3/8-2.png?featherlight=false&width=90pc)

This is the scenario where you have modfiy any model access into Amazon Bedrock. If you are in this case, choose **Enable Specific Model**.

 ![IAM Frontpage](/images/3/8-3.png?featherlight=false&width=90pc)

After that, choose the model that you want, and in this case, it is CLaude SOnnet 3.5.

 ![IAM Frontpage](/images/3/8-4.png?featherlight=false&width=90pc)