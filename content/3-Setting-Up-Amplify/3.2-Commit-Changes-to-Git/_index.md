---
title : "Commit Changes to Git"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

#### Save Amplify Configuration

After initializing Amplify, you need to commit the new configuration files to version control to track changes and enable team collaboration.

#### Stage Amplify Files

Add all the new Amplify-related files to Git staging:

```bash
git add .
```

This command stages all new files and directories created by the Amplify initialization, including:
- The `amplify/` directory and its contents
- Configuration files
- Any updated package files

#### Create Commit

Create a descriptive commit message for the Amplify setup:

```bash
git commit -m "Add AWS Amplify setup and configuration"
```

This commit captures the current state of your project with Amplify initialized.

#### Push to GitHub

Push the changes to your remote GitHub repository:

```bash
git push
```

#### Verify Repository Update

1. Navigate to your GitHub repository in the browser.
2. Refresh the page to see the new commits.
3. Verify that the `amplify/` directory appears in the repository.

![Repository Updated](/images/3/3-3.png?featherlight=false&width=90pc)

#### Project Structure Confirmation

Your project now includes:
- Original Vite + React + TypeScript files
- Git version control with GitHub integration
- AWS Amplify configuration and backend setup
- Complete project history tracked in version control

#### Result

Your project is now successfully configured with AWS Amplify and all changes are committed to version control, providing:
- Backend service integration capabilities
- Proper version control of Amplify configurations
- Team collaboration support through GitHub
- Foundation for AWS resource deployment

{{% notice note %}}
Always commit Amplify configuration changes to maintain consistency across development environments and enable proper deployment workflows.
{{% /notice %}}