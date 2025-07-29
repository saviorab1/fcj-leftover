---
title : "Connect GitHub to Amplify"
date : "2023-12-01T00:00:00Z"
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---

#### Access AWS Amplify Console

To deploy your application, you need to connect your GitHub repository to AWS Amplify for continuous deployment.

#### Navigate to Amplify Service

1. Open the AWS Management Console and search for **Amplify**.
2. Click on **AWS Amplify** to access the service.
3. Click **Deploy an App** or **Create New App** to start the deployment process.

![AWS Amplify Console](/images/4/4-1.png?featherlight=false&width=90pc)

#### Select Source Provider

1. On the "Start building with Amplify" page, choose **GitHub** as the source provider.
2. Click **Continue** to proceed with GitHub integration.

![Select GitHub](/images/4/4-2.png?featherlight=false&width=90pc)

#### Authorize GitHub Access

1. If prompted, log in to your GitHub account.
2. Authorize AWS Amplify to access your GitHub repositories.
3. Grant the necessary permissions for repository access.

#### Select Repository and Branch

1. From the dropdown menu, select your **leftover** repository.
2. Choose the **main** branch for deployment.
3. Verify that the correct repository and branch are selected.

![Repository Selection](/images/4/4-3.png?featherlight=false&width=90pc)

{{% notice info %}}
Ensure you select the correct repository and branch that contains your Vite React application with the Amplify configuration.
{{% /notice %}}

#### Confirm Repository Connection

1. Review the selected repository and branch settings.
2. Click **Next** to proceed to the build settings configuration.

#### Result

Your GitHub repository is now connected to AWS Amplify and ready for build configuration in the next step.