---
title : "Integrate API with Frontend"
date : "2023-12-01T00:00:00Z"
weight : 4
chapter : false
pre : " <b> 15.4 </b> "
---

Update your React application to include data collection functionality that sends user interactions to your newly created API Gateway endpoint.

#### Update App.tsx Imports

Add the necessary import for user authentication at the top of your `src/App.tsx` file:

```typescript
// ... existing imports ...
import { getCurrentUser } from 'aws-amplify/auth';
```

![Import Addition](/images/15/15-14.png?featherlight=false&width=90pc)

#### Add Data Collection Function

Insert the following data collection function within your `App()` component, before the existing `onSubmit` function:

```typescript
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

    // Replace YOUR_API_GATEWAY_URL with the actual URL from step 15.3
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
```

![Data Collection Function](/images/15/15-15.png?featherlight=false&width=90pc)

#### Update onSubmit Function

Modify your existing `onSubmit` function to include the data collection call. Add this line after the `ingredientsInput` variable declaration:

```typescript
const onSubmit = async (event: FormEvent<HTMLFormElement>) => {
  event.preventDefault();
  if (!inputValue.trim()) return;
  
  setLoading(true);
  setResult("");
  setError(null);

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

![OnSubmit Integration](/images/15/15-16.png?featherlight=false&width=90pc)

#### Replace API Gateway URL

1. Locate the line containing `YOUR_API_GATEWAY_URL` in the `collectUserData` function
2. Replace `YOUR_API_GATEWAY_URL` with your actual API Gateway endpoint from Step 15.3
3. The URL should look like: `https://xxxxxxxxxx.execute-api.region.amazonaws.com/stage-name`

**Example replacement:**
```typescript
// Before
await fetch('YOUR_API_GATEWAY_URL/collect-data', {

// After  
await fetch('https://abc123def4.execute-api.us-east-1.amazonaws.com/prod/collect-data', {
```

#### Test Integration

1. Save your changes and ensure your development server is running
2. Test the application by entering ingredients and submitting a recipe request
3. Check the browser's developer console for any data collection errors
4. Verify that data is being sent to your Lambda function through CloudWatch logs

![Testing Integration](/images/15/15-4-5.png?featherlight=false&width=90pc)

#### Result

Your React application now automatically collects user interaction data including ingredients, timestamps, user IDs, and session information. This data is sent to your API Gateway endpoint and processed by your Lambda function for storage and analysis.

**Data Collection Features:**
- **Automatic Tracking**: Captures every recipe generation request
- **User Identification**: Links data to authenticated users when available
- **Session Management**: Generates unique session IDs for analytics
- **Error Handling**: Fails silently to maintain user experience
- **Timestamp Recording**: Tracks when interactions occur

{{% notice warning %}}
Ensure you replace `YOUR_API_GATEWAY_URL` with your actual API Gateway endpoint URL. The application will not collect data properly without the correct endpoint configuration.
{{% /notice %}}

{{% notice info %}}
The data collection runs asynchronously and won't affect the user experience if the API call fails. This "fire and forget" approach ensures recipe generation continues smoothly even if data collection encounters issues.
{{% /notice %}}