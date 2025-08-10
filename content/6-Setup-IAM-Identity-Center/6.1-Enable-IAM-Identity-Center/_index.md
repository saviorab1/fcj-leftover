---
title : "Enable IAM Identity Center"
date : "2025-08-10T20:24:00Z"
weight : 1
chapter : false
pre : " <b> 6.1 </b> "
---

#### Access IAM Identity Center Service

To set up centralized access management, you need to enable AWS IAM Identity Center in your AWS account.

#### Navigate to IAM Identity Center

1. Open the AWS Management Console and search for **IAM Identity Center**.
2. Click on **IAM Identity Center** to access the service.
3. You'll see the IAM Identity Center dashboard with setup options.

![IAM Identity Center Console](/images/6/6-1.png?featherlight=false&width=90pc)

#### Enable IAM Identity Center

1. Click **Enable** to start the IAM Identity Center setup process.
2. This will initiate the configuration wizard for your organization.

#### Configure with AWS Organizations

1. A popup will appear with setup options.
2. Select **Enable with AWS Organizations** for integrated management.
3. Click **Continue** to proceed with the organization-based setup.

![Enable with Organizations](/images/6/6-2.png?featherlight=false&width=90pc)

{{% notice info %}}
Enabling with AWS Organizations provides centralized management across multiple AWS accounts and simplifies permission management for your organization.
{{% /notice %}}

#### Complete Basic Setup

1. IAM Identity Center will configure the basic infrastructure.
2. Wait for the setup process to complete.
3. You'll see confirmation that IAM Identity Center is now enabled.

#### Verify Setup

After enabling, you should see:
- IAM Identity Center dashboard with management options
- Access to Users, Groups, and Permission sets
- Integration with AWS Organizations (if applicable)
- Ready status for user and permission configuration

#### Result

IAM Identity Center is now enabled and ready for user and permission configuration in the next step.
