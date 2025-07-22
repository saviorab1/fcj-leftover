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


Hit enter

To validate that this worked, run the following command in the CloudShell:

You should see something like:
Start session url: https://d-XXXXXXXXXX.awsapps.com/start
Region: <your-account-associated-region>
Username: amplify-admin

## Finish the setup for 
