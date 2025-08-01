---
title : "Leftover – Creating a Smart Recipe Generator Website using Amazon Bedrock AI"
date : "2023-12-01T00:00:00Z"
weight : 1 
chapter : false
---

# Creating your first AWS account

#### Overview
Leftover suggests a new direction that integrates the latest cloud-native technologies. Vite + React + TypeScript is utilized for fast and modular frontend development, where AWS Amplify enables easy hosting, continuous deployment, and infrastructure management.

Looking ahead, the project also involves integrating AWS Bedrock, a robust foundation model service. With Bedrock, the application will be capable of integrating generative AI capabilities such as text generation, summarization, and intelligent search—without requiring teams to grapple with advanced machine learning infrastructure. This forward-thinking integration opens the door to a smarter, more responsive web application experience.

By combining rapid development tooling with scalable cloud and next-generation AI capabilities, this project addresses both the short-term pain points and long-term innovation opportunities.


#### Goals
Build and launch a modern web app using cloud technology and prepare it for future AI features. The goal is to replace old file-sharing tools with something faster, smarter, and more user-friendly—both for users and developers.

**Key Objectives:**
1. Make Frontend Development Fast and Smooth
- Use React, TypeScript, and Vite to build the app quickly and keep the code clean and modular.

Add features like hot module reload so developers can see changes instantly.

2. Deploy Automatically and at Scale
- Use AWS Amplify to handle app hosting and create a deployment pipeline.

- Connect with GitHub so changes go live through a smooth CI/CD process.

3. Get Ready for AI Integration
- Design the system so that it's easy to plug in AI services (like AWS Bedrock) later.

- This will allow features like smart search, AI-generated content, and insight automation in the future.

4. Follow Cloud Best Practices
- Use modern DevOps techniques (automation, caching, config files) to keep things fast and efficient.

- Make sure the app runs well at scale and is easy for developers to work with.

5. Work Together Securely and Smoothly
- Let multiple developers contribute safely using GitHub + Amplify environments.

- Make deployment steps repeatable and easy for long-term success and growth.



#### Scope
This is a project to create a modern, smart, and scalable web application using cloud-native frameworks and technologies. The scope covers everything from environment setup to deployment as well as future readiness for integration with AI through AWS Bedrock.

**In Scope:**
1.	Frontend Development:
- Develop the application interface using React + TypeScript and Vite for fast development and high performance.

2.	Cloud Infrastructure Integration:
- Configure and initialize AWS Amplify for deployment, hosting, and management of CI/CD pipeline.
- Customize Amplify’s amplify.yml for build and deployment automation.

3.	Source Control & Repository Management:
- Set up and manage the GitHub repository with commit history, branch handling, and integration with Amplify.

4.	Build and Deployment Process:
- Configure build artifacts, cache directories, and deploy the application to a live domain using Amplify Hosting.
- Support automatic redeployment via GitHub commits.

5.	AI-Ready Architecture:
- Design project structure to be compatible with future AWS Bedrock integration for embedding generative AI features.

**Out of Scope:**
1.	Backend API Development:
- Custom backend APIs and logic are not implemented in this phase, other than as introduced via Amplify defaults.

2.	Full AWS Bedrock Integration:
- Although the project is configured for AI integration, actual Bedrock services (i.e., text generation, embeddings) are not activated during this workshop phase.

3.	Production-Grade Security & Access Control:
- There is no complex access control, authentication, or fine-grained security roles in the project yet.

4.	Complex Multi-Environment Configurations:
- The Scope is a single environment deployment (i.e., main branch to Amplify hosting).


#### Solution Architecture

![Role Details](/images/1/0-1.png?featherlight=false&width=90pc)

This architecture shows how a web app and a developer interact with a secure AI system hosted on AWS Cloud.

**For Users:**
- A user accesses the app via a web browser.

- AWS Cognito verifies identity and gives secure credentials.

- AWS Amplify hosts the React frontend.

- Frontend uses AppSync (GraphQL) to talk to backend services.

**AI Request Flow:**
- AppSync sends a request to the Invoke Agent Handler (Lambda).

- This handler talks to either Region-1 or Region-2 AI models.

- Each region has inference profiles that choose a specific AI model to run.

- The model returns a result which flows back to the frontend.

**For Developers:**
- Developers access AWS services through IDE.

- IAM Identity Center gives access and credentials.

- They use a Sandbox environment for safe testing.

**Data Handling:**
Requests to API Gateway can:

- Trigger Lambda functions for storage

- Use IAM to get permission

- Store data in S3 bucket

- Analyze it via Amazon Athena

**Shared Tools:**
AWS tools like CDK, CloudFormation, CloudTrail, CLI, CloudWatch help with development, monitoring, and deployment.



#### IAM User
An **IAM user** is an entity that you create in AWS to represent the person or application that uses it to interact with AWS. A user in AWS consists of a name and credentials. \
Please note that an IAM user with administrator permissions is not the same thing as the AWS account root user.


#### AWS Support
AWS Basic Support offers all AWS customers access to our Resource Center, Service Health Dashboard, Product FAQs, Discussion Forums, and Support for Health Checks – at no additional charge. Customers who desire a deeper level of support can subscribe to AWS Support at the Developer, Business, or Enterprise level.

Customers who choose AWS Support gain one-on-one, fast-response support from AWS engineers. The service helps customers use AWS's products and features. With pay-by-the-month pricing and unlimited support cases, customers are freed from long-term commitments. Customers with operational issues or technical questions can contact a team of support engineers and receive predictable response times and personalized support.


#### Main Content

1. [Creating a new AWS Account](1-create-new-aws-account/)
2. [Setting up MFA for the AWS Account root user](2-MFA-Setup-For-AWS-User-(root))
3. [Creating an Administrator Accounts and Groups](3-create-admin-user-and-group/)
4. [Getting support for Account Authentication](4-verify-new-account/)
<!-- need to remove parenthesis for path in Hugo 0.88.1 for Windows-->
