---
title : "Setting Up Amazon Bedrock (Cross-Region Inference)"
date : "2025-08-10T20:24:00Z"
weight : 9
chapter : false
pre : " <b> 9. </b> "
---

**Content:**
- [Request Cross-Region Model Access](9.1-request-cross-region-model-access/)
- [Configure Cross-Region Backend](9.2-configure-cross-region-backend/)
- [Update Frontend Integration](9.3-update-frontend-integration/)

Amazon Bedrock Cross-Region Inference provides automatic routing and failover across multiple regions for improved availability and performance. This is the **main implementation approach** for this project, offering simplified configuration and better reliability compared to the legacy method.

{{% notice warning %}}
**Important**: Choose either Step 8 (Legacy) OR Step 9 (Cross-Region Inference). Do not mix implementations between these two approaches as they use different configuration patterns and may cause conflicts.
{{% /notice %}}

#### Request Cross-Region Model Access

1. Access Amazon Bedrock and request Claude 4 Sonnet model access.
2. Enable cross-region inference capabilities for the model.
3. Configure inference profiles for automatic region routing.

#### Configure Cross-Region Backend

1. Update Amplify backend with cross-region inference configuration.
2. Set up inference profile permissions and regional model access.
3. Configure automatic routing and failover mechanisms.

#### Update Frontend Integration

1. Implement the frontend application with cross-region support.
2. Update resolver functions for cross-region model invocation.
3. Configure error handling and timeout management.

{{% notice info %}}
Cross-Region Inference automatically handles region selection, load balancing, and failover, making it the recommended approach for production applications requiring high availability.
{{% /notice %}}
