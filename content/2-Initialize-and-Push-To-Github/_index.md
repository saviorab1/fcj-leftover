---
title : "Initialize Git and Push Project to GitHub"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

#### Setting up Git and Push

After setting up the local Vite + React + TypeScript project, the next step was to version control the project and push it to a remote GitHub repository named AWS-leftover.

#### Create a GitHub respository for the workshop 

We will need to publish our Workshop so that the services on AWS such as Amplify can access, henceforth, a GitHub account is necessary. Prepare yourself a GitHub account. Once you are ready, in your profile, click on New.

![GitHub profile](/images/1/2-1.png?featherlight=false&width=90pc)

Name the respository as leftover. 

![GitHub repository](/images/1/2-2.png?featherlight=false&width=90pc)

Once you are finished with the creation, you should see the link that will connect you to your project. 

![GitHub link](/images/1/2-3.png?featherlight=false&width=90pc)

  > **Note:** Do remember that your GitHub link is private and it should only come from your GitHub profile, so we have to censor it for security and privacy reasons.

#### Intialize Git into the project.

**Minimum Permissions:**
To proceed with the following steps, you will need to follow these steps:

First, open up a new bash terminal and direct Git towards the project root directory:

```bash
git init
```

Then, select all the files that you want to update to your repository. In this case, it will be:

```bash
git add .
```

You will need to create an intial commit as well. 

```bash
git commit -m "first commit"
```

You will need to link your local repository to Github after that: 

```bash
git remote add origin https://github.com/*<your-username>*/leftover.git
```

Replace <your-username> with your actual GitHub username.

Then, you will set the branch to main.

```bash
git branch -M main
```

Finally, you will need to push the project up to Github.

```bash
git push -u origin main
```

Once completed, the project is hosted remotely and can be accessed, shared, or collaborated on via GitHub.

![Running The Project](/images/1/2-4.png?featherlight=false&width=90pc)

  > **Note:** "git add .", "git commit -m" and "git push" will be your way to save and publish your progress onto the repository.

# Result

The screenshot below shows the successfully initialized GitHub repository with the project directory and supporting files committed.

![Result](/images/1/2-5.png?featherlight=false&width=90pc)
