---
inclusion: always
---

# AWS Amplify Gen 2 Deployment Standards

## Architecture Overview
AWS Amplify Gen 2 backend with 16+ Lambda functions, DynamoDB tables, and AppSync GraphQL API. This project has strict requirements to prevent CloudFormation circular dependencies and deployment failures.

## Critical Rules for AI Assistants

### ALWAYS Validate Before Suggesting Changes
When modifying backend code, you MUST:
1. Run `getDiagnostics` on modified TypeScript files
2. Verify no circular dependencies will be introduced
3. Ensure Lambda functions are properly registered in `amplify/backend.ts`
4. Check that environment variables and permissions are configured

### Pre-Deployment Validation Commands
```bash
npx tsc --noEmit                                    # Frontend TypeScript
npx tsc --noEmit --project amplify/tsconfig.json   # Backend TypeScript
npm run build                                       # Production build
node scripts/check-circular-dependencies.js         # Circular dependency check
```

## Three Critical Deployment Blockers

### 1. TypeScript Compilation Errors
**Rule:** All TypeScript must compile without errors before deployment.

**Common Issues:**
- Missing type guards for GraphQL results (use `if ('data' in result && result.data)`)
- Unused imports in files
- Incorrect type assertions

**Action:** Use `getDiagnostics` tool after modifying any `.ts` or `.tsx` file.

### 2. Missing Lambda Function Registration
**Rule:** Every Lambda function MUST be registered in `amplify/backend.ts`.

**Required Steps When Creating a Lambda:**
1. Create `amplify/functions/[name]/handler.ts` and `resource.ts`
2. Import in `amplify/backend.ts`: `import { myFunction } from './functions/my-function/resource';`
3. Add to `defineBackend({ ..., myFunction })`
4. Grant DynamoDB access: `table.grantReadWriteData(backend.myFunction.resources.lambda)`
5. Add environment variables: `backend.myFunction.addEnvironment('VAR_NAME', value)`
6. Grant invocation permissions if needed: `backend.targetFunction.resources.lambda.grantInvoke(backend.callerFunction.resources.lambda)`

### 3. Circular CloudFormation Dependencies
**Rule:** Lambda invocation hierarchy MUST be unidirectional (no cycles).

**Architecture Pattern:**
```
Level 1 (Leaf):     createNotification, evaluateBadges
Level 2:            calculatePoints, updateStreak
Level 3 (Entry):    createSubmission, createVote, createPeerReview, etc.
```

**Special Case - Auth Triggers:**
Auth triggers (e.g., `postConfirmation`) MUST use IAM policies with wildcards, NOT direct table grants:
```typescript
// ❌ WRONG - Creates circular dependency
tables['User'].grantReadWriteData(backend.postConfirmation.resources.lambda);

// ✅ CORRECT - Use IAM policy
backend.postConfirmation.resources.lambda.addToRolePolicy(
  new PolicyStatement({
    actions: ['dynamodb:PutItem', 'dynamodb:GetItem', 'dynamodb:UpdateItem'],
    resources: [`arn:aws:dynamodb:*:*:table/*User*`],
  })
);
```

**Action:** Run `node scripts/check-circular-dependencies.js` before suggesting Lambda changes.

## Lambda Configuration Patterns

### Environment Variables
Functions that invoke other Lambdas:
```typescript
backend.functionName.addEnvironment(
  'TARGET_FUNCTION_NAME',
  backend.targetFunction.resources.lambda.functionName
);
```

Functions that access DynamoDB:
```typescript
backend.functionName.addEnvironment(
  'TABLE_NAME',
  backend.data.resources.tables['TableName'].tableName
);
```

### Permission Grants
Invocation permissions (caller → target):
```typescript
backend.targetFunction.resources.lambda.grantInvoke(backend.callerFunction.resources.lambda);
```

DynamoDB access (all functions except auth triggers):
```typescript
Object.values(tables).forEach((table) => {
  table.grantReadWriteData(backend.functionName.resources.lambda);
});
```

## Code Standards for AI Assistants

### TypeScript Requirements
- No `any` types without justification
- Always use type guards for GraphQL: `if ('data' in result && result.data)`
- Remove unused imports and variables
- Prefer `@ts-expect-error` over `@ts-ignore`

### Lambda Handler Requirements
- Validate input with Zod schemas
- Check environment variables at handler start
- Wrap external calls in try-catch
- Return descriptive error messages

### GraphQL Result Handling Pattern
```typescript
const result = await client.graphql({ query, variables });

if ('errors' in result && result.errors) {
  throw new Error(`GraphQL errors: ${result.errors.map(e => e.message).join(', ')}`);
}

if ('data' in result && result.data) {
  return result.data.myQuery;
}

throw new Error('Unexpected response format');
```

## Build Process
Amplify runs: `npm ci` → `npx ampx pipeline-deploy` → `npm run build` (which is `tsc && vite build`)

**Critical:** Build script MUST run TypeScript compilation before Vite build.

## Complete Lambda Function Creation Checklist

When creating a new Lambda function, follow this exact sequence:

1. **Create function files:**
   - `amplify/functions/[name]/handler.ts`
   - `amplify/functions/[name]/resource.ts`

2. **Register in `amplify/backend.ts`:**
   ```typescript
   import { myFunction } from './functions/my-function/resource';
   
   const backend = defineBackend({
     // ... existing functions
     myFunction,
   });
   ```

3. **Grant DynamoDB permissions (unless auth trigger):**
   ```typescript
   Object.values(tables).forEach((table) => {
     table.grantReadWriteData(backend.myFunction.resources.lambda);
   });
   ```

4. **Add environment variables:**
   ```typescript
   backend.myFunction.addEnvironment('TABLE_NAME', backend.data.resources.tables['MyTable'].tableName);
   ```

5. **Grant invocation permissions (if calling other Lambdas):**
   ```typescript
   backend.targetFunction.resources.lambda.grantInvoke(backend.myFunction.resources.lambda);
   ```

6. **Verify no circular dependencies:**
   ```bash
   node scripts/check-circular-dependencies.js
   ```

## Validation Checklist for AI Assistants

Before suggesting code changes:
- [ ] Run `getDiagnostics` on modified TypeScript files
- [ ] Verify GraphQL results use type guards
- [ ] Check Lambda functions are registered in `amplify/backend.ts`
- [ ] Confirm no circular dependencies introduced
- [ ] Ensure environment variables are configured
- [ ] Verify IAM permissions are granted

## Available Tools
- `scripts/check-circular-dependencies.js` - Detect circular Lambda dependencies
- `scripts/pre-deploy-check.bat` / `.sh` - Full pre-deployment validation
- `getDiagnostics` - Check TypeScript compilation errors

## Key Principle
**Validate locally what AWS will validate remotely.** Catch deployment blockers before pushing to AWS.
