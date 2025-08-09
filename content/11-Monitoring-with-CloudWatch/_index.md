---
title : "Monitoring with CloudWatch"
date : "2023-12-01T00:00:00Z"
weight : 11
chapter : false
pre : " <b> 11. </b> "
---

**Content:**
- [Create CloudWatch Dashboard](11.1-create-cloudwatch-dashboard/)
- [Setup Bedrock Metrics Widget](11.2-setup-bedrock-metrics-widget/)
- [Add Invocation Counter Widget](11.3-add-invocation-counter-widget/)
- [Create Cost Calculation Widget](11.4-create-cost-calculation-widget/)

Amazon CloudWatch provides comprehensive monitoring capabilities for your Bedrock-powered application. By creating custom dashboards, you can track token usage, invocation counts, and calculate real-time costs to optimize your application's performance and budget.

{{% notice info %}}
CloudWatch dashboards help you visualize your application's usage patterns and costs in real-time, enabling proactive monitoring and optimization of your AI-powered recipe generator.
{{% /notice %}}

#### Create CloudWatch Dashboard

1. Navigate to CloudWatch console and access the Dashboards section.
2. Create a new dashboard with appropriate naming conventions.
3. Configure the initial dashboard settings and data sources.

#### Setup Bedrock Metrics Widget

1. Add a line chart widget to track input and output token counts.
2. Configure Bedrock metrics filtering by ModelID for your specific region.
3. Optimize widget display options for better visualization.

#### Add Invocation Counter Widget

1. Create a number widget to display total invocation counts.
2. Configure real-time data updates and sparkline visualization.
3. Set up proper time range and aggregation settings.

#### Create Cost Calculation Widget

1. Duplicate existing widgets and add mathematical functions.
2. Implement cost calculation formulas for input and output tokens.
3. Configure cost per invocation metrics and display options.

{{% notice tip %}}
Regular monitoring of your Bedrock usage helps identify optimization opportunities and prevents unexpected costs while ensuring optimal application performance.
{{% /notice %}}