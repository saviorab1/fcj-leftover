---
title : "Build the Lambda"
date : "2023-12-01T00:00:00Z"
weight : 3
chapter : false
pre : " <b> 4.3 </b> "
---

## Content
- [Set up IAM role for Lambda](#set-up-iam-role-for-lambda)
- [Create Lambda function for data collection](#create-lambda-function-for-data-collection)

## Set up IAM role for Lambda

Go to IAM console → Roles → Create Role

 ![Logo](/images/4/14-1.png?featherlight=false&width=90pc)

Choose AWS Service for Trusted entity and Lambda for Use case in the first step

 ![Logo](/images/4/14-2.png?featherlight=false&width=90pc)

For Permissions Policies, choose AWSLambdaBasicExecutionRole.

 ![Logo](/images/4/14-3.png?featherlight=false&width=90pc)

For Role name, we named it LeftoverDataCollectionRole, but you can pick your own poison to be fair. Afterward, go back to the Roles tab and click on the role we just created. Click on Add permissions → Create inline policy.

 ![Logo](/images/4/14-4.png?featherlight=false&width=90pc)

In the Policy Editor, switch to JSON.

 ![Logo](/images/4/14-5.png?featherlight=false&width=90pc)

Then replace the text with these line of codes:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:PutObjectAcl",
                "s3:GetObject"
            ],
            "Resource": "arn:aws:s3:::leftover-storage/*" 
        }
    ]
}
```

Here should be the result:

 ![Logo](/images/4/14-6.png?featherlight=false&width=90pc)

## Create Lambda function for data collection

Go to Lambda Console → click Create Function 

 ![Logo](/images/4/15-1.png?featherlight=false&width=90pc)

•	Function name: leftover-data-collector
•	Runtime: Node.js 22.x
•	Architecture: x86_64
•	Execution role: Use existing role → LeftoverDataCollectionRole
Fill that out and click Create function

 ![Logo](/images/4/15-2.png?featherlight=false&width=90pc)

Click on the new Lambda function we just created, in Code source, index.js, replace it with this snippet:

```js
import { S3Client, PutObjectCommand } from "@aws-sdk/client-s3";

const s3Client = new S3Client({ region: "ap-southeast-1" });

export const handler = async (event) => {
    try {
        const { ingredients, timestamp, userId, sessionId } = JSON.parse(event.body);
        
        // Create partition path based on date
        const date = new Date(timestamp);
        const year = date.getFullYear();
        const month = String(date.getMonth() + 1).padStart(2, '0');
        const day = String(date.getDate()).padStart(2, '0');
        
        // Create unique filename
        const filename = `${sessionId}-${Date.now()}.json`;
        const key = `user-inputs/year=${year}/month=${month}/day=${day}/${filename}`;
        
        // Prepare data for storage
        const dataToStore = {
            timestamp,
            userId,
            sessionId,
            ingredients: ingredients.split(',').map(ing => ing.trim()),
            ingredientCount: ingredients.split(',').length,
            rawInput: ingredients,
            metadata: {
                userAgent: event.headers['User-Agent'] || 'unknown',
                sourceIP: event.requestContext?.identity?.sourceIp || 'unknown'
            }
        };
        
        // Store in S3
        const command = new PutObjectCommand({
            Bucket: 'leftover-storage',
            Key: key,
            Body: JSON.stringify(dataToStore),
            ContentType: 'application/json'
        });
        
        await s3Client.send(command);
        
        return {
            statusCode: 200,
            headers: {
                'Access-Control-Allow-Origin': '*',
                'Access-Control-Allow-Headers': 'Content-Type',
                'Access-Control-Allow-Methods': 'POST, OPTIONS'
            },
            body: JSON.stringify({ 
                message: 'Data stored successfully',
                key: key 
            })
        };
        
    } catch (error) {
        console.error('Error storing data:', error);
        return {
            statusCode: 500,
            headers: {
                'Access-Control-Allow-Origin': '*'
            },
            body: JSON.stringify({ 
                error: 'Failed to store data' 
            })
        };
    }
};
```