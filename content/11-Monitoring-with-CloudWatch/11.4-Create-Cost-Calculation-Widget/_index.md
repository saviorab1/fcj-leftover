---
title : "Create Cost Calculation Widget"
date : "2025-08-10T20:24:00Z"
weight : 4
chapter : false
---

Implement mathematical functions to calculate real-time costs based on Bedrock token usage and pricing models.

#### Duplicate and Edit Widget

1. Click the **3 dots** on an existing widget and select **Duplicate**
2. On the new duplicated widget, click the **3 dots** again and choose **Edit**
3. This provides a foundation for adding cost calculation functions

![Widget Duplication and Edit](/images/11/11-12.png?featherlight=false&width=90pc)

#### Add Mathematical Functions

1. In the top-right of the graphed metrics section, click **Add math**
2. Choose **All functions** from the dropdown menu
3. Select any function initially (you'll modify it to fit your specific cost calculation needs)

![Add Math Functions](/images/11/11-13.png?featherlight=false&width=90pc)

#### Configure Cost Calculation Formulas

1. Click the **pen icon** in the details tab of the newly created metrics to modify equations
2. Implement the cost calculation based on Bedrock pricing:
   - **Input tokens**: $0.003 per 1000 tokens
   - **Output tokens**: $0.015 per 1000 tokens

![Edit Math Equations](/images/11/11-14.png?featherlight=false&width=90pc)

#### Implement Cost Formulas

Configure the mathematical expressions for cost tracking:

**Total Token Cost Formula:**
```
(m2*0.003/1000)+(m1*0.015/1000)
```
Where:
- `m2` = Input token count
- `m1` = Output token count

**Average Cost Per Invocation:**
```
e1/m3
```
Where:
- `e1` = Total cost calculation result
- `m3` = Total invocations

**Important**: Uncheck unnecessary metrics from the graphs to prevent confusion and focus on cost data.

![Cost Formula Implementation](/images/11/11-15.png?featherlight=false&width=90pc)

#### Optimize Display Settings

1. Switch to the **Options** tab for final configuration
2. **Show as many digits as can fit**: Enable before rounding to see precise small costs
3. **Latest value**: Choose to show from the most recent period of your time range
4. **Display sparkline at bottom**: Enable for trend visualization

![Display Optimization](/images/11/11-16.png?featherlight=false&width=90pc)

#### Complete Dashboard Setup

Apply the same mathematical approach to create additional cost-related metrics as needed. Your final dashboard should display comprehensive monitoring including:

- Token usage trends (input/output)
- Total invocation counts
- Real-time cost calculations
- Cost per invocation metrics

![Complete Dashboard](/images/11/11-17.png?featherlight=false&width=90pc)

#### Result

Your CloudWatch dashboard now provides complete visibility into your Bedrock application's performance and costs. The mathematical functions automatically calculate expenses based on actual token usage, enabling proactive cost management and optimization.

{{% notice warning %}}
Monitor your cost calculations regularly to ensure they align with current AWS Bedrock pricing. Pricing may change, requiring formula updates to maintain accuracy.
{{% /notice %}}

{{% notice tip %}}
Set up CloudWatch alarms based on these cost metrics to receive notifications when usage exceeds your defined thresholds, helping prevent unexpected charges.
{{% /notice %}}
