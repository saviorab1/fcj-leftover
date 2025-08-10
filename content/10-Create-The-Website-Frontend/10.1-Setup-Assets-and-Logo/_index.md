---
title : "Setup Assets and Logo"
date : "2025-08-10T20:24:00Z"
weight : 1
chapter : false
pre : " <b> 10.1 </b> "
---

#### Create Project Assets Structure

Organize your project files by creating a proper folder structure for images and other assets.

#### Create Assets Directory

1. Navigate to the `src/` folder in your project.
2. Create a new folder named `assets`.
3. Inside the `assets` folder, create another folder named `pics`.

The folder structure should look like:
```
src/
├── assets/
│   └── pics/
│       └── logo.png (to be added)
├── App.tsx
├── App.css
└── index.css
```

#### Add Custom Logo

For this project, we've created a custom logo for aesthetic purposes and branding.

![Custom Logo](/images/10/10-1.png?featherlight=false&width=90pc)

#### Download and Place Logo

1. Download the provided `logo.png` file from: [Download Logo](https://drive.google.com/file/d/1kgE_m9j1gMrEBotkg9uBTJ8R8RYin6Cj/view?usp=sharing)
2. Place the `logo.png` file inside the `src/assets/pics/` directory.
3. Ensure the file is named exactly `logo.png` for proper import.

{{% notice info %}}
You can use your own custom logo by replacing the provided logo.png file, or remove the logo entirely by modifying the App.tsx component in the next step.
{{% /notice %}}

#### Verify File Structure

After adding the logo, your project structure should include:
- `src/assets/pics/logo.png`
- Proper folder hierarchy for organized asset management
- Easy access for importing in React components

![Custom Logo](/images/10/10-2.png?featherlight=false&width=90pc)

#### Logo Specifications

The logo should ideally be:
- **Format**: PNG with transparent background
- **Size**: Approximately 150x150 pixels or similar square dimensions
- **Style**: Clean and simple design that works well with the application theme

#### Result

Your project now has a proper assets structure with a custom logo ready for integration into the main application component.
