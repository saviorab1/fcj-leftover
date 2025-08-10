---
title : "Create Database and Table"
date : "2025-08-10T20:24:00Z"
weight : 2
chapter : false
pre : " <b> 16.2 </b> "
---

Set up a dedicated database for your analytics workload and prepare the foundation for data analysis.

#### Create Analytics Database

1. In the **Query window**, enter the following SQL command:
   ```sql
   CREATE DATABASE leftover_analytics
   ```
2. Click **Run** to execute the database creation command
3. The database will be created and available for use

![Create Database](/images/16/16-3.png?featherlight=false&width=90pc)

#### Select New Database

1. On the left sidebar, locate the **Database** dropdown
2. Select **leftover_analytics** from the available databases
3. This sets the context for subsequent table operations

![Select Database](/images/16/16-4.png?featherlight=false&width=90pc)

#### Result

Your analytics database `leftover_analytics` is now created and selected. This database will serve as the container for all tables related to your user data analysis, providing organized access to your S3-stored information.

{{% notice info %}}
Creating a dedicated database helps organize your analytics tables and provides a clear namespace for your data analysis operations.
{{% /notice %}}
