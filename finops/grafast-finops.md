# Grafast FinOps

Grafast is MIT-licensed open-source software with no licensing fees. FinOps considerations focus on infrastructure costs and the financial impact of Grafast's performance characteristics.

## Direct Costs

| Item | Cost |
|------|------|
| Grafast npm package | $0 |
| License fees | $0 |
| API usage fees | $0 |
| Sponsorship (optional) | $0–Custom/month |

## Infrastructure Cost Impact

Grafast's core value proposition is significant reduction in infrastructure costs through query batching and elimination of N+1 problems.

### Database Cost Reduction
Traditional GraphQL resolvers generate one database query per resolver invocation (N+1 problem). Grafast's plan-based execution:
- Combines related queries into single batched calls
- Deduplicates identical sub-queries across a request
- Can reduce database query count by **10x–100x** for list-type queries

This directly translates to lower database compute costs:
- Fewer read replicas needed
- Lower RDS/Aurora instance sizing
- Reduced pgBouncer connection pool pressure
- Lower Supabase/Neon compute bills

### Server Cost Reduction
Because Grafast executes more work in fewer round-trips:
- CPU time per request decreases
- Event loop utilization improves
- Fewer concurrent connections needed to serve the same load
- Lower Node.js instance count or smaller instance sizing

### Estimated Savings
For a production application processing 1M GraphQL requests/day:
- Typical resolver approach: 10–50 DB queries per request = 10M–50M queries/day
- Grafast approach: 1–5 DB queries per request = 1M–5M queries/day
- Reduction: 80–90% fewer database operations

Actual savings depend on schema design and query patterns.

## Sponsorship ROI

Optional sponsorships starting at $25/month provide:
- Priority support (faster resolution of blocking issues)
- Access to consulting (can prevent expensive re-architecture)
- Sustaining active development of the tool

For organizations saving thousands per month in database costs, sponsoring Grafast development provides strong ROI.

## Open Source Sustainability

Grafast is crowd-funded. Organizations that rely on Grafast in production are encouraged to contribute to its sustainability:
- GitHub Sponsors: https://github.com/sponsors/benjie
- Sponsor page: https://grafast.org/support/

## Cost Monitoring Recommendations

1. **Before Grafast**: Baseline your PostgreSQL query counts per GraphQL request
2. **After Grafast**: Measure query count reduction and translate to DB cost savings
3. **Track**: Node.js CPU time, memory per request, and P99 response latency
4. **Tools**: Use `EXPLAIN ANALYZE` in PostgreSQL and Grafast's built-in explain output to audit plan efficiency
