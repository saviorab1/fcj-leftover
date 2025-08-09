---
title : "Add Invocation Counter Widget"
date : "2023-12-01T00:00:00Z"
weight : 3
chapter : false
---

Create a number widget to track total Bedrock model invocations with real-time updates and historical trends.

#### Create Invocation Widget

1. Click the **+** button to add a new widget to your dashboard
2. Configure the widget settings:
   - **Data source type**: CloudWatch
   - **Data type**: Metrics
   - **Widget type**: Number

![Invocation Widget Setup](/images/11/11-8.png?featherlight=false&width=90pc)

#### Select Invocation Metrics

1. Browse through the same Bedrock metrics path as the previous widget
2. Navigate to **Bedrock > By ModelID**
3. Select **Invocations** as the metric name to track total model calls

![Invocation Metrics Selection](/images/11/11-9.png?featherlight=false&width=90pc)

#### Configure Display Options

1. Switch to the **Options** tab for number widget configuration
2. **Latest value**: Shows the value from the most recent period of your chosen time range
3. **Display most recent data points**: Enable to see latest updates even when not fully aggregated
4. **Display sparkline at bottom**: Enable to show the trend graph over time

![Invocation Display Options](/images/11/11-10.png?featherlight=false&width=90pc)

#### Duplicate Widget for Efficiency

1. To save time for future widgets, click the **3 dots** on any existing widget
2. Select **Duplicate** to create a copy with similar settings
3. This allows quick modification rather than starting from scratch

![Widget Duplication](/images/11/11-11.png?featherlight=false&width=90pc)

#### Result

Your invocation counter widget now displays the total number of Bedrock model calls with both current count and historical trend visualization. The sparkline provides quick insight into usage patterns over time.

{{% notice info %}}
The invocation counter helps you understand your application's usage frequency and can be crucial for capacity planning and cost optimization strategies.
{{% /notice %}}