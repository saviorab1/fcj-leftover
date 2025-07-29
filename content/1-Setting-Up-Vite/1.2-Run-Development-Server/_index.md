---
title : "Run Development Server"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 1.2 </b> "
---

#### Navigate to Project Directory

After creating the Vite project, you need to enter the project folder and start the development server.

#### Enter Project Folder

Navigate to the newly created project directory:

```bash
cd leftover
```

This command changes your current directory to the `leftover` project folder where all the project files are located.

#### Install Dependencies

Install the required project dependencies:

```bash
npm install
```

This step ensures all packages specified in package.json are properly installed.

#### Start Development Server

Launch the development server with the following command:

```bash
npm run dev
```

![Development Server](/images/1/1-2.png?featherlight=false&width=90pc)

The development server will start and display:
- Local server URL (typically http://localhost:5173)
- Network URL for accessing from other devices
- Hot module replacement (HMR) status

#### Access the Application

1. Open your web browser and navigate to **http://localhost:5173**.
2. You should see the default Vite + React welcome screen.
3. The page displays the Vite and React logos with a counter button.

![Application Running](/images/1/1-3.png?featherlight=false&width=90pc)

#### Test Hot Module Replacement

1. Open `src/App.tsx` in your code editor.
2. Make a small change to the text or styling.
3. Save the file and observe the browser automatically update without refresh.

#### Result

Your Vite development environment is now running successfully with:
- Fast development server with HMR enabled
- React + TypeScript configuration ready for development
- Live reloading for efficient development workflow

{{% notice note %}}
The development server will continue running until you stop it with Ctrl+C. Keep it running while developing your application.
{{% /notice %}}