---
title : "Deploy and Access Application"
date : "2025-08-10T20:24:00Z"
weight : 3
chapter : false
pre : " <b> 4.3 </b> "
---

#### Complete Deployment Setup

After configuring the build settings, you're ready to deploy your application to AWS Amplify.

#### Review and Deploy

1. Review all configuration settings including repository, branch, and build settings.
2. Click **Next** to proceed to the final review step.
3. Click **Save and Deploy** to start the deployment process.

![Save and Deploy](/images/4/4-7.png?featherlight=false&width=90pc)

#### Monitor Build Progress

1. Amplify will start the build process automatically.
2. Monitor the build progress in the Amplify console.
3. The build process includes provisioning, building, deploying, and verifying stages.

![Build Progress](/images/4/4-8.png?featherlight=false&width=90pc)

#### Handle Build Issues (If Any)

If the build fails:
1. Check the build logs for error details.
2. Common issues include incorrect build commands or missing dependencies.
3. Edit build settings by going to **Hosting** → **Build Settings**.

![Build Settings](/images/4/4-9.png?featherlight=false&width=90pc)

{{% notice tip %}}
If you need to modify the amplify.yml file after deployment, navigate to Hosting → Build Settings to make changes.
{{% /notice %}}

#### Access Deployed Application

Once the build completes successfully:

1. Return to the Amplify app overview page.
2. Click **Visit deployed URL** to access your live application.

![Visit Deployed URL](/images/4/4-10.png?featherlight=false&width=90pc)

#### Verify Application

1. Your Vite React application should load successfully.
2. Test the application functionality to ensure everything works as expected.
3. The application is now live and accessible via the Amplify-generated URL.

![Application Live](/images/4/4-11.png?featherlight=false&width=90pc)

#### Set Up Continuous Deployment

Your application now has continuous deployment configured:
- Any changes pushed to the main branch will trigger automatic rebuilds
- The application will be updated automatically with new deployments
- Build history and logs are available in the Amplify console

#### Result

Your Vite React application is now successfully deployed on AWS Amplify with:
- Automatic builds triggered by GitHub commits
- Global content delivery via CloudFront
- HTTPS enabled by default
- Custom domain support available

{{% notice note %}}
The deployed URL will remain consistent, making it easy to share and access your application from anywhere.
{{% /notice %}}
