---
title : "Revoke Bedrock Model Access"
date : "2025-08-10T20:24:00Z"
weight : 7
chapter : false
pre : " <b> 17.7 </b> "
---

Remove access to Amazon Bedrock models to prevent further usage.

#### Modify Model Access

1. Go to **Amazon Bedrock**
2. In the left navigation, under **Configure and learn**, click **Model access**
3. Click **Modify model access**

![Bedrock Model Access](/images/17/17-13.png?featherlight=false&width=90pc)

4. In **Find model**, search for models you enabled (e.g., "Claude Sonnet 4")
5. Untick the checkbox for each enabled model
6. Click **Review and submit**

![Bedrock Model Access](/images/17/17-14.png?featherlight=false&width=90pc)

{{% notice note %}}
Repeat this process in any other regions where model access was granted.
{{% /notice %}}

#### Result

Model access is revoked in Amazon Bedrock.


