---
title : "Setting Up Vite"
date : "2023-12-01T00:00:00Z"
weight : 1
chapter : false
pre : " <b> 1. </b> "
---



#### Set Up The Vite, React and TypeScript

To kick off the development environment, we initialized the project with Vite, a next-generation frontend tooling system that offers fast build times and hot module replacement (HMR). We selected the React + TypeScript template to simplify development with type safety and modern React features.

#### Create the project using Vite

Create a new project by making a new folder and direct to it inside the Visual Studio Code. After the folder is created, use this command:

```bash
npm create vite@latest leftover -- --template react-ts -y
```

![Create A Development Site](/images/1/1-1.png?featherlight=false&width=90pc)

This command scaffolds a new Vite project named leftover with the React + TypeScript template.

#### Navigate and run the development template

Navigate towards the folder that you just created with this command. 

```bash
cd leftover
```

Then, to run the program after being set up.

```bash
npm run dev
```

![Running The Project](/images/1/1-2.png?featherlight=false&width=90pc)

#### Result

Once the server is running, the development version of the application becomes accessible at:
**http://localhost:5173**


The successful launch displays a default welcome screen with the Vite + React logo, a counter button, and instructions to test hot module replacement by editing the src/App.tsx file.


![Result](/images/1/1-3.png?featherlight=false&width=90pc)


