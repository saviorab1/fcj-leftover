---
title : "Initialize Amplify Project"
date : "2025-08-10T20:24:00Z"
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---

#### Access Project Directory

To set up AWS Amplify for your application, you need to initialize it within your existing Vite project directory.

#### Navigate to Project Root

1. Ensure you are in the `leftover` project directory.
2. Open a terminal or command prompt in the project root.
3. Verify you can see the `package.json` and other project files.

#### Initialize Amplify

Execute the following command to create a new Amplify project:

```bash
npm create amplify@latest -y
```

![Initialize Amplify](/images/3/3-1.png?featherlight=false&width=90pc)

This command performs the following actions:
- Downloads and installs the latest Amplify CLI tools
- Creates the basic Amplify project structure
- Sets up configuration files for AWS resource management
- Automatically confirms all prompts with the `-y` flag

{{% notice info %}}
The Amplify initialization creates a foundation for integrating AWS services like authentication, APIs, storage, and hosting into your application.
{{% /notice %}}

#### Verify Project Structure

After successful initialization, you should see:
- A new `amplify/` directory in your project root
- Amplify configuration files and folders
- Backend environment settings and resource definitions

#### Check Amplify Directory

The `amplify/` directory contains:
- Backend configuration files
- Resource definitions for AWS services
- Environment-specific settings
- Deployment configurations

![Amplify Directory](/images/3/3-2.png?featherlight=false&width=90pc)

#### Result

Your project now has AWS Amplify initialized and is ready for backend service configuration and version control in the next step.
