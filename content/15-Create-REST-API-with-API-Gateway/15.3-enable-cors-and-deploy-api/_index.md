---
title : "Enable CORS and Deploy API"
date : "2025-08-10T20:24:00Z"
weight : 3
chapter : false
pre : " <b> 15.3 </b> "
---

Configure Cross-Origin Resource Sharing (CORS) to allow your web application to communicate with the API, then deploy the API for production use.

#### Enable CORS Configuration

1. Select the `/collect-data` resource and choose **POST** method on the right
2. Select **Enable CORS** from the **Resource details** menu

![Enable CORS](/images/15/15-10.png?featherlight=false&width=90pc)

#### Configure CORS Settings

1. **Access-Control-Allow-Methods**: Ensure **POST** is selected
2. **Access-Control-Allow-Headers**: Enter the following headers:
   ```
   Content-Type,X-Amz-Date,Authorization,X-Api-Key,X-Amz-Security-Token
   ```
3. **Access-Control-Allow-Origin**: Enter `*` to allow requests from any origin

![CORS Configuration](/images/15/15-11.png?featherlight=false&width=90pc)

#### Deploy API

1. Click **Deploy API** from the Actions menu
2. **Deployment stage**: Select **[New Stage]**
3. **Stage name**: Enter a descriptive name (e.g., `prod`, `dev`, or `v1`)
4. **Stage description**: Optional - Add deployment notes
5. Click **Deploy** to make your API live

![Deploy API](/images/15/15-12.png?featherlight=false&width=90pc)

#### Retrieve API Endpoint URL

1. After deployment, navigate to the **Stages** section
2. Select your deployed stage
3. Copy the **Invoke URL** - this is your API Gateway endpoint
4. The complete endpoint will be: `[Invoke URL]/collect-data`

![API Endpoint URL](/images/15/15-13.png?featherlight=false&width=90pc)

#### Result

Your REST API is now deployed and accessible via the generated endpoint URL. The CORS configuration allows your web application to make cross-origin requests, and the API is ready to receive POST requests for data collection.

{{% notice warning %}}
Save the API Gateway endpoint URL as you'll need it in the next step to integrate with your frontend application. The URL format will be similar to: `https://xxxxxxxxxx.execute-api.region.amazonaws.com/stage-name`
{{% /notice %}}

{{% notice tip %}}
For production environments, consider restricting the `Access-Control-Allow-Origin` to your specific domain instead of using `*` for enhanced security.
{{% /notice %}}
