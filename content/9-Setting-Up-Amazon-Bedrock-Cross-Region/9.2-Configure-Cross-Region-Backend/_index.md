---
title : "Configure Cross-Region Backend"
date : "2025-08-10T20:24:00Z"
weight : 2
chapter : false
pre : " <b> 9.2 </b> "
---

#### Update Amplify Backend Configuration

Configure your Amplify backend to use cross-region inference with automatic routing and failover capabilities.

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

// Use the latest Claude 4.0 model with cross-region inference
const crossRegionModelId = "apac.anthropic.claude-sonnet-4-20250514-v1:0"; // Inference profile ID
const regionalModelId = "anthropic.claude-sonnet-4-20250514-v1:0"; // Bedrock model ID

// Primary region - Cross-region inference will handle routing automatically
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

// Grant permissions for cross-region inference profile
bedrockDataSource.grantPrincipal.addToPrincipalPolicy(
  new PolicyStatement({
    resources: [
      // Cross-region inference profile
      `arn:aws:bedrock:ap-southeast-1:<UserID>:inference-profile/${crossRegionModelId}`,
      // Regional model as fallback
      `arn:aws:bedrock:ap-southeast-1::foundation-model/${regionalModelId}`,
      // Additional regions that might be used by cross-region inference
      `arn:aws:bedrock:ap-northeast-1::foundation-model/${regionalModelId}`,
      `arn:aws:bedrock:ap-southeast-2::foundation-model/${regionalModelId}`,
      `arn:aws:bedrock:ap-northeast-2::foundation-model/${regionalModelId}`,
      `arn:aws:bedrock:ap-northeast-3::foundation-model/${regionalModelId}`,
      // Add wildcard for cross-region inference to handle all regions
      `arn:aws:bedrock:*::foundation-model/${regionalModelId}`,
    ],
    actions: ["bedrock:InvokeModel", "bedrock:InvokeModelWithResponseStream"],
  })
);
```

#### Configuration Details

**Model IDs**:
- `crossRegionModelId`: Inference profile ID for automatic routing
- `regionalModelId`: Base model ID used across regions

**Permission Strategy**:
- **Specific Regions**: List individual regions for controlled access
- **Wildcard Access**: Use `*` for all regions (simpler but broader permissions)

#### Regional Configuration Options

**Option 1: Specific Regional Order**
```ts
// Define specific region priority
`arn:aws:bedrock:ap-southeast-1::foundation-model/${regionalModelId}`, // Primary
`arn:aws:bedrock:ap-northeast-1::foundation-model/${regionalModelId}`, // Secondary
`arn:aws:bedrock:ap-southeast-2::foundation-model/${regionalModelId}`, // Tertiary
```

**Option 2: All Subscribed Regions**
```ts
// Allow access to all regions
`arn:aws:bedrock:*::foundation-model/${regionalModelId}`,
```

#### Update Data Schema

Replace the content of `amplify/data/resource.ts`:

```ts
import { type ClientSchema, a, defineData } from "@aws-amplify/backend";

const schema = a.schema({
  BedrockResponse: a.customType({
    body: a.string(),
    error: a.string(),
  }),

  askBedrock: a
    .query()
    .arguments({ 
      ingredients: a.string().array()
    })
    .returns(a.ref("BedrockResponse"))
    .authorization((allow) => [allow.authenticated()])
    .handler(
      a.handler.custom({ entry: "./bedrock.js", dataSource: "bedrockDS" })
    ),
});

export type Schema = ClientSchema<typeof schema>;

export const data = defineData({
  schema,
  authorizationModes: {
    defaultAuthorizationMode: "apiKey",
    apiKeyAuthorizationMode: {
      expiresInDays: 30,
    },
  },
});
```

#### Create Cross-Region Resolver

Create `amplify/data/bedrock.js` with cross-region support:

```js
export function request(ctx) {
  const { ingredients = [] } = ctx.args;

  // Construct the prompt with the provided ingredients
  const prompt = `Suggest a recipe idea using these ingredients (Please provide a recipe with the language used in the input ingredients. Provide 2 to 3 different recipes if possible): ${ingredients.join(", ")}.`;

  // Use cross-region inference profile for automatic region routing
  const modelId = "apac.anthropic.claude-sonnet-4-20250514-v1:0";

  // Return the request configuration
  return {
    resourcePath: `/model/${modelId}/invoke`,
    method: "POST",
    params: {
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        anthropic_version: "bedrock-2023-05-31",
        max_tokens: 1000,
        temperature: 0.4,
        messages: [
          {
            role: "user",
            content: [
              {
                type: "text",
                text: prompt,  
              },
            ],
          },
        ],
      }),
    },
  };
}

export function response(ctx) {
  // Parse the response body
  const parsedBody = JSON.parse(ctx.result.body);
  
  // Handle potential errors
  if (parsedBody.error) {
    return {
      error: parsedBody.error.message || "Model invocation failed"
    };
  }
  
  // Extract the text content from the response
  const res = {
    body: parsedBody.content && parsedBody.content[0].text, 
  };
  
  // Return the response
  return res;
}
```

{{% notice warning %}}
Replace `<UserID>` in the inference profile ARN with your actual AWS account ID. You can find this in the Cross-Region Interface section of the Bedrock console.
{{% /notice %}}

#### Understanding Token Counts

Large Language Models (LLMs) are billed and limited by tokens, not characters. Both your inputs (for example, the `messages` you send, including the constructed `prompt`) and the model’s outputs (the generated recipe text) consume tokens. The `max_tokens` parameter caps output tokens only.

To estimate usage and plan costs, you can use the Token Calculator for LLMs: [https://token-calculator.net](https://token-calculator.net). It approximates token counts for popular models and includes reference pricing tables to help with budgeting and capacity planning.


#### Result

Your backend is now configured for cross-region inference with automatic routing, failover capabilities, and simplified management compared to the legacy approach.
