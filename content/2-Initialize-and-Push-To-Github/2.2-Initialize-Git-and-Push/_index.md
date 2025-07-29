---
title : "Initialize Git and Push"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

#### Initialize Local Git Repository

After creating the GitHub repository, you need to initialize Git in your local project and push the code to the remote repository.

#### Navigate to Project Directory

1. Open a terminal or command prompt.
2. Navigate to your `leftover` project directory:

```bash
cd leftover
```

#### Initialize Git Repository

Initialize Git version control in your project:

```bash
git init
```

This command creates a new Git repository in the current directory.

#### Stage Project Files

Add all project files to the Git staging area:

```bash
git add .
```

This command stages all files in the project directory for the initial commit.

#### Create Initial Commit

Create the first commit with your project files:

```bash
git commit -m "Initial commit: Vite React TypeScript project setup"
```

![Git Commands](/images/2/2-4.png?featherlight=false&width=90pc)

#### Connect to Remote Repository

Link your local repository to the GitHub repository:

```bash
git remote add origin https://github.com/your-username/leftover.git
```

Replace `your-username` with your actual GitHub username.

#### Set Main Branch

Ensure you're working with the main branch:

```bash
git branch -M main
```

#### Push to GitHub

Push your local repository to GitHub:

```bash
git push -u origin main
```

![Push to GitHub](/images/2/2-5.png?featherlight=false&width=90pc)

The `-u` flag sets up tracking between your local main branch and the remote main branch.

#### Verify Repository Upload

1. Return to your GitHub repository page in the browser.
2. Refresh the page to see your uploaded project files.
3. Verify that all project files and folders are present.

#### Result

Your project is now successfully version-controlled and hosted on GitHub with:
- Complete project history tracked in Git
- Remote backup of your code on GitHub
- Ready for AWS service integration and deployment

{{% notice note %}}
Use `git add .`, `git commit -m "message"`, and `git push` for future updates to save and publish your progress to the repository.
{{% /notice %}}