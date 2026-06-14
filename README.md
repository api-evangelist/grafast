# Grafast

Next-generation PostgreSQL-backed GraphQL planning and execution engine from the Graphile project, replacing graphql-js execution with a plan-based approach to eliminate N+1 queries.

## Overview

Grafast is a ludicrously speedy, general-purpose, and holistic advanced planning and execution engine for GraphQL. It serves as a drop-in replacement for the `execute` method from `graphql-js`, using "plan resolvers" instead of traditional field resolvers to orchestrate data fetching efficiently.

- **Website**: https://grafast.org/
- **Documentation**: https://grafast.org/grafast/
- **GitHub**: https://github.com/grafast (org) / https://github.com/graphile/crystal (monorepo)
- **npm**: https://www.npmjs.com/package/grafast
- **Blog**: https://grafast.org/news/
- **LinkedIn**: https://uk.linkedin.com/company/graphile
- **Sponsorship**: https://grafast.org/support/

## How It Works

1. **Planning Phase**: Grafast analyzes the incoming GraphQL operation and builds an optimized execution plan — a DAG of steps derived from all plan resolvers in the schema.
2. **Execution Phase**: The plan is executed with automatic batching and deduplication of steps, dramatically reducing the number of database queries and remote calls.

## Repository Contents

```
apis.yml                        # APIs.json 0.19 catalog entry
graphql/grafast-graphql.md      # GraphQL API documentation
plans/grafast-plans.md          # Sponsorship and support plans
rate-limits/grafast-rate-limits.md  # Rate limiting guidance
finops/grafast-finops.md        # FinOps and cost analysis
```

## License

Grafast is MIT licensed and free to use. See https://grafast.org/support/ for optional sponsorship tiers that sustain ongoing development.

## Maintainer

Kin Lane — kin@apievangelist.com
