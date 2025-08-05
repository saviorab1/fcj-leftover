---
title : "Deploy Sandbox Environment"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 7.2 </b> "
---

#### Deploy Amplify Sandbox

With AWS credentials configured, you can now deploy the Amplify sandbox environment for local development.

#### Navigate to Project Directory

1. Open a terminal in your `leftover` project directory.
2. Ensure you're in the root folder where `package.json` and `amplify/` directory are located.

#### Deploy Sandbox with Profile

Execute the following command to deploy the sandbox:

```bash
npx ampx sandbox --profile amplify-admin
```

This command will:
- Deploy AWS resources in an isolated sandbox environment
- Generate the `amplify_outputs.json` configuration file
- Set up authentication and data services for local development

#### Monitor Deployment Progress

1. The deployment process will show progress updates.
2. Wait for the message: `[Sandbox] Watching for file changes...`
3. This indicates the sandbox is successfully deployed and monitoring for changes.

![Sandbox Success](/images/7/7-10.png?featherlight=false&width=90pc)

#### Troubleshooting Common Issues

**Invalid Credentials Error**:
If you see `InvalidCredentialError: Failed to load default AWS credentials`:
1. Verify your profile configuration with `aws configure list --profile amplify-admin`
2. Re-run the SSO login: `aws sso login --profile amplify-admin`

**SSM Credentials Error**:
If you encounter `SSMCredentialsError: UnrecognizedClientException`:
1. Navigate to `C:\Users\YourUserName\.aws` (Windows) or `~/.aws` (macOS/Linux)
2. Delete the existing configuration files
3. Reconfigure your profile following the previous step

![Troubleshooting](/images/7/7-11.png?featherlight=false&width=90pc)

#### Start Local Development Server

Once the sandbox is deployed, start your local development server:

```bash
npm run dev
```

![Local Server](/images/7/7-12.png?featherlight=false&width=90pc)

#### Create New Account

1. Open your browser and navigate to `http://localhost:5173`.
2. You should see the Amplify Authenticator component.
3. Click **Create Account** to start the sign-up process.
4. Fill in the required information (email, password, etc.).
5. Submit the registration form.

![Create Account](/images/7/7-13.png?featherlight=false&width=90pc)

#### Verify Email Address

1. Check your email inbox for a verification message from AWS.
2. Open the verification email and click the confirmation link.
3. Return to the application and complete the verification process.
4. Sign in with your newly created and verified credentials.

![Email Verification](/images/7/7-14.png?featherlight=false&width=90pc)
![Email Verification-2](/images/7/7-15.png?featherlight=false&width=90pc)

#### Verify Sandbox Integration

After successful authentication, you should see:
- Your application's main interface
- Proper integration with AWS services
- Real-time connection to the sandbox environment
- Ability to interact with authenticated features

![Application Running](/images/7/7-16.png?featherlight=false&width=90pc)

#### Result

Your Amplify sandbox environment is now fully operational with:
- Isolated AWS resources for development
- Local development server with hot reloading
- Complete authentication flow integration
- Real-time synchronization with cloud services

{{% notice note %}}
The sandbox environment runs continuously and watches for file changes. Keep the terminal open while developing to maintain the connection to AWS services.
{{% /notice %}}