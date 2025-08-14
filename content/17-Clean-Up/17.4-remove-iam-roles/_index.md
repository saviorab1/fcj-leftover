---
title : "Remove IAM Roles"
date : "2025-08-10T20:24:00Z"
weight : 4
chapter : false
pre : " <b> 17.4 </b> "
---

Delete IAM roles created for the project.

#### Delete Project IAM Roles

1. Go to **IAM** → **Roles**
2. In the search bar, enter `leftover`
3. Select all roles associated with this project
4. Click **Delete** and confirm

![IAM Delete Roles](/images/17/17-7.png?featherlight=false&width=90pc)

{{% notice note %}}
If a role cannot be deleted due to attached policies or active resources, detach the policies first and ensure no services reference the role.
{{% /notice %}}

#### Result

All project-related IAM roles are removed.


