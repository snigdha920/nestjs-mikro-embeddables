This repository demonstrates a limitation with the `@UseRequestContext` decorator from Mikro ORM, when used with NestJS `@ResolveFields` (from `@nestjs/graphql`).

### The problem:
- When a `@ResolveField` is queried over a subscription, it uses a global entity manager
- A run time error is thrown

### Steps to reproduce:
1. Clone the repo and cd over to the root 
2. Run `pnpm start`
3. Access the GraphQL playground at http://localhost:3000/graphql
3. Execute the following subscription in one tab:

```
subscription authorAdded {
  authorAdded {
    computedField
  }
}
```

4. Watch the API logs
5. Execute the following mutation (while keeping the subscription running in one tab):
```
mutation createAuthor {
  createAuthor {
    _id
  }
}

```
