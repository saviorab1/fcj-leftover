---
title : "Create Vite Project"
date : "2025-08-10T20:24:00Z"
weight : 1
chapter : false
pre : " <b> 1.1 </b> "
---

#### Initialize Development Environment

To begin building the leftover ingredients application, you need to set up a modern development environment using Vite with React and TypeScript.

#### Create Project Directory

1. Open Visual Studio Code or your preferred code editor.
2. Create a new folder for your project workspace.
3. Open a terminal in the project directory.

#### Generate Vite Project

Execute the following command to create a new Vite project:

```bash
npm create vite@latest leftover -- --template react-ts -y
```

![Create Vite Project](/images/1/1-1.png?featherlight=false&width=90pc)

This command performs the following actions:
- Creates a new project named `leftover`
- Uses the React + TypeScript template
- Automatically confirms all prompts with the `-y` flag

{{% notice info %}}
Vite provides fast build times and hot module replacement (HMR) for an optimal development experience with modern React features and TypeScript support.
{{% /notice %}}

#### Verify Project Structure

After successful creation, you should see:
- Project folder `leftover` with all necessary files
- Package.json with React, TypeScript, and Vite dependencies
- Basic project structure with src/, public/, and configuration files

#### Result

Your Vite project is now scaffolded and ready for development server startup in the next step.
