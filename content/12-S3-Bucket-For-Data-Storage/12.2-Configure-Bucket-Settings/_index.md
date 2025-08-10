---
title : "Configure Bucket Settings"
date : "2025-08-10T20:24:00Z"
weight : 2
chapter : false
pre : " <b> 12.2 </b> "
---

#### Basic Configuration Settings

Configure the essential settings for your S3 bucket to ensure proper functionality and security.

#### Set Bucket Name and Region

Configure the following basic settings:

**Bucket name**: `leftover-storage`
- Must be globally unique across all AWS accounts
- Use lowercase letters, numbers, and hyphens only

**Region**: `ap-southeast-1` (Singapore)
- Choose the same region as your Amplify app for optimal performance

![Basic Configuration](/images/12/12-3.png?featherlight=false&width=90pc)

{{% notice info %}}
If "leftover-storage" is already taken, append a unique identifier like your initials or numbers (e.g., "leftover-storage-abc123").
{{% /notice %}}

#### Security Configuration

**Block Public Access Settings**:
- Keep all four settings checked to ensure your data remains private
- This prevents accidental public exposure of your bucket contents

![Security Settings](/images/12/12-4.png?featherlight=false&width=90pc)

#### Advanced Features

**Bucket Versioning**: 
- Enable versioning for data integrity and recovery capabilities

**Default Encryption**:
- Enable with **SSE-S3** (Server-Side Encryption with Amazon S3-Managed Keys)
- This ensures all objects stored in the bucket are automatically encrypted

![Advanced Settings](/images/12/12-5.png?featherlight=false&width=90pc)

#### Result

Your bucket configuration is now complete and ready for creation in the next step.
