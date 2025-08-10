---
title : "Configure External Table"
date : "2025-08-10T20:24:00Z"
weight : 3
chapter : false
pre : " <b> 16.3 </b> "
---

Define the external table schema to map your S3 data structure and enable efficient querying with date-based partitioning.

#### Create External Table Schema

1. Create a new query in the Athena editor
2. Enter the following SQL command to define the table structure:

```sql
CREATE EXTERNAL TABLE leftover_analytics.user_inputs (
  timestamp string,
  userId string,
  sessionId string,
  rawInput string,
  ingredientCount int,
)
PARTITIONED BY (
  year string,
  month string,
  day string
)
ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe'
LOCATION 's3://leftover-storage/user-inputs/'
TBLPROPERTIES ('has_encrypted_data'='false')
```

3. Click **Run** to execute the table creation command

![Create External Table](/images/16/16-5.png?featherlight=false&width=90pc)

#### Table Configuration Details

**Schema Definition:**
- **timestamp**: When the user interaction occurred
- **userId**: Identifier for the user (authenticated or anonymous)
- **sessionId**: Unique session identifier for tracking user sessions
- **rawInput**: The original ingredient input from the user
- **ingredientCount**: Number of ingredients provided
- **userAgent**: Browser/client information
- **sourceIP**: User's IP address for geographic analysis

**Partitioning Strategy:**
- **year/month/day**: Date-based partitioning for efficient querying
- Reduces data scanning costs by limiting queries to specific time periods
- Improves query performance for time-based analytics

**Data Format:**
- **JsonSerDe**: Handles JSON data parsing from S3 objects
- **S3 Location**: Points to your data collection bucket
- **Encryption**: Configured for unencrypted data (modify if using encryption)

#### Result

Your external table `user_inputs` is now configured to read JSON data from your S3 bucket with date-based partitioning. The table schema matches the data structure collected by your Lambda function, enabling comprehensive analysis of user interactions.

{{% notice warning %}}
Ensure your S3 bucket name matches the LOCATION parameter. Replace `leftover-storage` with your actual bucket name if different.
{{% /notice %}}

{{% notice tip %}}
Date partitioning significantly reduces query costs by scanning only relevant data. Athena charges based on the amount of data scanned, making partitioning essential for cost optimization.
{{% /notice %}}
