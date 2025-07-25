---
title : "Setting up AWS Bedrock (Legacy)"
date : "2023-12-01T00:00:00Z"
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---

## Content



## Request an AWS Bedrock Model

You will need to get to Amazon Bedrock and click on Model Catalog. 

You will be greeted by one of those two pages. In either way, click on the mark part of the image.

 ![IAM Frontpage](/images/3/8-0.png?featherlight=false&width=90pc)

 ![IAM Frontpage](/images/3/8-0-1.png?featherlight=false&width=90pc)

Afterward, click on the AI model and click on Modify Access.

 ![IAM Frontpage](/images/3/8-1.png?featherlight=false&width=90pc)


## Using CloudShell to set up the management

In this case, we will choose Claude 3.5 Sonnet as it is readily available at ap-southeast-1 region. You can check the availability of AI models within each region via this link: https://docs.aws.amazon.com/bedrock/latest/userguide/models-regions.html

First, you will need to choose to modify the Model Access. There are two scenarios:



 ![IAM Frontpage](/images/3/8-2.png?featherlight=false&width=90pc)

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

Hit enter and wait.

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

## Finish the setup for AWS IAM Identity Center

Now create a password for the user that we need for the next step. In the IAM Identity Center console, navigate to Users→amplify-admin.

 ![IAM verification first step](/images/2/4-8.png?featherlight=false&width=90pc)

Once you have clicked on the user, you will see a pop-up telling you to verify the email address. You click on that:

 ![IAM verification second step](/images/2/4-9.png?featherlight=false&width=90pc)

Check your email, you should get a notification from the AWS to verify your email.

 ![IAM verification third step](/images/2/4-10.png?featherlight=false&width=90pc)

Next, you will be changing the password of your account. Once again, navigate to Users→amplify-admin. There, you will see an option to Reset Password, click on it. 

 ![IAM verification fourth step](/images/2/4-14.png?featherlight=false&width=90pc)

Upon clicking on it, choose Reset Password and wait for a few moments.

 ![IAM verification fourth step](/images/2/4-15.png?featherlight=false&width=90pc)

Check your email frequently, you should recieve a mail that look like this:

 ![IAM verification fourth step](/images/2/4-16.png?featherlight=false&width=90pc)

Follow the steps that is provided, you will need to create a new password and a MFA. Once you are finished, head back to the IAM Identity Center, you will be given an AWS Access Portal URL.

 ![IAM verification fourth step](/images/2/4-12.png?featherlight=false&width=90pc)

You will see a sign-in screen, sign in using the earlier account, password, MFA, and you are good to go.

 ![IAM verification fourth step](/images/2/4-11.png?featherlight=false&width=90pc)