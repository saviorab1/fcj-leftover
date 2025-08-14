---
title : "Remove Lambda Resources"
date : "2025-08-10T20:24:00Z"
weight : 3
chapter : false
pre : " <b> 17.3 </b> "
---

Delete Lambda functions and the related application.

#### Delete Lambda Functions

1. Go to **Lambda** → **Functions**
2. Select the following functions:
   - `leftover-data-collector`
   - `CustomCDKBucketDeployment`
   - `CustomS3AutoDeleteObject`
3. Click **Actions** → **Delete**

![Lambda Delete Functions](/images/17/17-4.png?featherlight=false&width=90pc)

4. Type `confirm` and click **Delete**

![Lambda Delete Functions](/images/17/17-5.png?featherlight=false&width=90pc)

#### Delete Lambda Application

1. In **Lambda**, open the **Applications** tab
2. Select your project's sandbox application
3. Click **Delete**, confirm the prompt

![Lambda Delete Application](/images/17/17-6.png?featherlight=false&width=90pc)

#### Result

The Lambda functions and the associated application are deleted.


