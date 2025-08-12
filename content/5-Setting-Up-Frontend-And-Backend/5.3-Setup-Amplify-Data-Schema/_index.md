---
title : "Setup Amplify Data Schema"
date : "2025-08-10T20:24:00Z"
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

#### Configure Data Layer

Set up the Amplify Data resource to define your application's data schema and API configuration.

#### Create Data Resource File

1. Navigate to the `amplify/data/` directory in your project.
2. Create a new file named `resource.ts`.
3. This file will define your data schema and authorization settings.

#### Implement Data Schema

Add the following code to `amplify/data/resource.ts`:

```tsx
import { type ClientSchema, a, defineData } from "@aws-amplify/backend";

const schema = a.schema({
  Todo: a
    .model({
      content: a.string(),
      done: a.boolean().default(false),
    })
    .authorization((allow) => [allow.owner()]),
});

export type Schema = ClientSchema<typeof schema>;

export const data = defineData({
  schema,
  authorizationModes: {
    defaultAuthorizationMode: "apiKey",
    apiKeyAuthorizationMode: {
      expiresInDays: 30,
    },
  },
});
```

#### Schema Configuration Details

**Schema Definition**:
- `Todo` model with `content` (string) and `done` (boolean) fields
- `done` field defaults to `false` for new todos
- Owner-based authorization ensures users can only access their own data

**Authorization Configuration**:
- `defaultAuthorizationMode: "apiKey"`: Uses API key for data access
- `expiresInDays: 30`: API key remains valid for 30 days
- Provides secure but convenient access to data operations

#### Wire Up Backend Resources

Update the backend entry to include both `auth` and `data` resources.

1. Open `amplify/backend.ts`.
2. Replace its contents with:

```ts
import { defineBackend } from "@aws-amplify/backend";
import { data } from "./data/resource";
import { auth } from "./auth/resource";

const backend = defineBackend({
  auth,
  data,
});
```

#### Data Layer Benefits

This configuration provides:
- **Type Safety**: Full TypeScript support for data operations
- **Automatic API Generation**: GraphQL API created automatically
- **Real-time Updates**: Built-in subscription support for live data
- **Offline Support**: Local data caching and sync capabilities

#### Todo Model Features

The Todo model provides:
- **Content Field**: Stores the todo item text
- **Done Field**: Tracks completion status with default false value
- **Owner Authorization**: Each user can only access their own todos
- **Automatic Timestamps**: Created and updated timestamps added automatically

{{% notice tip %}}
The owner authorization ensures data privacy by restricting access to the authenticated user who created each todo item.
{{% /notice %}}

#### Deploy Data Changes

After creating the resource file:
1. Commit your changes to Git
2. Push to GitHub to trigger automatic deployment
3. Amplify will provision the necessary AWS resources (AppSync, DynamoDB)

#### Result

Your application now has a complete data layer configured with:
- Properly structured data schema foundation
- API key-based authorization for secure access
- Type-safe data operations for frontend integration
- Scalable backend infrastructure ready for future enhancements

{{% notice note %}}
The data schema will be automatically deployed with your next Amplify build, creating the necessary AWS AppSync API and DynamoDB tables.
{{% /notice %}}
