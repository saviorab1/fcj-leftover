---
title : "Setting up the Frontend and Backend"
date : "2023-12-01T00:00:00Z"
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

**Content**

#### Coding the Frontend

In the terminal window, navigate to leftover folder and run this command to install the libraries:

```bash
npm install aws-amplify @aws-amplify/ui-react
```

![Install](/images/2/6-0-1.png?featherlight=false&width=90pc)

Open index.css file in src folder and update it with the following code to center the App UI:

```css
:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color: rgba(255, 255, 255, 0.87);

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
}

.card {
  padding: 2em;
}

.read-the-docs {
  color: #888;
}

.box:nth-child(3n + 1) {
  grid-column: 1;
}
.box:nth-child(3n + 2) {
  grid-column: 2;
}
.box:nth-child(3n + 3) {
  grid-column: 3;
}

```

Then update the App.css which is also in the same src folder with:

```css
.app-container {
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

.header-container {
  padding-bottom: 2.5rem;
  margin: auto;
  text-align: center;
  max-width: 48rem;
}

.main-header {
  font-size: 2.25rem;
  font-weight: bold;
  color: #1a202c;
}

.main-header .highlight {
  color: #2563eb;
}

@media (min-width: 640px) {
  .main-header {
    font-size: 3.75rem;
  }
}

.description {
  font-weight: 500;
  font-size: 1.125rem;
  max-width: 65ch;
  color: #1a202c;
}

```
#### Coding the Backend

Update main.tsx file in src folder with these codes to allow users to sign up, sign in, reset their password, and confirm sign-in for MFA with the Amplify Authenticator component:

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

In the same src folder, implement a simple UI for the App.tsx:

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

Lastly, setup Amplify Data by create a resource.ts file in amplify/data folder and update it with following code:

```tsx
import { type ClientSchema, a, defineData } from "@aws-amplify/backend";

const schema = a.schema({
  // Empty schema but properly formatted
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