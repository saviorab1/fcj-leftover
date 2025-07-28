---
title : "Set up Athena for analysis"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

Go to Athena console → choose Query your data with Trino SQL → click Launch Query editor

 ![Logo](/images/5/18-1.png?featherlight=false&width=90pc)

Click on Create → Create Table

 ![Logo](/images/5/18-2.png?featherlight=false&width=90pc)

On Query window, type in this line and click Run
CREATE DATABASE leftover_analytics
On the left handside, under Database dropbox, choose the new table we just created

 ![Logo](/images/5/18-3.png?featherlight=false&width=90pc)

Then, create another query and type in these lines and click Run:

```bash
CREATE EXTERNAL TABLE leftover_analytics.user_inputs ( timestamp string, userId string, sessionId string, rawInput string, ingredientCount int, userAgent string, sourceIP string
)
PARTITIONED BY ( year string, month string, day string
)
ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe'
LOCATION 's3://leftover-storage/user-inputs/'
TBLPROPERTIES ('has_encrypted_data'='false')
```

 ![Logo](/images/5/18-4.png?featherlight=false&width=90pc)

The database will now partitioned by date and save to the location you chose within the S3 bucket (In this case, it is in leftover-storage/users-input). You can then query any data you would like within the storage and download it as CSV file. 
For examples, you can see the last 10 prompts by using this line:

```bash
SELECT * FROM "leftover_analytics"."user_inputs" limit 10
```

Here should be the results that you should be getting after. 

 ![Logo](/images/5/18-5.png?featherlight=false&width=90pc)
 ![Logo](/images/5/16-6.png?featherlight=false&width=90pc)

