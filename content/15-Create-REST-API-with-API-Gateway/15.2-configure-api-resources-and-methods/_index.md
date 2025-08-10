---
title : "Configure API Resources and Methods"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 15.2 </b> "
---

Create the API resource structure and HTTP methods needed for data collection, integrating with your Lambda function for processing user inputs.

#### Create API Resource

1. In the API Gateway console, locate the **Resources** section on the left sidebar
2. Click **Create Resource** to add a new endpoint
3. Configure the resource settings:
   - **Resource Name**: `collect-data`
   - **Enable CORS**: Check this option for cross-origin support

![Create Resource](/images/15/15-5.png?featherlight=false&width=90pc)

![Create Resource](/images/15/15-6.png?featherlight=false&width=90pc)

#### Add POST Method

1. Select the newly created `/collect-data` resource
2. On the right side, click **Create Method**
3. Configure the method settings:
   - **Method Type**: **POST**
   - **Integration Type**: **Lambda Function**
   - **Lambda Region**: Verify it matches your Lambda function's region
   - **Lambda Function**: `leftover-data-collector`
   - **Use Lambda Proxy Integration**: **Yes** (Enable this option)

![Create Method](/images/15/15-7.png?featherlight=false&width=90pc)

![Create Method](/images/15/15-8.png?featherlight=false&width=90pc)

#### Verify Integration

1. The method execution flow will be displayed showing the integration path
2. Verify the **Integration Request** shows your Lambda function
3. The **Lambda Proxy Integration** should be enabled for automatic request forwarding

![Integration Verification](/images/15/15-9.png?featherlight=false&width=90pc)

#### Result

Your API now has a `/collect-data` resource with a POST method that integrates directly with your Lambda data collector function. The Lambda proxy integration ensures that all request data is automatically forwarded to your function for processing.

{{% notice info %}}
Lambda proxy integration simplifies the API setup by automatically passing the entire request to your Lambda function and expecting a properly formatted response, reducing the need for manual request/response transformations.
{{% /notice %}}