---
title : "Working on the main Functionality of the project using AWS Services"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

## Content

- [Content](#content)
- [Setting Up the IAM Identity Center](#setting-up-the-iam-identity-center)
- [Deploy the Application via AWS Amplify](#deploy-the-application-via-aws-amplify)
- [Setting up the Frontend, Backend and AWS Sandbox](#setting-up-the-frontend-backend-and-aws-sandbox)


## Setting Up the IAM Identity Center

In order to manage multiple accounts with Single-sign on (SSO) session, users, groups, permission sets, and more for your organization, you have to set up the IAM Identity Center.

1. Open AWS Console to access IAM Identity Center and enable the process.

2. Open CloudShell and set up the management for the AWS Services using your root email as the main profile for the project.

3. Configure the account by changing the password and finish setting up the new account and signing in.

## Deploy the Application via AWS Amplify

After initializing Amplify and enabling IAM Identity Center in the project, the application was deployed using AWS Amplify’s hosting feature, which supports seamless integration.

1. Connect and Deploy AWS Amplify with the Repository from your GitHub.

2. Edit the Build specification in the Amplify file.

3. Save and Redeploy the App.

---

## Setting up the Frontend, Backend and AWS Sandbox

You will need to set up the frontend, back and the aws sandbox following these steps.

   ### Frontend and Backend

1. Install the libraries necessary using npm inside the local repository for AWS Amplify and update the following files:l-2-ways
   - src/index.css (For Frontend)
   - src/App.css (For Frontend)
   - src/main.tsx (For UI)
   - src/App.tsx (For UI)

2. Set up the resources file for Amplify Data by creating the file:
   - amplify/data/resource.ts

   ### Amplify Sandbox

3. Using npm to install Amplify Sandbox.

4. After setting up, you will need to configure a profile inside the sandbox. 

5. Configure and make a localhost.


