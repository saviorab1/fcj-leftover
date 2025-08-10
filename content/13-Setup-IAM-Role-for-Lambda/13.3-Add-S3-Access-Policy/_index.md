---
title : "Add S3 Access Policy"
date : "2025-08-10T20:24:00Z"
weight : 3
chapter : false
pre : " <b> 13.3 </b> "
---

#### Access the Created Role

To add S3 permissions, you need to modify the existing role with additional policies.

#### Navigate to Role Details

1. Go back to the **Roles** section in the IAM console.
2. Click on the **LeftoverDataCollectionRole** that you just created.
3. This will open the role details page.

![Role Details](/images/13/13-7.png?featherlight=false&width=90pc)

#### Add Inline Policy

1. In the role details page, click **Add permissions**.
2. Select **Create inline policy** from the dropdown menu.

![Add Permissions](/images/13/13-8.png?featherlight=false&width=90pc)

#### Configure Policy Editor

1. In the Policy Editor, switch from **Visual** to **JSON** mode.
2. This allows you to define precise permissions using JSON syntax.

![Policy Editor](/images/13/13-9.png?featherlight=false&width=90pc)

#### Add S3 Permissions

Replace the default JSON content with the following policy:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:PutObjectAcl",
                "s3:GetObject"
            ],
            "Resource": "arn:aws:s3:::leftover-storage/*" 
        }
    ]
}
```

![JSON Policy](/images/13/13-10.png?featherlight=false&width=90pc)

#### Finalize Policy

1. Click **Next** to review the policy.
2. Provide a policy name such as **S3AccessPolicy**.
3. Click **Create policy** to attach it to the role.

![Create Policy](/images/13/13-11.png?featherlight=false&width=90pc)

#### Result

Your IAM role now has the necessary permissions to:
- Execute Lambda functions with basic logging capabilities
- Access S3 bucket operations (PutObject, GetObject, PutObjectAcl) on the leftover-storage bucket

{{% notice note %}}
The role is now ready to be used by Lambda functions that need to interact with your S3 storage.
{{% /notice %}}
