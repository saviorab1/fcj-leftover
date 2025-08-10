---
title : "Request Cross-Region Model Access"
date : "2025-08-10T20:24:00Z"
weight : 1
chapter : false
pre : " <b> 9.1 </b> "
---

#### Access Amazon Bedrock Console

Similar to the legacy approach, you need to request model access, but this time for Claude 4 Sonnet with cross-region inference capabilities.

#### Navigate to Model Catalog

1. Open the AWS Management Console and search for **Amazon Bedrock**.
2. Click on **Amazon Bedrock** to access the service.
3. Navigate to **Model Catalog** in the left sidebar.

![Bedrock Console](/images/9/9-1.png?featherlight=false&width=90pc)

#### Select Claude 4 Sonnet Model

1. Browse the available models in the catalog.
2. Locate **Claude 4 Sonnet** from Anthropic.
3. Note that this model supports **cross-region inference**.

![Model Selection](/images/9/9-2.png?featherlight=false&width=90pc)

{{% notice info %}}
Claude 4 Sonnet is available in ap-southeast-1 region and supports cross-region inference, providing automatic failover and load balancing across multiple regions.
{{% /notice %}}

#### Request Model Access

Choose your preferred access method:

**Enable All Models**:
- Enables access to all foundation models in the region
- No charges until models are actually used
- Can be harder to manage and track usage

![Model Access Options](/images/9/9-3.png?featherlight=false&width=90pc)

**Enable Specific Models** (Recommended):
- Select only Claude 4 Sonnet for better control
- Easier to track usage and manage permissions
- More cost-effective approach

![Model Access Options](/images/9/9-4.png?featherlight=false&width=90pc)

#### Configure Model Access

1. Select **Claude 4 Sonnet** from the available models list.
2. Review the model details and cross-region capabilities.
3. Complete any required use case information for Anthropic models.
4. Click **Submit** to request access.

![Configure Access](/images/9/9-5.png?featherlight=false&width=90pc)

#### Access Cross-Region Interface

1. After model approval, navigate to **Cross-Region Inference**.
2. You'll find the inference profile ARN and available regions.
3. Note the **Inference Profile ID** for later configuration.

![Cross-Region Interface](/images/9/9-6.png?featherlight=false&width=90pc)

#### Verify Cross-Region Setup

1. Confirm Claude 4 Sonnet is available with cross-region support.
2. Copy the **Inference Profile ID** (e.g., `apac.anthropic.claude-sonnet-4-20250514-v1:0`).
3. Note the supported regions for automatic routing.

{{% notice tip %}}
The cross-region inference profile automatically handles region selection and failover, eliminating the need to manually configure multiple regional endpoints.
{{% /notice %}}

#### Result

You now have Claude 4 Sonnet access with cross-region inference capabilities, ready for backend configuration.
