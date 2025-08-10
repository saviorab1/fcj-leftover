---
title : "Configure Authentication and Backend"
date : "2025-08-10T20:24:00Z"
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

#### Implement Authentication Wrapper

Configure the application to use AWS Amplify's authentication system with the Authenticator component.

#### Update Main Entry Point

Replace the content of `src/main.tsx` with the following code:

```tsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { Authenticator } from "@aws-amplify/ui-react";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <Authenticator>
      <App />
    </Authenticator>
  </React.StrictMode>
);
```

This configuration:
- Wraps the entire application with the Authenticator component
- Provides built-in sign-up, sign-in, password reset, and MFA functionality
- Ensures users must authenticate before accessing the application

#### Configure Main Application Component

Update the `src/App.tsx` file with Amplify integration:

```tsx
import { FormEvent, useState } from "react";
import { Loader, Placeholder } from "@aws-amplify/ui-react";
import "./App.css";
import { Amplify } from "aws-amplify";
import outputs from "../amplify_outputs.json";

import "@aws-amplify/ui-react/styles.css";

Amplify.configure(outputs);

function App() {
  return (
    <div className="app-container">
      <div className="header-container">
        <h1 className="main-header">
          This here is
          <br />
          <span className="highlight">just a website</span>
        </h1>
        <p className="description">
          You can develop your own website and deploy it to AWS Amplify.
        </p>
      </div>
    </div>
  );
}

export default App;
```

#### Key Configuration Elements

**Amplify Configuration**:
- `Amplify.configure(outputs)`: Connects the app to AWS services using generated configuration
- `amplify_outputs.json`: Contains service endpoints and configuration details

**UI Components**:
- Imports Amplify UI React styles for consistent theming
- Uses responsive design with proper CSS classes
- Implements a clean, modern interface

{{% notice note %}}
The `amplify_outputs.json` file is automatically generated when you deploy your Amplify backend and contains all necessary configuration for connecting to AWS services.
{{% /notice %}}

#### Authentication Features

The Authenticator component provides:
- User registration with email verification
- Secure sign-in and sign-out functionality
- Password reset capabilities
- Multi-factor authentication support
- Customizable UI themes and styling

#### Result

Your application now has complete authentication integration with AWS Amplify, providing secure user access control and a professional user interface.
