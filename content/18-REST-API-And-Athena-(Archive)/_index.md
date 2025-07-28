---
title : "Update API and Athena (Archive)"
date : "2023-12-01T00:00:00Z"
weight : 18
chapter : false
pre : " <b> 18. </b> "
---

**Content:**
- [Creating and Updating a REST API with an API Gateway](#creating-and-updating-a-rest-api-with-an-api-gateway)
- [Setting up Athena](#setting-up-athena)

## Creating and Updating a REST API with an API Gateway

To collect user data from your app, you’ll need to build and connect to an API using AWS API Gateway and Lambda.

1. Create a REST API in API Gateway, define the /collect-data resource, and integrate it with your Lambda function using POST method and Lambda Proxy Integration.

2. Enable CORS for the endpoint so it can be accessed from your frontend application (e.g., React).

3. Deploy the API with a stage name (e.g., prod) and copy the invoke URL.

4. Update your frontend (e.g., App.tsx) to send data (ingredients, user info, timestamp) to this new API endpoint.

The API collects and logs user inputs server-side. You’ll find the full API Gateway URL in the POST → ARN section.

## Setting up Athena

To analyze user data stored in S3, Amazon Athena lets you query it directly using SQL.

1. Open the Athena console and launch the Query Editor. Create a new database for analytics.

2. Set up an external table that connects to your S3 bucket containing user input data, and define how the data is structured and partitioned (e.g. by year, month, day).

3. Once the table is created, you can run queries to filter, analyze, and export the results.



