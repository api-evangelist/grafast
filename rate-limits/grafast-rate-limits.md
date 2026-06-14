# Grafast Rate Limits

Grafast is a self-hosted, open-source library and does not impose any rate limits at the library level. Rate limiting behavior is entirely determined by the host application and infrastructure.

## Library-Level Limits

**None.** Grafast itself does not:
- Impose request-per-second limits
- Enforce query complexity limits by default
- Restrict concurrent executions
- Apply throttling to plan resolution

## Application-Level Considerations

When deploying Grafast in production, operators are responsible for implementing appropriate controls:

### Query Complexity
Grafast generates an operation plan before execution. You can inspect the plan to apply custom complexity limits before allowing execution to proceed.

### Depth Limiting
Standard GraphQL depth-limiting middleware (e.g., `graphql-depth-limit`) can be applied to Grafast schemas.

### Concurrency
Grafast's batching model reduces database load significantly compared to traditional resolvers. However, you should still configure:
- PostgreSQL connection pool sizes (via `pg` or `pgBouncer`)
- HTTP server concurrency limits (via your Node.js HTTP server or reverse proxy)

### Production Considerations
See: https://github.com/graphile/crystal/blob/main/grafast/website/grafast/production-considerations.md

Recommended production safeguards:
- Set maximum query depth
- Apply request timeouts at the HTTP layer (e.g., nginx, Grafserv config)
- Monitor PostgreSQL query counts — Grafast's batching should keep these low relative to request volume
- Use `persisted queries` to prevent arbitrary query execution in production

## Infrastructure Rate Limits

If you deploy via a hosting provider (e.g., Fly.io, AWS, Render), rate limiting is controlled by:
- Your reverse proxy (nginx, Caddy, etc.)
- API gateway settings (AWS API Gateway, Cloudflare Workers)
- PostgreSQL connection limits

## Sponsorship / Support Access

Access to consulting and priority support is governed by sponsorship tier, not API rate limits. See `plans/grafast-plans.md` for details.
