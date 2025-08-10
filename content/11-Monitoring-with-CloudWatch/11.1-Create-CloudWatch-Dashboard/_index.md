---
title : "Create CloudWatch Dashboard"
date : "2025-08-10T20:24:00Z"
weight : 1
chapter : false
---

Setting up a CloudWatch dashboard provides centralized monitoring for your Bedrock application metrics and costs.

#### Navigate to CloudWatch Console

1. Open the **AWS Management Console** and search for **CloudWatch**
2. In the CloudWatch console, navigate to **Dashboards** in the left sidebar
3. Click **Create Dashboard** to begin setup

![CloudWatch Dashboard Creation](/images/11/11-1.png?featherlight=false&width=90pc)

#### Configure Dashboard Settings

1. **Dashboard Name**: Enter `leftover-dashboard`
2. Click **Create Dashboard** to proceed to widget configuration
3. The dashboard creation wizard will open automatically

![Dashboard Name Configuration](/images/11/11-2.png?featherlight=false&width=90pc)

#### Initial Widget Setup

The dashboard is now ready for widget configuration. You'll be prompted to add your first widget with the following default options:

- **Data source type**: CloudWatch
- **Data type**: Metrics  
- **Widget type**: Line

![Initial Widget Setup](/images/11/11-3.png?featherlight=false&width=90pc)

#### Result

Your CloudWatch dashboard foundation is now established and ready for Bedrock metrics configuration. The next step will focus on adding specific monitoring widgets for token usage and invocation tracking.
