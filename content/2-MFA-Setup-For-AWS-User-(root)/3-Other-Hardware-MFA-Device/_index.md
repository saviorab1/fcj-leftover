---
title : "Setting up the Frontend, Backend and AWS Sandbox"
date : "2023-12-01T00:00:00Z"
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---

**Content**

- [Enable other hardware MFA device through the Console](#enable-other-hardware-mfa-device-through-the-console)

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

### Setup AWS Sandbox

By using Amplify Sandbox, developers can rapidly integrate the website within an isolated development environment, while still able to use AWS services and features. In order to do that, run open a new terminal window, navigate to workshop2 directory and run the following command:

```bash
npx ampx sandbox
```

Once the cloud sandbox has been fully deployed, your terminal will display a confirmation message and the amplify_outputs.json file will be generated and added to your project.

![Invalid](/images/2/6-0-2.png?featherlight=false&width=90pc)

→If it says InvalidCredentialError: Failed to load default AWS credentials it means you need to configure your profile, in order to do that, type:

```bash
aws configure
```

You can find the necessary information in the logged in session of your amplify-admin account by logging into the AWS Identity Center. Log into the Center and you will be able to find your code here.

![IAM](/images/2/6-1.png?featherlight=false&width=90pc)

So, once you click into the keys, you will be able to see the 3 options. Based on the operation you are running, choose the suitable one. In my case, it will be Windows.

![IAM](/images/2/6-2.png?featherlight=false&width=90pc)

You will be seeing the SSO and every info necessary for your SSO registration.

![SSO](/images/2/6-3.png?featherlight=false&width=90pc)

Redo:

```bash
aws configure
```

As for SSO session name and Profile name, please leave it at amplify-default. You can leave the SSO registration scopes and CLI default output format as blank.

![SSO](/images/2/6-4.png?featherlight=false&width=90pc)


Afterward, type in:
```bash
aws configure sso
```

You should see this in response:

![SSO](/images/2/6-5.png?featherlight=false&width=90pc)

You shall see the link. Click on it, and click on **Allow Access**.

![SSO](/images/2/6-6.png?featherlight=false&width=90pc)

You shall be greeted with this message.

![SSO](/images/2/6-7.png?featherlight=false&width=90pc)

Then, in order to use your newly created profile, type in:
npx ampx sandbox –profile amplify-default (or whatever your profile name is)
The terminal will output this line “[Sandbox] Watching for file changes…” when success.

![SSO](/images/2/6-8.png?featherlight=false&width=90pc)

→If it says SSMCredentialsError: UnrecognizedClientException: The security token included in the request is invalid, it might be due to a conflict amplify accounts, in order to fix this problem, navigate to C:\Users\YourUserName\.aws and delete everything in there then start configure your profile as demonstrated above.

![SSO](/images/2/6-8-1.png?featherlight=false&width=90pc)

Finally, to check the sso, you can use these commands.

```bash
aws sts get-caller-identity --profile amplify-1
```

```bash
npm ampx sandbox --profile amplify-1
```

When you’re done with setting up the sandbox environment, run:

```bash
npm run dev
```
![SSO](/images/2/7-1.png?featherlight=false&width=90pc)
to initialize a localhost for your website, you can then get access to the website locally at **locahost:5173**.

Afterwards, sign up and sign in using your account normally. Remember to verify your account as well.

![SSO](/images/2/7-2.png?featherlight=false&width=90pc)

![SSO](/images/2/7-3.png?featherlight=false&width=90pc)

![SSO](/images/2/7-4.png?featherlight=false&width=90pc)

The result should be:

![SSO](/images/2/7-5.png?featherlight=false&width=90pc)