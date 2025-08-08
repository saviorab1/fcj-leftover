---
title : "Request Model Access"
date : "2023-12-01T00:00:00Z"
weight : 1
chapter : false
pre : " <b> 8.1 </b> "
---

#### Access Amazon Bedrock Console

To use Amazon Bedrock models, you need to request access to specific foundation models in your AWS account.

#### Navigate to Model Catalog

1. Open the AWS Management Console and search for **Amazon Bedrock**.
2. Click on **Amazon Bedrock** to access the service.
3. Navigate to **Model Catalog** in the left sidebar.

![Bedrock Console](/images/8/8-1.png?featherlight=false&width=90pc)

#### Select Claude 3.5 Sonnet Model

1. Browse the available models in the catalog.
2. Locate **Claude 3.5 Sonnet** from Anthropic.
3. Click on the model to view its details.

![Model Selection](/images/8/8-2.png?featherlight=false&width=90pc)

{{% notice info %}}
Claude 3.5 Sonnet is readily available in the ap-southeast-1 region. Check the [AWS documentation](https://docs.aws.amazon.com/bedrock/latest/userguide/models-regions.html) for model availability in different regions.
{{% /notice %}}

#### Request Model Access

You have two options for enabling model access:

**Enable All Models**:
1. Click **Modify model access** and select all available models.
2. This enables access to all foundation models in the region.
3. **Cost**: No charges apply until you actually use the models.
4. **Management**: Can be harder to manage and track which models are being used.

![Enable All Models](/images/8/8-3.png?featherlight=false&width=90pc)

**Enable Specific Models**:
1. Click **Enable specific model** to choose individual models.
2. Select only the models you need (recommended approach).
3. **Cost**: Only pay for models you actually invoke.
4. **Management**: Easier to track usage and manage permissions.

![Enable Specific Models](/images/8/8-5.png?featherlight=false&width=90pc)

{{% notice tip %}}
For this workshop, we recommend **Enable Specific Models** and select only Claude 3.5 Sonnet to maintain better control and visibility over your model usage.
{{% /notice %}}

#### Configure Model Access

1. Select **Claude 3.5 Sonnet** from the available models list.
2. Review the model details and pricing information.
3. For Anthropic models, you'll be prompted to provide use case details.
![Use Case Details](/images/8/8-6.png?featherlight=false&width=90pc)

#### Provide Use Case Details

When requesting access to Anthropic models, fill in the required information:

**Company Information**:
- **Company Name**: Your organization or personal project name
- **Company Website URL**: Use your deployed Amplify application URL
- **Industry**: Select the most appropriate category for your use case

**Use Case Description**:
- **Primary Use Case**: Recipe generation and cooking assistance
- **Description**: AI-powered application that suggests recipes based on available ingredients
- **Expected Usage**: Development and testing purposes for educational workshop

![Use Case Details](/images/8/8-7.png?featherlight=false&width=90pc)

1. Click **Submit** to request access after completing the form.

![Submit Request](/images/8/8-8.png?featherlight=false&width=90pc)

#### Wait for Approval

1. The model access request will be processed.
2. You'll see a status indicating the request is being reviewed.
3. Wait for the approval process to complete.

![Access Pending](/images/8/8-9.png?featherlight=false&width=90pc)

#### Verify Access

Once approved, you should see:
- Model status showing as "Available" or "Enabled"
- Ability to invoke the model through API calls
- Access to model configuration options

#### Result

You now have access to Claude 3.5 Sonnet in your primary region and can proceed to set up the fallback region.