---
title : "Configure Build Settings"
date : "2023-12-01T00:00:00Z"
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

#### Set Up Build Configuration

After connecting your repository, you need to configure the build settings for your Vite React application.

#### Review App Settings

1. Amplify will automatically detect your app settings and suggest a build configuration.
2. Review the detected framework (should show Vite or React).
3. Verify the build commands and output directory settings.

![App Settings](/images/4/4-4.png?featherlight=false&width=90pc)

#### Edit Build Specification

1. Click **Edit** next to the build settings or **Edit YML file**.
2. This opens the amplify.yml configuration editor.

#### Configure amplify.yml File

Replace the default configuration with the following optimized build specification:

```yml
version: 1
backend:
  phases:
    preBuild:
      commands:
        - npm install
    build:
      commands:
        - nvm use 20
        - npm ci --cache .npm --prefer-offline
        - npx ampx pipeline-deploy --branch $AWS_BRANCH --app-id $AWS_APP_ID
frontend:
  phases:
    build:
      commands:
        - npm run build
  artifacts:
    baseDirectory: dist
    files:
      - '**/*'
  cache:
    paths:
      - node_modules/**/*
```

![YML Configuration](/images/4/4-5.png?featherlight=false&width=90pc)

{{% notice warning %}}
Ensure proper indentation in the YAML file. Incorrect indentation will cause build failures.
{{% /notice %}}

#### Save Configuration

1. After editing the amplify.yml file, click **Save**.
2. Review the build settings to ensure they match your requirements.

![Save Configuration](/images/4/4-6.png?featherlight=false&width=90pc)

#### Configure Environment Variables (Optional)

1. If your application requires environment variables, add them in the **Environment variables** section.
2. Set any necessary build-time or runtime environment variables.

#### Result

Your build configuration is now set up with the proper commands for Vite React application deployment.