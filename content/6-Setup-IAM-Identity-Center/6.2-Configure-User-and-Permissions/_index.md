---
title : "Configure User and Permissions"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 6.2 </b> "
---

#### Setup Administrative User via CloudShell

Use AWS CloudShell to create an administrative user with proper permissions for Amplify deployment and management.

#### Access AWS CloudShell

1. In the AWS Console, click on the CloudShell icon in the top navigation bar.
2. Wait for the CloudShell environment to initialize.
3. You'll have access to a terminal with AWS CLI pre-configured.

#### Collect User Email

Enter the following command to capture your email address:

```bash
read -p "Enter email address: " user_email
```

![CloudShell Email Input](/images/6/6-3.png?featherlight=false&width=90pc)

Type your email address and press Enter. This email will be used for the administrative user account.

#### Create User and Permission Set

Execute the following multi-line command to create the user and configure permissions:

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

![CloudShell Configuration](/images/6/6-4.png?featherlight=false&width=90pc)

{{% notice warning %}}
You may see warnings due to the multi-line nature of the command. Continue pasting the entire command block and press Enter to execute.
{{% /notice %}}

#### Wait for Completion

1. The command will execute multiple AWS API calls.
2. Wait for all operations to complete successfully.
3. You should see confirmation messages for each step.

![CloudShell Completion](/images/6/6-5.png?featherlight=false&width=90pc)

#### Validate Configuration

Run the following command to verify the setup and get access information:

```bash
printf "\\n\\nStart session url: https://$ssoId.awsapps.com/start\\nRegion: $AWS_REGION\\nUsername: amplify-admin\\n\\n"
```

![CloudShell Validation](/images/6/6-6.png?featherlight=false&width=90pc)

#### Configuration Details

This setup creates:
- **User**: `amplify-admin` with your email address
- **Permission Set**: `amplify-policy` with 12-hour session duration
- **Policy**: `AmplifyBackendDeployFullAccess` for complete Amplify access
- **Account Assignment**: Links the user to your AWS account with the permission set

#### Result

You now have an administrative user configured with proper permissions for Amplify deployment and management.