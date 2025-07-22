---
title : "Setting Up the IAM Identity Center"
date : "2023-12-01T00:00:00Z"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

## Start up the IAM Identity Center

(If you already have a profile, attach the AmplifyBackendDeployFullAccess managed policy to your IAM user)

Open AWS Console to access IAM Identity Center and choose Enable.

 ![IAM Frontpage](/images/2/4-1.png?featherlight=false&width=90pc)

 Afterward, a pop up will open, select Enable with AWS Organizations and choose Continue.

 ![Enabling IAM Identity Center](/images/2/4-2.png?featherlight=false&width=90pc)

 And the basics for IAM Identity Center is ready.

## Using CloudShell to set up the management.

We will now using CloudShell to connect our mail account as the main profile for the project.

Open CloudShell terminal within the website and paste this line of code, then enter your email address after the prompt.

```bash
read -p "Enter email address: " user_email # hit enter
```
 ![CloudShell first step](/images/2/4-4.png?featherlight=false&width=90pc)


Afterward, copy and paste the following command, it will show a warning due to the multiline nature, but just keep pasting anyway.

```bash
response=$(aws sso-admin list-instances)
ssoId=$(echo $response | jq '.Instances[0].IdentityStoreId' -r)
ssoArn=$(echo $response | jq '.Instances[0].InstanceArn' -r)
email_json=$(jq -n --arg email "$user_email" '{"Type":"Work","Value":$email}')
response=$(aws identitystore create-user --identity-store-id $ssoId --user-name amplify-admin --display-name 'Amplify Admin' --name Formatted=string,FamilyName=Admin,GivenName=Amplify --emails "$email_json")
userId=$(echo $response | jq '.UserId' -r)
response=$(aws sso-admin create-permission-set --name amplify-policy --instance-arn=$ssoArn --session-duration PT12H)
permissionSetArn=$(echo $response | jq '.PermissionSet.PermissionSetArn' -r)
aws sso-admin attach-managed-policy-to-permission-set --instance-arn $ssoArn --permission-set-arn $permissionSetArn --managed-policy-arn arn:aws:iam::aws:policy/service-role/AmplifyBackendDeployFullAccess
accountId=$(aws sts get-caller-identity | jq '.Account' -r)
aws sso-admin create-account-assignment --instance-arn $ssoArn --target-id $accountId --target-type AWS_ACCOUNT --permission-set-arn $permissionSetArn --principal-type USER --principal-id $userId
```
 ![CloudShell second step](/images/2/4-5.png?featherlight=false&width=90pc)

Hit enter and just keep on waiting.

 ![CloudShell second step](/images/2/4-6.png?featherlight=false&width=90pc)

To validate that this worked, run the following command in the CloudShell:

```bash
printf "\n\nStart session url: https://$ssoId.awsapps.com/start\nRegion: $AWS_REGION\nUsername: amplify-admin\n\n"
```

 ![CloudShell third step](/images/2/4-7.png?featherlight=false&width=90pc)

You should see something like:

Start session url: https://d-XXXXXXXXXX.awsapps.com/start

Region: <your-account-associated-region>

Username: amplify-admin

## Finish the setup for IAM Identity Center

Now create a password for the user that we need for the next step. In the IAM Identity Center console, navigate to Users→amplify-admin

 ![IAM Verification first step](/images/2/4-8.png?featherlight=false&width=90pc)

You will see a notice that will tell you to verify your email address, do click on it and verify. 

 ![IAM Verification second step](/images/2/4-9.png?featherlight=false&width=90pc)

Once you have clicked on it, a verification email will appear. You will need to follow their instructions throughout.

 ![IAM Verification third step](/images/2/4-10.png?featherlight=false&width=90pc)

After verifying the email, you will need to come back to the IAM Dashboard and the setting. Click on the account once again, and click on change password.

 ![IAM Verification fourth step](/images/2/4-14.png?featherlight=false&width=90pc)

Then, click on Reset Password.

 ![IAM Verification fifth step](/images/2/4-15.png?featherlight=false&width=90pc)

You will need to check your email afterwards, since there will be an email that helps you to change password + setting up the MFA. Follow their instructions.

 ![IAM Verification fifth step](/images/2/4-16.png?featherlight=false&width=90pc)

Afterward, get back to the Dashboard, and click on the AWS Access Portal URL, and sign in normally. 

 ![IAM Verification sixth step](/images/2/4-12.png?featherlight=false&width=90pc)
 ![IAM Verification sixth-2nd step](/images/2/4-11.png?featherlight=false&width=90pc)