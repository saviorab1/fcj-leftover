---
title : "Implement Data Collection Code"
date : "2025-08-10T20:24:00Z"
weight : 2
chapter : false
pre : " <b> 14.2 </b> "
---

#### Access Function Code Editor

After creating the Lambda function, you need to implement the data collection logic.

#### Navigate to Code Source

1. Click on the **leftover-data-collector** function you just created.
2. Scroll down to the **Code source** section.
3. You will see the default `index.mjs` file in the code editor.

![Code Source](/images/14/14-5.png?featherlight=false&width=90pc)

#### Replace Default Code

1. Select all the existing code in the `index.mjs` file.
2. Replace it with the following data collection implementation:

```javascript
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

#### Deploy the Function

1. After replacing the code, click **Deploy** to save and deploy your changes.
2. The function will be updated with the new implementation.

![Deploy Function](/images/14/14-6.png?featherlight=false&width=90pc)

#### Code Functionality

This Lambda function provides the following capabilities:

**Data Processing**:
- Parses incoming JSON data from API requests
- Extracts ingredients, timestamp, user ID, and session ID

**Data Organization**:
- Creates date-based partitions (year/month/day) for efficient storage
- Generates unique filenames using session ID and timestamp

**S3 Integration**:
- Stores processed data in the `leftover-storage` bucket
- Includes metadata such as user agent and source IP

**CORS Support**:
- Enables cross-origin requests for web application integration

#### Result

Your Lambda function is now ready to collect and store user input data with proper organization and error handling.

{{% notice note %}}
The function automatically organizes data by date, making it easier to query and analyze user inputs over time.
{{% /notice %}}
