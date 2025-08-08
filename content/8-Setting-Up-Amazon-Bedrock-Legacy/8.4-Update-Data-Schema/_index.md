---
title : "Update Data Schema"
date : "2023-12-01T00:00:00Z"
weight : 4
chapter : false
pre : " <b> 8.4 </b> "
---

#### Create Custom Resolver Function

Create a custom resolver to handle Bedrock API requests and responses.

#### Create Bedrock Resolver

1. Navigate to the `amplify/data/` directory.
2. Create a new file named `bedrock.js`.
3. Add the following resolver code:

```js
export function request(ctx) {
    const { ingredients = [], useFallback } = ctx.args;
  
    // Construct the prompt with the provided ingredients
    const prompt = `Suggest a recipe idea using these ingredients (Please provide a recipe with the language used in the input ingredients. Provide 2 to 3 different recipes if possible): ${ingredients.join(", ")}.`;
  
    // Determine which endpoint to use based on the useFallback parameter
    // If useFallback is undefined or false, use the primary endpoint
    const endpoint = useFallback === true
      ? "bedrockFallbackDS" // Use fallback
      : "bedrockDS";        // Use primary
  
    // Return the request configuration
    return {
      resourcePath: `/model/anthropic.claude-3-5-sonnet-20240620-v1:0/invoke`,
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
                  text: `\n\nHuman: ${prompt}\n\nAssistant:`,
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
    // Extract the text content from the response
    const res = {
      body: parsedBody.content[0].text,
    };
    // Return the response
    return res;
  }
```

#### Resolver Configuration Parameters

**Key Parameters**:
- **prompt**: Custom prompt construction for recipe suggestions
- **resourcePath**: Model endpoint path with Model ID
- **max_tokens**: Maximum response length (1000 characters)
- **temperature**: Response randomness (0.4 for balanced creativity)
- **type**: Data type being sent (text in this case)

#### Update Data Schema

Replace the content of `amplify/data/resource.ts` with:

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
      ingredients: a.string().array(),
      useFallback: a.boolean()
    })
    .returns(a.ref("BedrockResponse"))
    .authorization((allow) => [allow.authenticated()])
    .handler(
      a.handler.custom({ entry: "./bedrock.js", dataSource: "bedrockDS" })
    ),
    
  askBedrockFallback: a
    .query()
    .arguments({ 
      ingredients: a.string().array() 
    })
    .returns(a.ref("BedrockResponse"))
    .authorization((allow) => [allow.authenticated()])
    .handler(
      a.handler.custom({ entry: "./bedrock.js", dataSource: "bedrockFallbackDS" })
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

#### Schema Components

**Custom Types**:
- `BedrockResponse`: Defines the structure of Bedrock API responses

**Queries**:
- `askBedrock`: Primary query with fallback option
- `askBedrockFallback`: Dedicated fallback query

**Authorization**:
- `allow.authenticated()`: Requires user authentication
- API key mode for development convenience

#### Deploy Changes

1. Save all files in the `amplify/` directory.
2. Commit your changes to Git:
   ```bash
   git add .
   git commit -m "Add Bedrock integration with fallback support"
   git push
   ```
3. The changes will be automatically deployed via Amplify.

#### Result

Your application now has complete Bedrock integration with:
- Custom resolver for recipe generation
- Primary and fallback region support
- Authenticated access to Claude 3.5 Sonnet
- Flexible prompt configuration

{{% notice note %}}
The schema update will create GraphQL queries that your frontend can use to interact with the Bedrock models for recipe generation.
{{% /notice %}}