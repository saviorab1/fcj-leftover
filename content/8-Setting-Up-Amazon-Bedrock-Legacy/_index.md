---
title : "Setting Up Amazon Bedrock (Legacy)"
date : "2023-12-01T00:00:00Z"
weight : 8
chapter : false
pre : " <b> 8. </b> "
---

**Content:**
- [Request Model Access](8.1-request-model-access/)
- [Setup Fallback Region](8.2-setup-fallback-region/)
- [Configure Backend Integration](8.3-configure-backend-integration/)
- [Update Data Schema](8.4-update-data-schema/)

Amazon Bedrock provides access to foundation models from leading AI companies through a fully managed service. In this section, we'll set up Bedrock integration using the legacy approach with direct HTTP data sources and custom resolvers.

#### Request Model Access

1. Access the Amazon Bedrock console and navigate to the Model Catalog.
2. Request access to Claude 3.5 Sonnet model in your primary region.
3. Configure model permissions and wait for approval.

#### Setup Fallback Region

1. Configure model access in a secondary region for redundancy.
2. Set up the same Claude 3.5 Sonnet model in the fallback region.
3. Verify both regions have active model access.

#### Configure Backend Integration

1. Update the Amplify backend configuration with Bedrock data sources.
2. Configure HTTP data sources for both primary and fallback regions.
3. Set up IAM permissions for model invocation.

#### Update Data Schema

1. Create custom resolver functions for Bedrock integration.
2. Update the data schema with Bedrock query definitions.
3. Configure authentication and response handling.