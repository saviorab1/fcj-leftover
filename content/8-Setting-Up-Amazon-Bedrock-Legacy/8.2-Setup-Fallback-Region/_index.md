---
title : "Setup Fallback Region"
date : "2025-08-10T20:24:00Z"
weight : 2
chapter : false
pre : " <b> 8.2 </b> "
---

#### Configure Secondary Region

Set up a fallback region to ensure high availability and redundancy for your Bedrock integration.

#### Switch to Fallback Region

1. In the AWS Console, change your region to a secondary region (e.g., **ap-northeast-1**).
2. Navigate to **Amazon Bedrock** in the new region.
3. Access the **Model Catalog** as you did in the primary region.

![Fallback Region](/images/8/8-10.png?featherlight=false&width=90pc)

#### Request Model Access in Fallback Region

Follow the same process as the primary region:

1. Navigate to **Model Catalog**.
2. Select **Claude 3.5 Sonnet** from Anthropic.
3. Click **Modify model access** or **Enable specific model**.
4. Select Claude 3.5 Sonnet and submit the request.

![Fallback Region](/images/8/8-11.png?featherlight=false&width=90pc)
#### Wait for Approval

1. Monitor the approval status in the fallback region.
2. Ensure the model becomes available before proceeding.
3. Verify that both regions now have active Claude 3.5 Sonnet access.
4. 
![Fallback Region](/images/8/8-12.png?featherlight=false&width=90pc)

#### Document Region Information

Keep track of your configured regions:
- **Primary Region**: `ap-southeast-1` (Singapore)
- **Fallback Region**: `ap-northeast-1` (Tokyo)

{{% notice tip %}}
Choose regions that are geographically close to your users for optimal performance, while ensuring both regions support the Claude 3.5 Sonnet model.
{{% /notice %}}

#### Verify Multi-Region Setup

1. Switch between regions in the AWS Console.
2. Confirm Claude 3.5 Sonnet is available in both regions.
3. Note the model ARNs for each region (you'll need these later).

#### Result

You now have Claude 3.5 Sonnet access configured in both primary and fallback regions, providing redundancy for your application.
