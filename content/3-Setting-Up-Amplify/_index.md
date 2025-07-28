---
title : "Setting Up Amplify For The Project"
date : "2023-12-01T00:00:00Z"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

####  Intializing Amplify in the project

First, you will need to use the npm command: 

```bash
npm create amplify@latest -y
```

This command sets up a minimal Amplify project, preparing the application for AWS resource integration.

#### Project Structure Update and Version Control Reminder

Upon successful execution, an amplify/ directory is generated in the root folder of the project. This directory contains all configurations and backend environment settings related to Amplify.

After this change, remember to commit and push the updates to the GitHub repository:

```bash
git add .
git commit -m "Add AWS Amplify setup"
git push
```

![Result](/images/1/3-1.png?featherlight=false&width=90pc)

#### Results
The screenshot below highlights the newly added amplify folder in the project directory, confirming successful initialization.

![Result](/images/1/3-2.png?featherlight=false&width=90pc)
