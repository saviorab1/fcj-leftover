---
title : "Update Frontend Integration"
date : "2023-12-01T00:00:00Z"
weight : 3
chapter : false
pre : " <b> 9.3 </b> "
---

#### Implement Frontend Application

Update your React application to integrate with the cross-region Bedrock implementation.

#### Update App Component

Replace the content of `src/App.tsx` with the following enhanced implementation:

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

#### Key Implementation Features

**Cross-Region Benefits**:
- **Automatic Routing**: Bedrock handles region selection automatically
- **Improved Reliability**: Built-in failover across multiple regions
- **Simplified Configuration**: Single inference profile instead of multiple endpoints
- **Better Performance**: Automatic load balancing and latency optimization

**Error Handling**:
- 30-second timeout for API requests
- Comprehensive error logging and user feedback
- Graceful fallback for service unavailability

**User Experience**:
- Multilingual support for ingredient input
- Real-time loading indicators with placeholders
- Responsive design with animations
- Clear error messages and status updates

#### Cost Estimation

To calculate the cost of using Claude 4 Sonnet with cross-region inference:

1. Visit the [AWS Bedrock Pricing page](https://aws.amazon.com/bedrock/pricing/)
2. Select your region (Asia Pacific) and model (Claude 4 Sonnet by Anthropic)
3. Use the formula: ***(0.003 × input tokens / 1000) + (0.015 × output tokens / 1000)***

![Cost Calculation](/images/9/9-7.png?featherlight=false&width=90pc)

#### Deploy and Test

1. Save all files and commit changes to Git:
   ```bash
   git add .
   git commit -m "Implement cross-region Bedrock inference"
   git push
   ```

2. Test the application with various ingredient combinations
3. Monitor the console for cross-region routing behavior
4. Verify automatic failover functionality

#### Result

Your application now uses Amazon Bedrock's Cross-Region Inference for:
- **Enhanced Reliability**: Automatic failover across multiple regions
- **Simplified Management**: Single configuration for multi-region access
- **Improved Performance**: Optimized routing and load balancing
- **Better User Experience**: Consistent response times and availability

{{% notice note %}}
Cross-Region Inference provides the most robust and production-ready implementation for Bedrock integration, making it the recommended approach for this project.
{{% /notice %}}