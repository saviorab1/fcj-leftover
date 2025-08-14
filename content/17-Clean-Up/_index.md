---
title : "Clean Up AWS Resources"
date : "2025-08-10T20:24:00Z"
weight : 17
chapter : false
pre : " <b> 17. </b> "
---

**Content:**
- [Clean Up Athena](17.1-clean-up-athena/)
- [Delete API Gateway](17.2-delete-api-gateway/)
- [Remove Lambda Resources](17.3-remove-lambda-resources/)
- [Remove IAM Roles](17.4-remove-iam-roles/)
- [Delete S3 Bucket](17.5-delete-s3-bucket/)
- [Delete CloudWatch Dashboard](17.6-delete-cloudwatch-dashboard/)
- [Revoke Bedrock Model Access](17.7-revoke-bedrock-model-access/)
- [Delete Amplify App](17.8-delete-amplify-app/)
- [Delete IAM Identity Center Instance](17.9-delete-iam-identity-center/)

Decommission all resources provisioned throughout the workshop to avoid incurring ongoing costs. Follow the steps in order.

{{% notice warning %}}
These actions are irreversible and will permanently remove data and configurations. Double-check resource names before deleting.
{{% /notice %}}

#### What You'll Do

1. Drop the Athena database used for analytics.
2. Delete the project API in API Gateway.
3. Remove Lambda functions and the related application.
4. Delete IAM roles created for the project.
5. Empty and delete the S3 bucket storing data.
6. Remove the CloudWatch dashboard.
7. Revoke Amazon Bedrock model access.
8. Delete the AWS Amplify application.
9. Delete the IAM Identity Center instance used for sandbox access.


