---
title : "Configure Backend Integration"
date : "2025-08-10T20:24:00Z"
weight : 3
chapter : false
pre : " <b> 8.3 </b> "
---

#### Update Amplify Backend Configuration

Configure your Amplify backend to integrate with Amazon Bedrock using HTTP data sources.

#### Locate Backend Configuration

1. Navigate to your project's `amplify/` directory.
2. Open the `backend.ts` file in your code editor.
3. This file defines your backend resources and configurations.

#### Update Backend Configuration

Replace the content of `amplify/backend.ts` with the following code:

```ts
import { defineBackend } from "@aws-amplify/backend";
import { data } from "./data/resource";
import { PolicyStatement } from "aws-cdk-lib/aws-iam";
import { auth } from "./auth/resource";

const backend = defineBackend({
  auth,
  data,
});

// Primary region
const bedrockDataSource = backend.data.resources.graphqlApi.addHttpDataSource(
  "bedrockDS",
  "https://bedrock-runtime.ap-southeast-1.amazonaws.com",
  {
    authorizationConfig: {
      signingRegion: "ap-southeast-1",
      signingServiceName: "bedrock",
    },
  }
);

// Fallback region
const bedrockFallbackDataSource = backend.data.resources.graphqlApi.addHttpDataSource(
  "bedrockFallbackDS",
  "https://bedrock-runtime.ap-northeast-1.amazonaws.com",
  {
    authorizationConfig: {
      signingRegion: "ap-northeast-1",
      signingServiceName: "bedrock",
    },
  }
);

// Grant permissions for primary region
bedrockDataSource.grantPrincipal.addToPrincipalPolicy(
  new PolicyStatement({
    resources: [
      "arn:aws:bedrock:ap-southeast-1::foundation-model/anthropic.claude-3-5-sonnet-20240620-v1:0",
    ],
    actions: ["bedrock:InvokeModel"],
  })
);

// Grant permissions for fallback region
bedrockFallbackDataSource.grantPrincipal.addToPrincipalPolicy(
  new PolicyStatement({
    resources: [
      "arn:aws:bedrock:ap-northeast-1::foundation-model/anthropic.claude-3-5-sonnet-20240620-v1:0",
    ],
    actions: ["bedrock:InvokeModel"],
  })
);
```

#### Find Model ARN

To get the correct Model ARN for your regions:

1. Go to **Amazon Bedrock** → **Model Catalog**.
2. Filter by **Anthropic** and select **Claude 3.5 Sonnet**.
3. Switch to your target region and copy the **Model ID**.

![Model ARN](/images/8/8-13.png?featherlight=false&width=90pc)

#### Update Region-Specific ARNs

For models like Claude 3.5 Sonnet that don't display the full ARN:

1. Change to the correct region in the console.
2. Copy the **Model ID** from the model details.
3. Replace the model ID in the ARN format:
   ```
   arn:aws:bedrock:REGION::foundation-model/MODEL_ID
   ```

#### Configuration Details

**HTTP Data Sources**:
- `bedrockDS`: Primary region endpoint (ap-southeast-1)
- `bedrockFallbackDS`: Fallback region endpoint (ap-northeast-1)

**IAM Permissions**:
- `bedrock:InvokeModel`: Allows calling the specified foundation models
- Region-specific ARNs ensure access to models in both regions

{{% notice warning %}}
Ensure the regions in your backend configuration match the regions where you requested model access.
{{% /notice %}}

#### Result

Your Amplify backend is now configured with Bedrock HTTP data sources and proper IAM permissions for both primary and fallback regions.
