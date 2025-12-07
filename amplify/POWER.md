---
name: "amplify"
displayName: "AWS Amplify"
description: "AWS Amplify for full-stack application development - build and deploy web and mobile applications with authentication, APIs, storage, and hosting"
keywords: ["amplify", "fullstack", "frontend", "backend", "hosting", "authentication", "graphql", "appsync"]
author: "Zen"
repository: "https://github.com/stormlrd/zens-kiro-powers"
---

# AWS Amplify Power

## Overview

AWS Amplify provides a complete solution for building full-stack web and mobile applications with built-in authentication, APIs, storage, and hosting capabilities.

**Key capabilities:**
- **Authentication**: User sign-up, sign-in, and access control with Cognito
- **APIs**: GraphQL and REST APIs with AppSync and API Gateway
- **Storage**: File storage with S3 integration
- **Hosting**: Static web hosting with CI/CD
- **DataStore**: Offline-first data synchronization
- **Functions**: Serverless Lambda functions

## Available MCP Servers

### appsync
**Package:** `awslabs.aws-appsync-mcp-server@latest`
**Purpose:** Manage GraphQL APIs with AppSync for Amplify applications
**Authentication:** AWS IAM credentials

### serverless
**Package:** `awslabs.aws-serverless-mcp-server@latest`
**Purpose:** Deploy and manage serverless functions for Amplify backends
**Authentication:** AWS IAM credentials

## Architecture Patterns

### Full-Stack Application
```
Frontend (React/Vue/Angular)
    ↓
Amplify Hosting
    ↓
AppSync GraphQL API
    ↓
Lambda Resolvers → DynamoDB
    ↓
Cognito Authentication
```

### Mobile Application
```
Mobile App (iOS/Android)
    ↓
Amplify Libraries
    ↓
AppSync + DataStore (Offline)
    ↓
S3 Storage + Lambda Functions
```

## Best Practices

### ✅ Do:

- **Use Amplify CLI** - Initialize and configure projects with `amplify init`
- **Environment separation** - Use separate environments for dev/staging/prod
- **GraphQL schema first** - Design schema before implementation
- **Use DataStore** - For offline-first mobile apps
- **Implement auth** - Use Amplify Auth for user management
- **Optimize hosting** - Enable caching and CDN
- **Monitor usage** - Track API calls and storage

### ❌ Don't:

- **Don't hardcode endpoints** - Use Amplify configuration
- **Don't skip authentication** - Secure all APIs
- **Don't ignore offline** - Handle network failures
- **Don't over-fetch** - Use GraphQL queries efficiently
- **Don't skip testing** - Test auth flows and APIs
- **Don't ignore costs** - Monitor AppSync and storage usage

## Configuration

**Authentication Required**: AWS IAM credentials

**Environment Variables:**
- `AWS_PROFILE` - AWS CLI profile name
- `AWS_REGION` - AWS region (e.g., us-east-1)
- `FASTMCP_LOG_LEVEL` - Logging level

**Setup Steps:**
1. Install Amplify CLI: `npm install -g @aws-amplify/cli`
2. Configure Amplify: `amplify configure`
3. Initialize project: `amplify init`
4. Add features: `amplify add auth`, `amplify add api`, etc.
5. Deploy: `amplify push`

## Common Use Cases

### Authentication Flow
```javascript
// Sign up
await Auth.signUp({
  username: email,
  password: password,
  attributes: { email }
});

// Sign in
await Auth.signIn(email, password);

// Get current user
const user = await Auth.currentAuthenticatedUser();
```

### GraphQL API
```javascript
// Query
const result = await API.graphql({
  query: listTodos,
  variables: { limit: 10 }
});

// Mutation
await API.graphql({
  query: createTodo,
  variables: { input: { name: 'New Todo' } }
});

// Subscription
API.graphql({ query: onCreateTodo })
  .subscribe({
    next: (data) => console.log(data)
  });
```

### Storage
```javascript
// Upload file
await Storage.put('photo.jpg', file, {
  contentType: 'image/jpeg'
});

// Download file
const url = await Storage.get('photo.jpg');

// List files
const files = await Storage.list('photos/');
```

## Tips

1. **Start with templates** - Use Amplify Studio for visual development
2. **Use DataStore** - For complex offline requirements
3. **Optimize queries** - Use GraphQL fragments and pagination
4. **Implement caching** - Reduce API calls with client-side caching
5. **Monitor performance** - Use CloudWatch and X-Ray
6. **Version APIs** - Use AppSync schema versioning
7. **Test locally** - Use Amplify mock for local development
8. **Secure APIs** - Implement proper authorization rules

---

**Source:** AWS Labs
**License:** Apache-2.0
