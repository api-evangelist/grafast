# Grafast GraphQL Execution Engine

Grafast is a next-generation planning and execution engine for GraphQL servers from the Graphile team, designed as a replacement for the graphql-js execution layer. Rather than resolving fields individually, Grafast uses a planning phase to build a dependency graph of "steps" that can be executed optimally — eliminating N+1 queries and enabling efficient batching across the entire operation.

The primary integration is PostGraphile v5 (also called PostGraphile Next), which uses Grafast to generate a full-featured GraphQL API from a PostgreSQL database schema automatically. The resulting GraphQL API includes CRUD operations, filtering, pagination via Relay cursor connections, ordering, mutations, and subscriptions.

**Endpoint:** Self-hosted; generated endpoint from PostGraphile (typically https://localhost:5000/graphql or via Grafserv)

**Documentation:** https://grafast.org and https://postgraphile.org

## GraphQL Schema

The SDL schema is available at [grafast-schema.graphql](grafast-schema.graphql). It documents:

- **Scalars**: `Cursor`, `BigInt`, `BigFloat`, `UUID`, `JSON`, `Datetime`, `Date`, `Time`, `InternetAddress`
- **Node interface**: Relay global object identification (`id: ID!`)
- **PageInfo**: `hasNextPage`, `hasPreviousPage`, `startCursor`, `endCursor`
- **Connection/edge pattern**: `UsersConnection`, `UsersEdge`, `PostsConnection`, `PostsEdge`
- **Condition/filter inputs**: `UserCondition`, `PostCondition`
- **Ordering enums**: `UsersOrderBy`, `PostsOrderBy`
- **CRUD mutations**: `createUser`, `updateUserById`, `deleteUserById` and equivalent Post mutations, each with typed input/payload objects
- **Subscription**: `listen(topic: String!): ListenPayload` via PostgreSQL NOTIFY

## Key Concepts

- **Plan Resolvers**: Functions attached to schema fields that describe how to fetch data, rather than fetching it directly.
- **Operation Plan**: A directed acyclic graph (DAG) of steps derived from all plan resolvers in a given request.
- **Steps**: Atomic units of work (e.g., a database query, a remote API call) that are deduplicated and batched automatically. Core steps include `AccessStep`, `ConnectionStep`, `EdgeStep`, `ConstantStep`, `LambdaStep`, `ListStep`, `ObjectStep`, `LoadOneStep`, `LoadManyStep`, `SideEffectStep`, and `ListenStep`.
- **Execution Phase**: After planning, Grafast executes the operation plan efficiently, running batched steps in parallel where possible.

## Step Classes (grafast package)

Exported from `grafast/src/steps/`:

| Step | Purpose |
|---|---|
| `AccessStep` | Access a property of another step's result |
| `ConnectionStep` / `EdgeStep` | Relay-style cursor pagination |
| `ConstantStep` | Return a compile-time constant value |
| `LambdaStep` | Apply a synchronous transform to step values |
| `ListStep` | Combine multiple steps into an array |
| `ObjectStep` | Combine named steps into a plain object |
| `LoadOneStep` / `LoadManyStep` | Batched data loading (DataLoader pattern) |
| `SideEffectStep` | Mutations / writes with side effects |
| `ListenStep` | Real-time subscriptions via async iterables |
| `CoalesceStep` | Return the first non-null value from multiple steps |
| `ConditionStep` | Conditional branching in the plan graph |
| `RemapKeysStep` | Transform object keys |
| `ReverseStep` | Reverse a list step |

## Drop-in Replacement

Grafast can be used as a drop-in replacement for `graphql-js`'s `execute` method:

```js
import { grafast } from "grafast";

const result = await grafast({
  schema,
  document,
  variableValues,
});
```

## Schema Definition (makeGrafastSchema)

```ts
import { makeGrafastSchema, lambda } from "grafast";

const schema = makeGrafastSchema({
  typeDefs: /* GraphQL */ `
    type Query {
      addTwoNumbers(a: Int!, b: Int!): Int
    }
  `,
  objects: {
    Query: {
      plans: {
        addTwoNumbers(_, fieldArgs) {
          const { $a, $b } = fieldArgs;
          return lambda([$a, $b], ([a, b]) => a + b);
        },
      },
    },
  },
});
```

## Integration

Grafast integrates with:
- **PostGraphile v5**: Automatic plan generation from PostgreSQL schema introspection.
- **Grafserv**: A high-performance GraphQL HTTP server built for Grafast.
- **Ruru**: A GraphiQL-based IDE with Grafast-aware features.

## References

- Documentation: https://grafast.org
- GettingStarted: https://postgraphile.org/postgraphile/next/migrating-from-v4
- GitHub: https://github.com/graphile/crystal

## NPM Package

```
npm install grafast
```

Package: https://www.npmjs.com/package/grafast  
License: MIT  
Weekly Downloads: ~22,000+
