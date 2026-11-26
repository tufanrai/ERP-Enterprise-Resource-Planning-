# ADR-0002: Shared-schema multi-tenancy with PostgreSQL row-level security

- **Status:** Proposed
- **Date:** 2026-11-26
- **Deciders:** Tech Lead, Security Lead

## Context

We will host thousands of small tenants. Leaking data between tenants would be the worst possible failure. We also need low cost per tenant and simple migrations.

## Options considered

1. **Database per tenant.** Strongest isolation, but expensive and slow to migrate at thousands of tenants.
2. **Schema per tenant.** Good isolation, but migrations and connection pooling become hard beyond a few hundred tenants.
3. **Shared schema with `tenant_id`.** Cheapest and simplest to operate; isolation depends on correct filtering.

## Decision

Use **shared schema with `tenant_id`** on every tenant-owned table, protected by **three layers**:

1. **PostgreSQL row-level security (RLS)** policies on every tenant table, using a session variable `app.tenant_id` set at the start of each request transaction.
2. **Tenant-scoped repositories** in the application that always apply the tenant filter.
3. **Automated isolation tests** that create two tenants and assert that no endpoint returns or changes the other's data.

Large enterprise tenants can later be moved to a dedicated database (a "silo") using the same schema.

## Consequences

- ✅ Low cost, one migration path, simple operations.
- ✅ Defense in depth against application bugs.
- ⚠️ Every new table must have `tenant_id` and an RLS policy; a migration lint check enforces this.
- ⚠️ "Noisy neighbor" risk; mitigated by rate limits, query timeouts and monitoring per tenant.
