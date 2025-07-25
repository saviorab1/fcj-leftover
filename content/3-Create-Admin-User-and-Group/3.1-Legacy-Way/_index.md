---
title : "Setting up AWS Bedrock (Legacy)"
date : "2023-12-01T00:00:00Z"
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---

## Content
- [Request an AWS Bedrock Model](#request-an-aws-bedrock-model)
- [Choosing the AI Model inside Bedrock](#choosing-the-ai-model-inside-bedrock)
- [Make a fallback server](#make-a-fallback-server)
- [Request an AWS Bedrock Model](#request-an-aws-bedrock-model)

## Request an AWS Bedrock Model

You will need to get to Amazon Bedrock and click on Model Catalog. 

You will be greeted by one of those two pages. In either way, click on the mark part of the image.

 ![IAM Frontpage](/images/3/8-0.png?featherlight=false&width=90pc)

 ![IAM Frontpage](/images/3/8-0-1.png?featherlight=false&width=90pc)

Afterward, click on the AI model and click on Modify Access.

 ![IAM Frontpage](/images/3/8-1.png?featherlight=false&width=90pc)


## Choosing the AI Model inside Bedrock

In this case, we will choose Claude 3.5 Sonnet as it is readily available at ap-southeast-1 region. You can check the availability of AI models within each region via this link: https://docs.aws.amazon.com/bedrock/latest/userguide/models-regions.html

First, you will need to choose to modify the Model Access. There are two scenarios:

This is the scenario where you have not modfiy any model access into Amazon Bedrock. If you are in this case, choose **Modify model access**.

 ![IAM Frontpage](/images/3/8-2.png?featherlight=false&width=90pc)

This is the scenario where you have modfiy any model access into Amazon Bedrock. If you are in this case, choose **Enable Specific Model**.

 ![IAM Frontpage](/images/3/8-3.png?featherlight=false&width=90pc)

After that, choose the model that you want, and in this case, it is Claude Sonnet 3.5.

 ![IAM Frontpage](/images/3/8-4.png?featherlight=false&width=90pc)

Hit Submit after, nothing much will need to be changed. 

 ![IAM Frontpage](/images/3/8-5.png?featherlight=false&width=90pc)

You will need to wait for a while for the model to finish setting up. You should see this screen.

 ![IAM Frontpage](/images/3/8-6.png?featherlight=false&width=90pc)

# Make a fallback server

We will need a fallback server since it acts like a backup server whether our main server shutdown. You will create it using another region and follow the same steps as up there.

 ![IAM Frontpage](/images/3/9-1.png?featherlight=false&width=90pc)

# Integrate and invoke Bedrock Models to be used in our project

We will need to integrate the models. Remember the two regions that you have used to make the Bedrock Models. Remember to check those. 

 ![IAM Frontpage](/images/3/10-0.png?featherlight=false&width=90pc)

Afterward, get to amplify folder, look for **backend.ts** and update it with these lines of codes:

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
Now, Update the corresponding region for all requested models.

You will need to find the model ARN next to put in. To find the link, you will once again click on Model Catalog -> Choose Anthropic on Filter and click on Claude Sonnet 3.5 or the model that you have chosen.

 ![IAM Frontpage](/images/3/10-1.png?featherlight=false&width=90pc)

Scroll down or search around. Some models such as Karakuri or Liquid will have their own line of Model ARN and all user has to do is copy that line to resources.

 ![IAM Frontpage](/images/3/10-2.png?featherlight=false&width=90pc)

However, since we do not have that luxury with Claude 3.5 Sonnet, we have to be smart about the approach. First off, we have to change to the correct region for the ARN then copy the Model ID to replace the one at the end of that line.

 ![IAM Frontpage](/images/3/10-3.png?featherlight=false&width=90pc)

To grant permission for each models, you have to update the corresponding ARN in the PolicyStatement.

 ![IAM Frontpage](/images/3/10-4.png?featherlight=false&width=90pc)

Go to amplify/data folder and create a new file called **bedrock.js** and paste in these lines of codes.

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

These might be long but there are only a few you have to beware of:
•	prompt: you can construct a custom prompt prior to the user’s input to keep it consistent with what you want users to experience. (Albeit, you can just skip this all together and type it in text under content).
•	resourcePath: input the model you want to use, just copy the Model ID and put it between /model/****/invoke
•	max_tokens: the maximum sequence of characters each user can input.
•	temperature: dictate the randomness of output response.
•	type: what type of data you want to send. It can either be text or image.

In amplify/data folder, update resource.ts with these lines of codes:

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