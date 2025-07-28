---
title : "Create and Implement API"
date : "2023-12-01T00:00:00Z"
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

## Content

- [Create a REST API with API Gateway](#create-a-rest-api-with-api-gateway)
- [Update project’s codebase to work with new changes](#update-projects-codebase-to-work-with-new-changes)

## Create a REST API with API Gateway

Go to API Gateway console → Create API → REST API → Build

 ![Logo](/images/5/16-1.png?featherlight=false&width=90pc)

•	API name: leftover-data-collection-api
•	Endpoint type: Regional

 ![Logo](/images/5/16-2.png?featherlight=false&width=90pc)

On the left handside, click Create resource and fill in these info:
•	Create resource: /collect-data
•	CORS: Enable

 ![Logo](/images/5/16-3.png?featherlight=false&width=90pc)

Then on the right handside, click Create method with these settings:
•	Create method: POST
•	Integration type: Lambda Function
•	Lambda function: leftover-data-collector
•	Use Lambda Proxy integration: Yes

 ![Logo](/images/5/16-4.png?featherlight=false&width=90pc)

Click on the resource directory we just made to enable CORS by following these steps:
•	Select the POST method
•	Actions → Enable CORS
•	Access-Control-Allow-Origin: *
•	Access-Control-Allow-Headers: Content-Type,X-Amz-Date,Authorization,X-Api-Key,X-Amz-Security-Token

 ![Logo](/images/5/16-5.png?featherlight=false&width=90pc)
 ![Logo](/images/5/16-6.png?featherlight=false&width=90pc)

Then click Deploy API with stage name of your choice:

## Update project’s codebase to work with new changes

In App.tsx, incorporate these new lines of code to the existing one:

```tsx
// ... existing imports ...
import { getCurrentUser } from 'aws-amplify/auth';

// ... existing code ...

function App() {
  // ... existing state variables ...
  
  // Add this new function for data collection
  const collectUserData = async (ingredients: string) => {
    try {
      const user = await getCurrentUser();
      const sessionId = `session_${Date.now()}_${Math.random().toString(36).substr(2, 9)}`;
      
      const dataPayload = {
        ingredients,
        timestamp: new Date().toISOString(),
        userId: user.userId || 'anonymous',
        sessionId
      };

      // Replace YOUR_API_GATEWAY_URL with the actual URL from step 15
      await fetch('YOUR_API_GATEWAY_URL/collect-data', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(dataPayload)
      });
    } catch (error) {
      // Silently fail - don't disrupt user experience
      console.log('Data collection failed:', error);
    }
  };

  const onSubmit = async (event: FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    if (!inputValue.trim()) return;
    
    setLoading(true);
    setResult("");
    setError(null);
    setUsingFallback(false);

    try {
      const ingredientsInput = inputValue.trim();
      
      // Collect user data (fire and forget)
      collectUserData(ingredientsInput);
      
      const ingredientsArray = ingredientsInput
        .split(",")
        .map(ingredient => ingredient.trim())
        .filter(ingredient => ingredient.length > 0);
      
      // ... rest of existing onSubmit logic remains the same ...

```

I have commented all necessary information on what each part of the code should do. However, it will now run out of the box, you should replace the API Gateway URL yourself. You can expect to find it in the ARN box in POST method.

 ![Logo](/images/5/17-1.png?featherlight=false&width=90pc)