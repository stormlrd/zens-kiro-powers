# Amplify GraphQL Patterns

## Schema Design

### Basic Model
```graphql
type Todo @model @auth(rules: [{ allow: owner }]) {
  id: ID!
  name: String!
  description: String
  completed: Boolean!
  owner: String
}
```

### Relationships

#### One-to-Many
```graphql
type Blog @model {
  id: ID!
  name: String!
  posts: [Post] @hasMany
}

type Post @model {
  id: ID!
  title: String!
  blog: Blog @belongsTo
}
```

#### Many-to-Many
```graphql
type Post @model {
  id: ID!
  title: String!
  tags: [Tag] @manyToMany(relationName: "PostTags")
}

type Tag @model {
  id: ID!
  label: String!
  posts: [Post] @manyToMany(relationName: "PostTags")
}
```

## Authorization Rules

### Owner-Based
```graphql
type Note @model @auth(rules: [
  { allow: owner }
]) {
  id: ID!
  content: String!
}
```

### Group-Based
```graphql
type Document @model @auth(rules: [
  { allow: groups, groups: ["Admins"] }
  { allow: groups, groups: ["Editors"], operations: [read, update] }
]) {
  id: ID!
  title: String!
}
```

### Public/Private
```graphql
type Post @model @auth(rules: [
  { allow: public, operations: [read] }
  { allow: private, operations: [create, update, delete] }
]) {
  id: ID!
  title: String!
}
```

### Field-Level Auth
```graphql
type User @model {
  id: ID!
  username: String!
  email: String @auth(rules: [{ allow: owner }])
  ssn: String @auth(rules: [{ allow: owner }])
}
```

## Custom Resolvers

### Lambda Function
```graphql
type Query {
  getCustomData(id: ID!): CustomData @function(name: "getCustomData")
}
```

### HTTP Resolver
```graphql
type Query {
  getExternalData: ExternalData @http(url: "https://api.example.com/data")
}
```

## Subscriptions

### Real-Time Updates
```graphql
type Subscription {
  onCreateTodo: Todo @aws_subscribe(mutations: ["createTodo"])
  onUpdateTodo: Todo @aws_subscribe(mutations: ["updateTodo"])
  onDeleteTodo: Todo @aws_subscribe(mutations: ["deleteTodo"])
}
```

### Filtered Subscriptions
```graphql
type Subscription {
  onCreateTodoByOwner(owner: String!): Todo
    @aws_subscribe(mutations: ["createTodo"])
}
```

## Query Patterns

### Pagination
```javascript
const result = await API.graphql({
  query: listTodos,
  variables: {
    limit: 20,
    nextToken: previousResult.data.listTodos.nextToken
  }
});
```

### Filtering
```javascript
const result = await API.graphql({
  query: listTodos,
  variables: {
    filter: {
      completed: { eq: false },
      name: { contains: 'important' }
    }
  }
});
```

### Sorting
```javascript
const result = await API.graphql({
  query: listTodos,
  variables: {
    sortDirection: 'DESC'
  }
});
```

## DataStore Patterns

### Sync with Cloud
```javascript
import { DataStore } from '@aws-amplify/datastore';
import { Todo } from './models';

// Create
await DataStore.save(
  new Todo({
    name: 'My first todo',
    completed: false
  })
);

// Query
const todos = await DataStore.query(Todo);

// Update
await DataStore.save(
  Todo.copyOf(original, updated => {
    updated.completed = true;
  })
);

// Delete
await DataStore.delete(todo);

// Observe changes
DataStore.observe(Todo).subscribe(msg => {
  console.log(msg.model, msg.opType, msg.element);
});
```

### Selective Sync
```javascript
DataStore.configure({
  syncExpressions: [
    syncExpression(Todo, t => t.completed('eq', false))
  ]
});
```

## Best Practices

### Schema Design
- Use meaningful type names
- Add descriptions to fields
- Use enums for fixed values
- Implement proper relationships
- Add indexes for queries

### Authorization
- Start with least privilege
- Use owner-based auth for user data
- Implement group-based for teams
- Use field-level auth for sensitive data
- Test all auth rules

### Performance
- Use pagination for large lists
- Implement caching strategies
- Use DataStore for offline
- Optimize query depth
- Monitor AppSync metrics

### Error Handling
- Implement retry logic
- Handle network failures
- Validate inputs
- Log errors appropriately
- Provide user feedback
