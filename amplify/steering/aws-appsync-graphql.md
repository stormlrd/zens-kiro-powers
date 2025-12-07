---
inclusion: always
---

# AWS AppSync GraphQL Standards

This project uses AWS AppSync with Amplify Gen 2. Follow these patterns to prevent runtime errors.

## Critical Rules

### 1. Custom Type Naming (CRITICAL)
Amplify Gen 2 automatically appends "Input" to custom types used in mutation arguments.

**Rule:** NEVER name custom types with "Input" suffix.

```typescript
// ❌ WRONG - Becomes UpdateBrandingConfigInputInput
UpdateBrandingConfigInput: a.customType({ ... })

// ✅ CORRECT - Becomes UpdateBrandingConfigInput
UpdateBrandingConfig: a.customType({ ... })
```

**Error symptoms:** `Unknown type XyzInput` or `Variable type 'XyzInput!' doesn't match expected type 'XyzInputInput'`

### 2. DateTime Fields
AppSync requires full ISO 8601 format: `"2024-12-03T14:30:00.000Z"`

**Always convert to ISO 8601:**
```typescript
// ❌ WRONG - datetime-local (no timezone)
startDate: "2024-12-03T14:30"

// ✅ CORRECT - Use .toISOString()
const startDate = new Date(formData.startDate).toISOString();
```

Schema: `a.datetime().required()` | Zod: `z.string().datetime()`

### 3. URL Fields
URLs must include protocol (http:// or https://).

```typescript
// ❌ WRONG
repositoryLink: "github.com/user/repo"

// ✅ CORRECT - Add protocol if missing
if (!url.startsWith('http://') && !url.startsWith('https://')) {
  url = 'https://' + url;
}
new URL(url); // Validate
```

Schema: `a.url()` | Zod: `z.string().url().optional()`

### 4. Enum Fields
Enum values are case-sensitive and must match schema exactly.

```typescript
// Define as TypeScript types
export type ChallengeStatus = 'upcoming' | 'active' | 'completed';

// Validate before sending
if (!validStatuses.includes(status)) {
  throw new Error(`Invalid status: ${status}`);
}
```

Schema: `a.enum(['upcoming', 'active', 'completed'])`

## GraphQL Response Handling

### Required Type Guard Pattern
**ALWAYS use type guards for GraphQL responses:**

```typescript
const result = await client.graphql({ query, variables });

// Check for errors first
if ('errors' in result && result.errors) {
  throw new Error(`GraphQL errors: ${result.errors.map(e => e.message).join(', ')}`);
}

// Then extract data
if ('data' in result && result.data) {
  return result.data.myQuery;
}

throw new Error('Unexpected response format');
```

### Common Error Types
- **MalformedHttpRequestException**: Invalid data format (datetime, URL) - validate before sending
- **Unauthorized**: User not in required Cognito group - check authorization
- **ValidationError**: Data doesn't match schema constraints - add frontend validation
- **ConflictException**: Duplicate key violation - check for existing records

## Schema Patterns

### Custom Mutations
```typescript
// amplify/data/resource.ts - Note: NO "Input" suffix on custom type
createChallenge: a
  .mutation()
  .arguments({ input: a.ref('CreateChallenge') })  // Amplify adds "Input"
  .returns(a.ref('Challenge'))
  .authorization((allow) => [allow.group('Admins')])
  .handler(a.handler.function(createChallenge))
```

### Lambda Handler Structure
```typescript
export const handler = async (event: CreateChallengeEvent) => {
  // 1. Verify authorization
  const groups = event.identity.groups || [];
  if (!groups.includes('Admins')) {
    throw new Error('Unauthorized: Admin access required');
  }
  
  // 2. Validate with Zod
  const validationResult = schema.safeParse(event.arguments.input);
  if (!validationResult.success) {
    throw new Error(`Validation failed: ${validationResult.error.message}`);
  }
  
  // 3. Process and return data matching GraphQL schema
  return await processChallenge(validationResult.data);
};
```

### Authorization Patterns
```typescript
// Schema authorization
.authorization((allow) => [allow.group('Admins')])
.authorization((allow) => [allow.authenticated()])
.authorization((allow) => [allow.owner()])

// Frontend authorization check
import { fetchAuthSession } from 'aws-amplify/auth';

const session = await fetchAuthSession();
const groups = session.tokens?.idToken?.payload['cognito:groups'] as string[] | undefined;
const isAdmin = groups?.includes('Admins') ?? false;
```

## Best Practices

### Pagination
```typescript
async function listAllItems() {
  const items = [];
  let nextToken = null;
  
  do {
    const result = await client.graphql({
      query: listQuery,
      variables: { limit: 100, nextToken }
    });
    
    if ('data' in result && result.data) {
      items.push(...result.data.listItems.items);
      nextToken = result.data.listItems.nextToken;
    }
  } while (nextToken);
  
  return items;
}
```

### Optimistic Updates
```typescript
// Update UI immediately, rollback on error
const optimisticItem = { ...item, voteCount: item.voteCount + 1 };
setItems(items.map(i => i.id === item.id ? optimisticItem : i));

try {
  await client.graphql({ query: createVote, variables: { input } });
} catch (error) {
  setItems(items); // Rollback
  throw error;
}
```

### Batch Operations
```typescript
// Execute multiple queries in parallel
const [users, submissions, challenges] = await Promise.all([
  client.graphql({ query: listUsers }),
  client.graphql({ query: listSubmissions }),
  client.graphql({ query: listChallenges })
]);
```

### Selective Fields
```typescript
// Only request fields you need
const query = `
  query ListChallenges {
    listChallenges {
      items {
        id
        title
        status
      }
    }
  }
`;
```

## Debugging Checklist

When GraphQL operations fail:
1. Check error type: `MalformedHttpRequestException` = invalid data format (datetime/URL)
2. Verify datetime fields use `.toISOString()`
3. Verify URLs include protocol (https://)
4. Check user authorization groups
5. Validate enum values match schema exactly
6. Check Lambda CloudWatch logs: `aws logs tail /aws/lambda/[function-name] --follow`
7. Verify `amplify_outputs.json` has real values (not PLACEHOLDER)

## Quick Reference

### Data Validation Checklist
Before sending GraphQL mutations:
- [ ] DateTime fields converted with `.toISOString()`
- [ ] URLs include protocol (https://)
- [ ] Enum values match schema exactly (case-sensitive)
- [ ] Custom types don't have "Input" suffix
- [ ] Type guards used for all responses

### Common Patterns
```typescript
// DateTime conversion
const startDate = new Date(formData.startDate).toISOString();

// URL normalization
if (!url.startsWith('http://') && !url.startsWith('https://')) {
  url = 'https://' + url;
}

// Type guard (REQUIRED)
if ('errors' in result && result.errors) {
  throw new Error(`GraphQL errors: ${result.errors.map(e => e.message).join(', ')}`);
}
if ('data' in result && result.data) {
  return result.data.myQuery;
}

// Authorization check
const session = await fetchAuthSession();
const isAdmin = session.tokens?.idToken?.payload['cognito:groups']?.includes('Admins') ?? false;
```
