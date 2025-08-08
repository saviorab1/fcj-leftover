---
title : "Implement Main Application"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 10.2 </b> "
---

#### Build Complete React Application

Create the main application component with full functionality including API integration, error handling, and user interface.

#### Update App.tsx Component

Replace the content of `src/App.tsx` with the following comprehensive implementation:

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
  const [usingFallback, setUsingFallback] = useState(false);

  useEffect(() => {
    // Trigger animation after component mounts
    setAnimateIntro(true);
  }, []);

  const callBedrockAPI = async (ingredients: string[], useFallback = false) => {
    // Create a promise that will reject after 30 seconds
    const timeout = new Promise<never>((_, reject) => {
      setTimeout(() => reject(new Error('Request timed out')), 30000);
    });
    
    try {
      const response = await Promise.race([
        useFallback 
          ? amplifyClient.queries.askBedrockFallback({ ingredients })
          : amplifyClient.queries.askBedrock({ ingredients }),
        timeout
      ]);
      
      // If we get here, API request completed before timeout
      if (!response.data) {
        throw new Error("No data returned from the API");
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
    setUsingFallback(false);

    try {
      const ingredientsInput = inputValue.trim();
      const ingredientsArray = ingredientsInput
        .split(",")
        .map(ingredient => ingredient.trim())
        .filter(ingredient => ingredient.length > 0);
      
      try {
        // First try the primary region (ap-southeast-1)
        const resultText = await callBedrockAPI(ingredientsArray, false);
        setResult(resultText || "No recipe content returned");
      } catch (primaryError) {
        console.warn("Primary region failed, trying fallback:", primaryError);
        setUsingFallback(true);
        
        try {
          // If primary region fails, try the fallback region (ap-northeast-1)
          const fallbackResult = await callBedrockAPI(ingredientsArray, true);
          setResult(fallbackResult || "No recipe content returned");
        } catch (fallbackError) {
          // Both regions failed
          console.error("Both regions failed:", fallbackError);
          if (fallbackError instanceof Error) {
            setError(`Service unavailable: ${fallbackError.message}`);
          } else {
            setError("Service is unavailable in all regions. Please try again later.");
          }
        }
      }
    } catch (e) {
      console.error("Exception:", e);
      if (e instanceof Error) {
        setError(`An error occurred: ${e.message}`);
      } else {
        setError("An unknown error occurred. Please try again.");
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
            <>
              {usingFallback && (
                <p className="fallback-notice">Using fallback region (ap-northeast-1)</p>
              )}
              <p className="result">{result}</p>
            </>
          )}
        </div>
      )}
      
      <footer className="footer">
        © {new Date().getFullYear()} Aiden Dinh & Arthur Nguyen
      </footer>
    </div>
  );
}

export default App;
```

#### Key Application Features

**State Management**:
- `result`: Stores the generated recipe content
- `loading`: Manages loading state during API calls
- `inputValue`: Tracks user input for ingredients
- `animateIntro`: Controls entrance animations
- `error`: Handles error messages
- `usingFallback`: Indicates when fallback region is used

**API Integration**:
- **Primary Region**: First attempts API call to ap-southeast-1
- **Fallback Region**: Automatically tries ap-northeast-1 if primary fails
- **Timeout Handling**: 30-second timeout for all API requests
- **Error Recovery**: Comprehensive error handling with user feedback

**User Interface Components**:
- **Logo Integration**: Custom logo with hover effects
- **Responsive Form**: Input field with validation and submit button
- **Loading States**: Visual feedback during processing
- **Results Display**: Formatted recipe output with error handling
- **Authentication**: Logout functionality with Amplify integration

**Multilingual Support**:
- Accepts ingredients in any language
- Provides recipes in the same language as input
- Clear instructions for international users

{{% notice note %}}
This implementation works with both the Legacy (Step 8) and Cross-Region Inference (Step 9) approaches, automatically handling fallback scenarios for maximum reliability.
{{% /notice %}}

#### Result

Your application now has a complete, functional React component with professional error handling, fallback support, and a polished user interface ready for styling.