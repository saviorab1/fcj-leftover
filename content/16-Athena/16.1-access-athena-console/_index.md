---
title : "Access Athena Console"
date : "2023-12-01T00:00:00Z"
weight : 1
chapter : false
pre : " <b> 16.1 </b> "
---

Navigate to Amazon Athena and set up the query environment for analyzing your S3 data using SQL queries.

#### Navigate to Athena Console

1. Go to the **AWS Management Console** and search for **Athena**
2. Click on **Athena** to access the service
3. Choose **Query your data with Trino SQL** option

![Athena Console](/images/16/16-1.png?featherlight=false&width=90pc)

#### Launch Query Editor

1. Click **Launch Query editor** to open the SQL interface
2. The Athena query editor will load with the default interface
3. You'll see the query workspace ready for database operations

![Launch Query Editor](/images/16/16-2.png?featherlight=false&width=90pc)

#### Result

Your Athena console is now ready for database and table creation. The query editor provides a SQL interface where you can execute commands to set up your analytics environment and query your S3 data.

{{% notice note %}}
Athena uses Trino SQL (formerly Presto SQL) as its query engine, providing fast, interactive analytics on large datasets stored in S3.
{{% /notice %}}