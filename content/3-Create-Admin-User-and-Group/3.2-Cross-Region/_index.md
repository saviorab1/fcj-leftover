---
title : "Setting up AWS Bedrock (Cross-Region)"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

## Content
- [Request an AWS Bedrock Model](#request-an-aws-bedrock-model)
- [Choosing the AI Model inside Bedrock](#choosing-the-ai-model-inside-bedrock)
- [Make a fallback server](#make-a-fallback-server)
- [Request an AWS Bedrock Model](#request-an-aws-bedrock-model)

## Request an AWS Bedrock Model

Same as the Legacy Way, you will need to get to Amazon Bedrock and click on Model Catalog. 

You will be greeted by one of those two pages. In either way, click on the mark part of the image.

 ![IAM Frontpage](/images/3/8-0.png?featherlight=false&width=90pc)

 ![IAM Frontpage](/images/3/8-0-1.png?featherlight=false&width=90pc)

Afterward, click on the AI model and click on Modify Access.

 ![IAM Frontpage](/images/3/8-1.png?featherlight=false&width=90pc)

## Choosing the AI Model inside Bedrock

In this case, we will choose Claude 4 Sonnet as it is readily available at ap-southeast-1 region and **it has cross-region**. 

First, you will need to choose to modify the Model Access. There are two scenarios:

This is the scenario where you have not modfiy any model access into Amazon Bedrock. If you are in this case, choose **Modify model access**.

 ![IAM Frontpage](/images/3/8-2.png?featherlight=false&width=90pc)

This is the scenario where you have modfiy any model access into Amazon Bedrock. If you are in this case, choose **Enable Specific Model**.

 ![IAM Frontpage](/images/3/8-3.png?featherlight=false&width=90pc)

After that, choose the model that you want, and in this case, it is Claude Sonnet 4.

 ![IAM Frontpage](/images/3/8-4-Alternate.png?featherlight=false&width=90pc)

Hit Submit after, nothing much will need to be changed. You will need to wait for a while for the model to finish setting up. You should see this screen.

 ![IAM Frontpage](/images/3/8-5-Alternate.png?featherlight=false&width=90pc)

## Checking and implementing cross-region Model

You will be able to find the ARN Model as well as the available regions for the models by clicking on the Cross-Region Interface and scrolled down to the model you want. (In our case, Claude Sonnet 4.)

 ![IAM Frontpage](/images/3/8-6-Alternate.png?featherlight=false&width=90pc)

You can request the Claude Sonnet 4 to as many local zones as you want in the same Region.

## Integrate and invoke Bedrock Models to be used in our project

Then, go to your bedrock.js:

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

App.tsx:

```tsx
import type { FormEvent } from "react";
import { useState, useEffect } from "react";
import { Loader, Placeholder } from "@aws-amplify/ui-react";
import "./App.css";
import { Amplify } from "aws-amplify";
import type { Schema } from "../amplify/data/resource";
import { generateClient } from "aws-amplify/data";
import outputs from "../amplify_outputs.json";
import logoImage from "./assets/pics/logo.png";
import { signOut } from "aws-amplify/auth";

import "@aws-amplify/ui-react/styles.css";

Amplify.configure(outputs);

const amplifyClient = generateClient<Schema>({
  authMode: "userPool",
});

function App() {
  const [result, setResult] = useState<string>("");
  const [loading, setLoading] = useState(false);
  const [inputValue, setInputValue] = useState("");
  const [animateIntro, setAnimateIntro] = useState(false);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    // Trigger animation after component mounts
    setAnimateIntro(true);
  }, []);

  const callBedrockAPI = async (ingredients: string[]) => {
    // Create a promise that will reject after 30 seconds
    const timeout = new Promise<never>((_, reject) => {
      setTimeout(() => reject(new Error('Request timed out')), 30000);
    });
    
    try {
      console.log('Calling Bedrock API with cross-region inference, ingredients:', ingredients);
      const response = await Promise.race([
        amplifyClient.queries.askBedrock({ ingredients }),
        timeout
      ]);
      console.log('Received response:', response);
      
      // If we get here, API request completed before timeout
      if (!response.data) {
        throw new Error("No data returned from the API");
      }
      
      // Check if there's an error in the response
      if (response.data.error) {
        console.error('Bedrock API returned error:', response.data.error);
        console.error('Full response:', response);
        throw new Error(response.data.error);
      }
      
      // Check if body is empty or null
      if (!response.data.body) {
        throw new Error("Empty response body from the API");
      }
      
      return response.data.body;
    } catch (error) {
      // Re-throw the error to handle it in the calling function
      throw error;
    }
  };

  const onSubmit = async (event: FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    if (!inputValue.trim()) return;
    
    setLoading(true);
    setResult("");
    setError(null);

    try {
      const ingredientsInput = inputValue.trim();
      const ingredientsArray = ingredientsInput
        .split(",")
        .map(ingredient => ingredient.trim())
        .filter(ingredient => ingredient.length > 0);
      
      // Use cross-region inference - AWS Bedrock will handle routing automatically
      const resultText = await callBedrockAPI(ingredientsArray);
      setResult(resultText || "No recipe content returned");
      
    } catch (e) {
      console.error("Cross-region inference failed:", e);
      if (e instanceof Error) {
        setError(`Service error: ${e.message}`);
      } else {
        setError("Service is currently unavailable. Please try again later.");
      }
    } finally {
      setLoading(false);
    }
  };

  const handleInputChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    setInputValue(e.target.value);
  };

  const handleLogout = async () => {
    try {
      await signOut();
      // The Authenticator will handle the UI change automatically
    } catch (error) {
      console.error('Error signing out: ', error);
    }
  };

  return (
    <div className="app-container">
      <div className="nav-container">
        <button className="logout-button" onClick={handleLogout}>
          Log Out
        </button>
      </div>
      
      <div className={`header-container ${animateIntro ? 'fade-in' : ''}`}>
        <img src={logoImage} alt="Recipe AI Logo" className="logo" />
        <h1 className="main-header">
          Do you have some
          <br />
          <span className="highlight">Leftover?</span>
        </h1>
        <p className="description">
          Just type in any ingredients you have left in your fridge or pantry,
          separated by commas. We'll help you create a delicious recipe with what you already have!
          <br />
          <span className="multilingual-note">
            (Our website supports all languages, please input the ingredients in your language)
          </span>
        </p>
      </div>
      
      <form onSubmit={onSubmit} className={`form-container ${animateIntro ? 'slide-up' : ''}`}>
        <div className="search-container">
          <input
            type="text"
            className="wide-input"
            id="ingredients"
            name="ingredients"
            placeholder="Chicken, rice, carrots, onion..."
            value={inputValue}
            onChange={handleInputChange}
          />
          <button 
            type="submit" 
            className="search-button"
            disabled={loading || !inputValue.trim()}
          >
            {loading ? 'Processing...' : 'Generate'}
          </button>
        </div>
      </form>
      
      {(loading || result || error) && (
        <div className={`result-container ${result || loading || error ? 'appear' : ''}`}>
          {loading ? (
            <div className="loader-container">
              <p>Creating your personalized recipe...</p>
              <Loader size="large" />
              <Placeholder size="large" />
              <Placeholder size="large" />
              <Placeholder size="large" />
            </div>
          ) : error ? (
            <p className="result error-message">{error}</p>
          ) : (
            <p className="result">{result}</p>
          )}
        </div>
      )}
    </div>
  );
}

export default App;
```

resource.ts:

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

Bedrock.ts:

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
const crossRegionModelId = "apac.anthropic.claude-sonnet-4-20250514-v1:0"; //Declare the inference profile ID here
const regionalModelId = "anthropic.claude-sonnet-4-20250514-v1:0"; //Declare the Bedrock modelID here

// Primary region  - Cross-region inference will handle routing automatically
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

You will be able to find the Cross-Region interface profile ID here:

 ![IAM Frontpage](/images/3/8-7-Alternate.png?featherlight=false&width=90pc)

Going back to the code:

 ![IAM Frontpage](/images/3/8-7-1-Alternate.png?featherlight=false&width=90pc)

In the image above, you will need to specify the Cross Region Inference Profile first before the Region Model ID. You can add as many Regional Models as you want. Therefore, if you want to specify the order of region models that will be used for the project, you can write like this:

```bash

  // Regional model as fallback
  `arn:aws:bedrock:<The primary local zone>::foundation-model/${regionalModelId}`,
  // Additional regions that might be used by cross-region inference
  `arn:aws:bedrock:<The following local zone>::foundation-model/${regionalModelId}`,
  `arn:aws:bedrock:<The following local zone>::foundation-model/${regionalModelId}`,
  `arn:aws:bedrock:<The following local zone>::foundation-model/${regionalModelId}`,
  `arn:aws:bedrock:<The following local zone>::foundation-model/${regionalModelId}`,
…
```

Or if you want to use all of the subscribed Regional Models, then you can write like this:

```bash
`arn:aws:bedrock:*::foundation-model/${regionalModelId}`,
```

In the bedrock.js file, you will see these lines:

 ![IAM Frontpage](/images/3/8-8-Alternate.png?featherlight=false&width=90pc)

For the ModelID: Since we are using cross-region which is different from the legacy, we will need to define the inference region profile before the agent model. Then it can automatically route between different local zone within the region we defined in the backend.ts file. 

For the max_tokens: The maximum string output can a response generate. This will help us manage the estimation cost.

For the temperature: This is to dictate the randomness of a response. 

For the type: This is to define the type of content it will deliver.

For the text: This is to generate a prompt to the agent model. 

Furthermore, to calculate the estimation cost of the service, we will need to access to the AWS Price Estimation website **(https://aws.amazon.com/vi/bedrock/pricing/)** and check on the company, the area and the model that you are using for the project.

Example: Our project, which is located in the Asia Pacific region, developed by Anthropic and the model is Claude Sonnet 4, then you can calculate the price under this formula:

***(0.003 x (The number of input tokens) / 1000) + (0.015 x (The number of output tokens) / 1000)***

 ![IAM Frontpage](/images/3/8-9-Alternate.png?featherlight=false&width=90pc)

