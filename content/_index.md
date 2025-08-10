---
title : "Overview"
date : "2025-08-10T20:24:00Z"
weight : -1
chapter : false

---

# Leftover – AI Recipe Generator Workshop

## Overview

Welcome to Leftover! We're going to build something pretty cool together – a smart recipe app that turns your random leftover ingredients into delicious meal ideas using AI.

Think about it: you've got some chicken, half an onion, and random spices sitting in your fridge. Instead of ordering takeout again, you'll just tell our app what you have, and it'll suggest amazing recipes you can actually make. No more food waste, no more "what's for dinner?" stress.

We'll use modern web technologies like React and TypeScript to build a sleek frontend, AWS Amplify to handle all the cloud stuff, and Amazon Bedrock to power the AI magic. Don't worry if some of these sound intimidating – we'll walk through everything step by step, and by the end, you'll have a fully working app that your friends will actually want to use.

## What We're Building
We're creating a modern web app that solves a real problem – turning random ingredients into great meals. But more than that, we're building something that showcases how easy it can be to integrate AI into everyday applications.

**What You'll Learn:**
1. **Modern Frontend Development** - Set up a React + TypeScript + Vite project from scratch and get it running with hot reload for instant feedback.

2. **Git & GitHub Integration** - Initialize version control, create a repository, and establish the foundation for collaborative development.

3. **AWS Amplify Deployment** - Connect your GitHub repo to Amplify, configure automated builds, and deploy your app to a live URL.

4. **Full-Stack Development** - Add authentication, set up backend services, and create data schemas that work seamlessly with your frontend.

5. **Enterprise Security** - Configure IAM Identity Center for secure team access and set up sandbox environments for safe development.

6. **AI Integration** - Connect Amazon Bedrock models (both single and cross-region) to power intelligent recipe generation.

7. **Production UI** - Build a polished frontend with proper assets, styling, and user experience.

8. **Monitoring & Analytics** - Set up CloudWatch dashboards to track performance, costs, and usage patterns.

9. **Data Pipeline** - Create S3 storage, Lambda functions, API Gateway endpoints, and Athena analytics for comprehensive data handling.



## Scope
This is a project to create a modern, smart, and scalable web application using cloud-native frameworks and technologies. The scope covers everything from environment setup to deployment as well as future readiness for integration with AI through AWS Bedrock.

**In Scope:**
1.	Frontend Development:
- Develop the application interface using React + TypeScript and Vite for fast development and high performance.

2.	Cloud Infrastructure Integration:
- Configure and initialize AWS Amplify for deployment, hosting, and management of CI/CD pipeline.
- Customize Amplify's amplify.yml for build and deployment automation.

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


## Solution Architecture

![Architecture Diagram](/images/0/0-1.png?featherlight=false&width=90pc)

### Architecture Overview

Our app follows a modern serverless architecture that's designed to be both powerful and easy to manage. Think of it like a well-organized kitchen – everything has its place and purpose.

The frontend is where users interact with our app. We're building it with React and TypeScript, which gives us a fast, responsive interface that feels smooth and professional. AWS Amplify hosts this frontend, handling all the technical stuff like SSL certificates and global content delivery, so your app loads quickly no matter where your users are.

Behind the scenes, we have our API layer that acts like the nervous system of our application. AWS AppSync provides a GraphQL API that keeps everything in sync in real-time, while API Gateway handles additional services. Lambda functions do the heavy lifting – they're like smart assistants that process requests, talk to the AI, and manage data without you having to worry about servers.

The AI magic happens through Amazon Bedrock, which gives us access to powerful language models without needing a PhD in machine learning. We've set up multi-region deployment so the AI responds quickly regardless of where your users are located, and intelligent model selection ensures we're always using the best AI for each type of request.

For data storage, we use Amazon S3 to keep user content, recipe images, and app assets safe and accessible. Amazon Athena helps us understand how people use the app by analyzing usage patterns and preferences, which helps us make it even better over time.

## Developer Sequence Diagram

![Developer Sequence](/images/0/0-2.png?featherlight=false&width=90pc)

### Your Development Journey

This diagram maps out your entire development experience from start to finish. Here's what happens at each stage:

**Initial Setup Phase**: You'll begin by accessing AWS through IAM Identity Center, which gives you secure, centralized access to all AWS services. This isn't just about security – it's about making your development workflow smooth and professional.

**Local Development**: Using your IDE (like VS Code), you'll create the Vite + React project locally. The AWS CLI becomes your command-line companion, letting you deploy and manage services directly from your terminal. You'll also use the Amplify CLI to scaffold backend services and manage your app's infrastructure as code.

**Service Configuration**: Through various AWS consoles (Amplify, Bedrock, S3, Lambda), you'll configure each service step by step. The beauty of this approach is that you're not just clicking buttons – you're learning how each piece fits together and why it matters.

**Sandbox Testing**: Before anything goes live, you'll deploy to a sandbox environment. This is your safe space to break things, experiment, and iterate without affecting production. It's like having a practice kitchen before cooking for guests.

**Continuous Integration**: Once you push code to GitHub, Amplify automatically builds and deploys your changes. This creates a professional development workflow where your code changes become live updates seamlessly.

**Monitoring and Iteration**: Using CloudWatch and other monitoring tools, you'll see how your app performs in real-time and make data-driven improvements.

## User Sequence Diagram

![User Sequence](/images/0/0-3.png?featherlight=false&width=90pc)

### The User Experience Journey

This diagram shows the magic that happens behind the scenes when someone uses your recipe app. Let's break down each step:

**Authentication Flow**: When users first visit your app, they'll create an account or sign in through AWS Cognito. This isn't just basic login – Cognito handles password security, email verification, and even social logins if you want to add them later. Users get secure JWT tokens that authenticate all their subsequent requests.

**Ingredient Input**: Once logged in, users interact with your beautiful React frontend to input their leftover ingredients. Maybe they have "chicken breast, bell peppers, and rice" sitting in their fridge. The interface is intuitive and responsive, built with TypeScript for reliability.

**Real-time Communication**: When they hit "Generate Recipe," the frontend sends this data through AWS AppSync using GraphQL. This isn't just a simple API call – AppSync provides real-time subscriptions, so users can see live updates as their recipe is being generated.

**AI Processing Pipeline**: AppSync triggers a Lambda function that acts as the orchestrator. This function takes the ingredient list, formats it properly, and sends it to Amazon Bedrock. Bedrock's AI models analyze the ingredients and generate creative, practical recipes with cooking instructions, prep time, and even nutritional information.

**Smart Response Delivery**: The generated recipe flows back through the same pipeline – Lambda processes the AI response, AppSync delivers it in real-time, and the React frontend displays it beautifully. Users see their personalized recipe appear almost instantly.

**Data Persistence**: Behind the scenes, user interactions are logged to S3 for analytics. This helps you understand what ingredients are popular, which recipes users love, and how to improve the app over time. All of this happens transparently while maintaining user privacy.

**The Result**: In just a few seconds, users go from "I don't know what to cook" to having a complete, personalized recipe based on what they actually have available. It's like having a professional chef in their pocket.

## Prerequisites

- AWS Account with appropriate permissions
- Node.js 18+ and npm/yarn
- Git and GitHub account
- Basic knowledge of React and TypeScript
- AWS CLI configured

## Workshop Modules

1. [Setting Up Vite Development Environment](../1-setting-up-vite/)
2. [Initialize and Push To Github](../2-initialize-and-push-to-github/)
3. [Setting Up Amplify](../3-setting-up-amplify/)
4. [Deploy The Application via AWS Amplify](../4-deploy-the-application-via-aws-amplify/)
5. [Setting Up Frontend And Backend](../5-setting-up-frontend-and-backend/)
6. [Setup IAM Identity Center](../6-setup-iam-identity-center/)
7. [Setting Up Sandbox](../7-setting-up-sandbox/)
8. [Setting Up Amazon Bedrock Legacy](../8-setting-up-amazon-bedrock-legacy/)
9. [Setting Up Amazon Bedrock Cross Region](../9-setting-up-amazon-bedrock-cross-region/)
10. [Create The Website Frontend](../10-create-the-website-frontend/)
11. [Monitoring with CloudWatch](../11-monitoring-with-cloudwatch/)
12. [S3 Bucket For Data Storage](../12-s3-bucket-for-data-storage/)
13. [Setup IAM Role for Lambda](../13-setup-iam-role-for-lambda/)
14. [Create Lambda Function for Data Collection](../14-create-lambda-function-for-data-collection/)
15. [Create REST API with API Gateway](../15-create-rest-api-with-api-gateway/)
16. [Athena Analytics](../16-athena/)
