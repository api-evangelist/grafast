# Grafast

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
