# Team FAQ

> **Audience:** Everyone, especially new joiners. Add questions as they come up.

**Where do I start?**
The [docs index](../README.md) has a reading path for your role. Developers follow the [New developer guide](01-new-developer-guide.md).

**Why a monolith and not microservices?**
Small team, many tightly linked business processes, and a need for real transactions. See [ADR-0001](../architecture/adr/0001-modular-monolith.md).

**How do we stop tenants seeing each other's data?**
Three layers: database row-level security, tenant-scoped repositories and automated isolation tests. See [ADR-0002](../architecture/adr/0002-multi-tenancy-strategy.md).

**Can I edit a posted invoice?**
No. Posted financial documents are immutable. Create a credit note or reversing entry. This protects the audit trail.

**Why are amounts strings in the API?**
To avoid floating-point rounding errors. See [API design](../architecture/03-api-design.md#1-basics).

**How do I propose a big technical change?**
Write an ADR and open a PR. See [ADR README](../architecture/adr/README.md).

**How do I add a new module?**
Create `apps/api/src/modules/<name>` with the standard layers, its own database schema, RLS on every table, and export only its public interface from `index.ts`. Add it to the [feature catalog](../product/04-feature-catalog.md) and to the architecture diagram.

**Who approves product scope changes?**
The Product Lead, with the Sponsor for anything affecting timeline or budget. See the [Project charter](../business/03-project-charter.md#12-governance).

**The docs are wrong or out of date. What do I do?**
Fix them in a PR. Docs are owned by everyone; the owner listed at the top of each page reviews.
