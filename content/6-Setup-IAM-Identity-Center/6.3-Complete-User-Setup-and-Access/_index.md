---
title : "Complete User Setup and Access"
date : "2023-12-01T00:00:00Z"
weight : 3
chapter : false
pre : " <b> 6.3 </b> "
---

#### Verify Email and Setup Authentication

Complete the user setup process by verifying the email address and configuring authentication credentials.

#### Access User Management

1. Return to the IAM Identity Center console.
2. Navigate to **Users** in the left sidebar.
3. Click on the **amplify-admin** user you created.

![User Management](/images/6/6-7.png?featherlight=false&width=90pc)

#### Verify Email Address

1. You'll see a notification about email verification.
2. Click on the email verification prompt or button.
3. Check your email inbox for the verification message from AWS.

![Email Verification](/images/6/6-8.png?featherlight=false&width=90pc)

#### Complete Email Verification

1. Open the verification email from AWS.
2. Click the verification link provided in the email.
3. Follow the instructions to confirm your email address.

![Email Confirmation](/images/6/6-9.png?featherlight=false&width=90pc)

#### Reset User Password

1. Return to the IAM Identity Center console.
2. Navigate to **Users** → **amplify-admin**.
3. Click **Reset password** to set up the user's credentials.

![Reset Password](/images/6/6-10.png?featherlight=false&width=90pc)

#### Configure Password and MFA

1. Click **Reset Password** and wait for the process to complete.
2. Check your email for the password reset instructions.
3. Follow the email instructions to set a new password.
4. Configure Multi-Factor Authentication (MFA) as prompted.

![Password Setup](/images/6/6-11.png?featherlight=false&width=90pc)

#### Access AWS Access Portal

1. After completing password and MFA setup, return to IAM Identity Center.
2. Note the **AWS Access Portal URL** displayed in the console.
3. This URL will be used for future access to AWS resources.

![Access Portal URL](/images/6/6-12.png?featherlight=false&width=90pc)

#### Test Access Portal Login

1. Navigate to the AWS Access Portal URL.
2. Sign in using:
   - Username: `amplify-admin`
   - Password: The password you just created
   - MFA: Your configured multi-factor authentication

![Portal Login](/images/6/6-13.png?featherlight=false&width=90pc)

#### Verify Access

After successful login, you should see:
- Available AWS accounts
- Permission sets assigned to your user
- Access to AWS services based on your permissions
- Ability to access the AWS Console with Amplify permissions

#### Result

Your IAM Identity Center setup is now complete with:
- Verified administrative user account
- Proper authentication and MFA configured
- Access portal ready for secure AWS resource management
- Full permissions for Amplify deployment and management

{{% notice note %}}
Save the AWS Access Portal URL and your credentials securely. You'll use this for future access to AWS services and Amplify management.
{{% /notice %}}