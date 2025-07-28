---
title : "Apply CloudWatch to monitor average response time"
date : "2023-12-01T00:00:00Z"
weight : 9
chapter : false
pre : " <b> 3.3 </b> "
---

## Content

On AWS Management Console, go to CloudWatch → Metrics → All metrics.

 ![IAM Frontpage](/images/3/11-0.png?featherlight=false&width=90pc)

In the search box on the right, find “AWS Bedrock” and choose Bedrock > By ModelID.

 ![IAM Frontpage](/images/3/11-0-1.png?featherlight=false&width=90pc)

Choose any log options that you want to look out for. In this case, it should be Invocations (to see how many Invoke has been triggered during a specific time) and InvocationLatency (the latency between invoke and returned results).

 ![IAM Frontpage](/images/3/11-0-2.png?featherlight=false&width=90pc)

Now go back to Dashboard on the left tab and click Create dashboard.

 ![IAM Frontpage](/images/3/11-0-3.png?featherlight=false&width=90pc)

Name the newly created dashboard. In my case, I named it LeftoverResponseLatency. In the Add widget table, choose Cloudwatch for Data source types. You can pick whichever Widget Type you are fancy with or just choose Number like me.

 ![IAM Frontpage](/images/3/11-1.png?featherlight=false&width=90pc)

Now these are the number of average response time for you to see. You can do the same for the other fallback region to monitor its average response time as well.