---
title : "Install Dependencies and Setup Frontend"
date : "2023-12-01T00:00:00Z"
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

#### Install Required Dependencies

To integrate AWS Amplify with your React application, you need to install the necessary libraries and UI components.

#### Navigate to Project Directory

1. Open a terminal in your `leftover` project directory.
2. Ensure you're in the root folder where `package.json` is located.

#### Install Amplify Libraries

Execute the following command to install AWS Amplify dependencies:

```bash
npm install aws-amplify @aws-amplify/ui-react
```

![Install Dependencies](/images/5/5-1.png?featherlight=false&width=90pc)

This command installs:
- `aws-amplify`: Core Amplify library for AWS service integration
- `@aws-amplify/ui-react`: Pre-built React UI components for authentication and other features

#### Configure Base Styling

Update the `src/index.css` file with improved styling:

```css
:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color: rgba(255, 255, 255, 0.87);

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
}

.card {
  padding: 2em;
}

.read-the-docs {
  color: #888;
}

.box:nth-child(3n + 1) {
  grid-column: 1;
}
.box:nth-child(3n + 2) {
  grid-column: 2;
}
.box:nth-child(3n + 3) {
  grid-column: 3;
}
```

#### Setup Application Styling

Update the `src/App.css` file with component-specific styles:

```css
.app-container {
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

.header-container {
  padding-bottom: 2.5rem;
  margin: auto;
  text-align: center;
  max-width: 48rem;
}

.main-header {
  font-size: 2.25rem;
  font-weight: bold;
  color: #1a202c;
}

.main-header .highlight {
  color: #2563eb;
}

@media (min-width: 640px) {
  .main-header {
    font-size: 3.75rem;
  }
}

.description {
  font-weight: 500;
  font-size: 1.125rem;
  max-width: 65ch;
  color: #1a202c;
}
```

{{% notice info %}}
These styles provide a clean, responsive design foundation for your application with proper typography and layout structure.
{{% /notice %}}

#### Result

Your project now has the necessary Amplify dependencies installed and basic styling configured for the frontend interface.