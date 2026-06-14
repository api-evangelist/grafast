# Grafast GraphQL

Grafast is a next-generation planning and execution engine for GraphQL, developed by the Graphile project. It replaces the standard `execute` function from `graphql-js` with a plan-based approach that eliminates N+1 query problems and dramatically improves performance.

## Overview

Rather than using traditional field resolvers, Grafast introduces "plan resolvers" that describe the abstract steps required to resolve a field. These steps are combined across all fields in a request into a single operation plan, which is then executed in an optimized and batched manner.

## Key Concepts

- **Plan Resolvers**: Functions attached to schema fields that describe how to fetch data, rather than fetching it directly.
- **Operation Plan**: A directed acyclic graph (DAG) of steps derived from all plan resolvers in a given request.
- **Steps**: Atomic units of work (e.g., a database query, a remote API call) that are deduplicated and batched automatically.
- **Execution Phase**: After planning, Grafast executes the operation plan efficiently, running batched steps in parallel where possible.

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

## Integration

Grafast integrates with:
- **PostGraphile v5**: Automatic plan generation from PostgreSQL schema introspection.
- **Grafserv**: A high-performance GraphQL HTTP server built for Grafast.
- **Ruru**: A GraphiQL-based IDE with Grafast-aware features.

## Documentation

- Getting Started: https://grafast.org/grafast/getting-started/
- Plan Resolvers: https://grafast.org/grafast/plan-resolvers/
- Servers: https://grafast.org/grafast/servers/
- Production Considerations: https://github.com/graphile/crystal/blob/main/grafast/website/grafast/production-considerations.md

## NPM Package

```
npm install grafast
```

Package: https://www.npmjs.com/package/grafast  
License: MIT  
Weekly Downloads: ~22,000+
