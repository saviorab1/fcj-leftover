---
title : "Query and Analyze Data"
date : "2025-08-10T20:24:00Z"
weight : 4
chapter : false
pre : " <b> 16.4 </b> "
---

Execute SQL queries to analyze user interaction patterns and export results for further analysis and reporting.

#### Repair Table Partitions

1. Before querying data, run the following command to discover existing partitions:

```sql
MSCK REPAIR TABLE leftover_analytics.user_inputs;
```

2. Click **Run** to execute the partition repair command
3. This command scans your S3 location and adds any existing partitions to the table metadata

![Execute Query](/images/16/16-6.png?featherlight=false&width=90pc)

#### Execute Sample Query

1. Create a new query to test your table configuration
2. Enter the following SQL command to retrieve recent user inputs:

```sql
SELECT * FROM "leftover_analytics"."user_inputs" LIMIT 10
```

3. Click **Run** to execute the query and view results

![Execute Query](/images/16/16-7.png?featherlight=false&width=90pc)

#### View Query Results

1. After running the query, results will appear in the **Results** section below
2. The data table shows your collected user interaction data
3. You can scroll through columns to see all captured information

![Query Results](/images/16/16-8.png?featherlight=false&width=90pc)

#### Analyze Data Patterns

**Common Analysis Queries:**

**Most Popular Ingredients:**
```sql
SELECT rawInput, COUNT(*) as frequency 
FROM "leftover_analytics"."user_inputs" 
GROUP BY rawInput 
ORDER BY frequency DESC 
LIMIT 20
```

**Daily Usage Patterns:**
```sql
SELECT year, month, day, COUNT(*) as daily_requests 
FROM "leftover_analytics"."user_inputs" 
GROUP BY year, month, day 
ORDER BY year, month, day
```

**User Session Analysis:**
```sql
SELECT userId, COUNT(DISTINCT sessionId) as sessions, COUNT(*) as total_requests 
FROM "leftover_analytics"."user_inputs" 
GROUP BY userId 
ORDER BY total_requests DESC
```

#### Export Results

1. After executing any query, locate the **Download results** option
2. Click the download button to export data as a CSV file
3. The exported file contains all query results for external analysis

![Export Results](/images/16/16-9.png?featherlight=false&width=90pc)

#### Visualization and Reporting

1. **Data Insights**: Use the results to understand user behavior patterns
2. **Trend Analysis**: Identify popular ingredients and usage trends
3. **Performance Metrics**: Track application usage over time
4. **User Engagement**: Analyze session patterns and user retention

#### Result

Your Athena setup is now complete and functional. You can query your user interaction data using standard SQL, analyze patterns, and export results for further processing. The partitioned table structure ensures efficient and cost-effective analytics on your growing dataset.

**Analytics Capabilities:**
- **Real-time Querying**: Query data as soon as it's written to S3
- **Cost-effective Analysis**: Pay only for data scanned during queries
- **Scalable Performance**: Handle growing datasets without infrastructure management
- **Standard SQL**: Use familiar SQL syntax for complex analytics
- **Export Flexibility**: Download results in CSV format for external tools

{{% notice info %}}
Regular analysis of user interaction data helps optimize your recipe application by understanding user preferences, popular ingredients, and usage patterns.
{{% /notice %}}

{{% notice tip %}}
Consider setting up scheduled queries or connecting Athena to visualization tools like Amazon QuickSight for automated reporting and dashboard creation.
{{% /notice %}}
