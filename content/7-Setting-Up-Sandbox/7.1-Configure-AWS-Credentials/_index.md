---
title : "Configure AWS Credentials"
date : "2025-08-10T20:24:00Z"
weight : 1
chapter : false
pre : " <b> 7.1 </b> "
---

#### Setup AWS CLI with SSO Authentication

Configure AWS CLI to use the IAM Identity Center credentials for sandbox deployment and management.

#### Access AWS Identity Center Portal

1. Navigate to your AWS Access Portal URL from the previous step.
2. Sign in with your `amplify-admin` credentials.
3. Click on your AWS account to access the credential options.

![AWS Access Portal](/images/7/7-1.png?featherlight=false&width=90pc)

#### Get Access Credentials

1. Click on **Command line or programmatic access**.
2. Select your operating system (Windows, macOS, or Linux).
3. Copy the SSO configuration details displayed.

![Access Credentials](/images/7/7-2.png?featherlight=false&width=90pc)

#### Initial AWS Configuration

First, run the basic AWS configuration command:

```bash
aws configure
```

This will prompt for basic AWS configuration.

![Access Credentials](/images/7/7-3.png?featherlight=false&width=90pc)

#### Configure AWS CLI Profile

Open a terminal in your project directory and run:

```bash
aws configure sso
```

Enter the following information when prompted:
- **SSO session name**: `amplify-admin`
- **SSO start URL**: Your AWS Access Portal URL
- **SSO region**: Your AWS region (e.g., `ap-southeast-1`)
- **SSO registration scopes**: Leave blank (press Enter)

![AWS Configure SSO](/images/7/7-4.png?featherlight=false&width=90pc)

#### Complete SSO Authorization

1. The CLI will provide a verification URL and code.
2. Open the URL in your browser and enter the verification code.
3. Click **Allow access** to authorize the CLI.
4. After authorization, you'll be redirected to the Amplify app for confirmation.

![SSO Authorization](/images/7/7-5.png?featherlight=false&width=90pc)
![SSO Authorization-2](/images/7/7-6.png?featherlight=false&width=90pc)

#### Select Account and Role

1. Choose your AWS account from the list.
2. Select the appropriate role (should show the amplify-policy permission set).
3. Set the **CLI default client Region** to your preferred region.
4. Set the **CLI default output format** to `json` or leave blank.

#### Set Profile Name

When prompted for the profile name, use:
```
amplify-admin
```

{{% notice warning %}}
Do not use "default" as the profile name. Use "amplify-admin" to avoid conflicts with existing AWS configurations and ensure proper credential isolation.
{{% /notice %}}

#### Verify Configuration

Test your configuration by running:

```bash
aws sts get-caller-identity --profile amplify-admin
```

You should see your account information, confirming the credentials are working correctly.

![Configuration Verification](/images/7/7-7.png?featherlight=false&width=90pc)

#### Add Session Token (If Required)

In some cases, you may need to add an AWS session token manually:

1. Navigate to `Users/<Username>/.aws/credentials` on your system.
2. Open the credentials file in a text editor.
3. Add the session token to the end of your profile section:
![Credentials File](/images/7/7-8.png?featherlight=false&width=90pc)

```
[amplify-admin]
aws_access_key_id = YOUR_ACCESS_KEY
aws_secret_access_key = YOUR_SECRET_KEY
aws_session_token = YOUR_SESSION_TOKEN
```
![Token Session](/images/7/7-9.png?featherlight=false&width=90pc)

{{% notice info %}}
The session token is typically only required if you encounter authentication issues during sandbox deployment.
{{% /notice %}}

#### Result

Your AWS CLI is now configured with SSO authentication and ready for sandbox deployment.
