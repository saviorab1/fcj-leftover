---
title : "Deploy the Application via AWS Amplify"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

**Content**
- [Deploy the Application via AWS Amplify](#enable-u2f-security-key-via-console)

#### Connecting AWS Amplify with GitHub

After initializing Amplify in the project, the application was deployed using AWS Amplify’s hosting feature, which supports seamless integration with GitHub for CI/CD.

You will open the AWS Console by navigating to the AWS Amplify service, and click on **Deploy an App** or **Create New App**.

![AWS Frontpage](/images/2/5-1.png?featherlight=false&width=90pc)

On the “Start building with Amplify” page, choose GitHub as the source provider. Log in and authorize GitHub access if prompted.

![AWS GitHub](/images/2/5-2.png?featherlight=false&width=90pc)

Remember to check the branch/repository of the GitHub repository you used to store the data. 

![Repository](/images/2/5-3.png?featherlight=false&width=90pc)

At the app setting part, you will need to edit the YML file. Put all the info just like the screenshot under and click on **Edit YML file**.

![Repository](/images/2/5-4.png?featherlight=false&width=90pc)

Inside the YML file, paste the following code:

```yml
Modify the amplify.yml file as follows:
version: 1
backend:
  phases:
    preBuild:
      commands:
        - npm install
    build:
      commands:
        - nvm use 20
        - npm ci --cache .npm --prefer-offline
        - npx ampx pipeline-deploy --branch $AWS_BRANCH --app-id $AWS_APP_ID
frontend:
  phases:
    build:
      commands:
        - npm run build
  artifacts:
    baseDirectory: dist
    files:
      - '**/*'
  cache:
    paths:
      - node_modules/**/*

```
{{%notice warning%}}
THE COMMAND LINES MUST BE INDENTED CORRECTLY JUST LIKE THE INSTRUCTIONS.
{{%/notice%}}

![YML File](/images/2/5-5.png?featherlight=false&width=90pc)

After finished editing the YML file, save and then scroll down to next.

![Finish Step 3](/images/2/5-6.png?featherlight=false&width=90pc)

Click on Finish and Deploy, this will create an AWS Amplify Console that will match your liking.

![Finish Setting up](/images/2/5-7.png?featherlight=false&width=90pc)

Return to the Overview, click the Production branch, and then select Redeploy this version. Wait for the build process to complete. Once deployed, the app will be accessible at the generated domain link provided in the main branch overview.

![Finish Setting up](/images/2/5-8.png?featherlight=false&width=90pc)

{{%notice tip%}}
In case of the yml file being wrong somewhere, you can come back to the file by choosing **Hosting** then **Build Settings**.
{{%/notice%}}

![Finish Setting up](/images/2/5-8-1.png?featherlight=false&width=90pc)

```js
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowManageOwnUserMFA",
            "Effect": "Allow",
            "Action": [
                "iam:DeactivateMFADevice",
                "iam:EnableMFADevice",
                "iam:GetUser",
                "iam:ListMFADevices",
                "iam:ResyncMFADevice"
            ],
            "Resource": "arn:aws:iam::*:user/${aws:username}"
        },
        {
            "Sid": "DenyAllExceptListedIfNoMFA",
            "Effect": "Deny",
            "NotAction": [
                "iam:EnableMFADevice",
                "iam:GetUser",
                "iam:ListMFADevices",
                "iam:ResyncMFADevice"
            ],
            "Resource": "arn:aws:iam::*:user/${aws:username}",
            "Condition": {
                "BoolIfExists": {
                    "aws:MultiFactorAuthPresent": "false"
                }
            }
        }
    ]
}
```

![MFA](/images/3/0001.png?featherlight=false&width=90pc)

4. Select **Next: Tags**. This is a screen of **Tags**, a tool used to differentiate AWS resources.
5. Select **Next: Review**. This is the screen that allows you to review the permission set you are creating.
6. Enter the permission set name (eg MFAHardDevice) and select **Create policy**.

![MFA](/images/3/0002.png?featherlight=false&width=90pc)

![MFA](/images/3/0003.png?featherlight=false&width=90pc)

7. In the left sidebar, select **Dashboard** and then select **Enable MFA**.

![MFA](/images/3/0004.png?featherlight=false&width=90pc)

8. Expand Multi-factor authentication (MFA) then select **Active MFA**.

9. In **Manage MFA Device**, select **U2F security key** then press **Continue**.
10. Plug the U2F security key into the computer's USB port.

![Image](/images/1-account-setup/U2FSK.png?featherlight=false&width=90pc)

11. Click the U2F security key, and then select **Close** when U2F is successfully set up.
