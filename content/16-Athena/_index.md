---
title : "Set up Athena for analysis"
date : "2023-12-01T00:00:00Z"
weight : 16
chapter : false
pre : " <b> 16. </b> "
---

AWS Athena is a serverless interactive query service that lets you analyze data in Amazon S3 using standard SQL. You simply point Athena to your S3 data, define the schema, and start running queries without needing to load the data into a separate database. It’s cost-effective since you only pay for the amount of data scanned, making it ideal for quick analytics on large datasets.

#### Create Lambda Function

Go to Athena console → choose Query your data with Trino SQL → click Launch Query editor

![Role Details](/images/16/16-1.png?featherlight=false&width=90pc)

Click on Create → Create Table
 
![Role Details](/images/16/16-2.png?featherlight=false&width=90pc)

On Query window, type in this line and click Run
CREATE DATABASE leftover_analytics
On the left handside, under Database dropbox, choose the new table we just created

![Role Details](/images/16/16-3.png?featherlight=false&width=90pc)
 
Then, create another query and type in these lines and click Run:
CREATE EXTERNAL TABLE leftover_analytics.user_inputs ( timestamp string, userId string, sessionId string, rawInput string, ingredientCount int, userAgent string, sourceIP string
)
PARTITIONED BY ( year string, month string, day string
)
ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe'
LOCATION 's3://leftover-storage/user-inputs/'
TBLPROPERTIES ('has_encrypted_data'='false')
 
![Role Details](/images/16/16-4.png?featherlight=false&width=90pc)

The database will now partitioned by date and save to the location you chose within the S3 bucket (In this case, it is in leftover-storage/users-input). You can then query any data you would like within the storage and download it as CSV file. 
For examples, you can see the last 10 prompts by using this line:
SELECT * FROM "leftover_analytics"."user_inputs" limit 10

And after you run the code, you should see the box at below, which is shown at the bottom of this screenshot.

![Role Details](/images/16/16-5.png?featherlight=false&width=90pc)

You can check the dataset and the graph. Furthermore, you can export CSV file as well.

![Role Details](/images/16/16-6.png?featherlight=false&width=90pc)
