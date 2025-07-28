---
title : "Setting up AWS Sandbox"
date : "2023-12-01T00:00:00Z"
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

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