---
title : "Create REST API"
date : "2025-08-10T20:24:00Z"
weight : 1
chapter : false
pre : " <b> 15.1 </b> "
---

Setting up a REST API through Amazon API Gateway provides a secure and scalable endpoint for collecting user data from your recipe application.

#### Navigate to API Gateway Console

1. Open the **AWS Management Console** and search for **API Gateway**
2. In the API Gateway console, click **Create API**

![API Gateway Console](/images/15/15-1.png?featherlight=false&width=90pc)

3. Select **REST API** and click **Build** to proceed with configuration

![Select REST API](/images/15/15-2.png?featherlight=false&width=90pc)

#### Configure API Settings

1. **API name**: Enter `leftover-data-collection-api`
2. **Description**: Optional - Add a description for the data collection API
3. **Endpoint type**: Select **Regional** for optimal performance in your region

![API Configuration](/images/15/15-3.png?featherlight=false&width=90pc)

#### Create API

1. Review your configuration settings
2. Click **Create API** to establish the REST API foundation
3. The API Gateway console will display your newly created API dashboard

![API Creation Complete](/images/15/15-4.png?featherlight=false&width=90pc)

#### Result

Your REST API foundation is now established with the name `leftover-data-collection-api` and configured as a regional endpoint. The next step will focus on creating the necessary resources and methods for data collection functionality.

{{% notice note %}}
Regional endpoints provide lower latency for users in the same AWS region as your API, making them ideal for applications with geographically concentrated users.
{{% /notice %}}
