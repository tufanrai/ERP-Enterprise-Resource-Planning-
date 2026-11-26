# Risk Register

> **Status:** Living document · **Owner:** Project Manager · **Audience:** Leadership, project leads
> Review at every steering committee meeting.

Scoring: Likelihood (L) and Impact (I) from 1 (low) to 5 (high). Score = L × I.

| ID | Risk | Category | L | I | Score | Mitigation | Owner | Status |
|---|---|---|---|---|---|---|---|---|
| R1 | Scope creep delays MVP | Delivery | 4 | 4 | 16 | Strict MVP scope in PRD, change requests, phased roadmap | Product Lead | Open |
| R2 | Data leak between tenants | Security | 2 | 5 | 10 | Row-level security in the database, tenant-scoped repositories, automated isolation tests ([ADR-0002](../architecture/adr/0002-multi-tenancy-strategy.md)) | Tech Lead | Open |
| R3 | Accounting logic errors damage customer trust | Quality | 3 | 5 | 15 | Double-entry invariants enforced in code and DB, property-based tests, accountant review | Tech Lead | Open |
| R4 | Key engineer leaves | People | 3 | 4 | 12 | Documentation (this folder), pairing, code review, no single owners | Tech Lead | Open |
| R5 | Low adoption by pilot customers | Market | 3 | 4 | 12 | Early customer interviews, onboarding wizard, success manager for pilots | Product Lead | Open |
| R6 | Cloud cost grows faster than revenue | Financial | 2 | 3 | 6 | Cost dashboards, budgets and alerts, right-sizing reviews | Tech Lead | Open |
| R7 | Compliance requirements in a target market not met | Legal | 3 | 4 | 12 | Legal review per market, configurable tax and localization engine | Sponsor | Open |
| R8 | Major outage or data loss | Operations | 2 | 5 | 10 | Multi-AZ deployment, backups with tested restores, incident runbooks | Tech Lead | Open |
| R9 | Strong competitor launches a similar SMB offer | Market | 3 | 3 | 9 | Focus on niche industries, fast onboarding, local support | Marketing Lead | Open |
| R10 | Performance problems as tenants grow | Technical | 3 | 3 | 9 | Load testing before each phase, indexes reviewed, read replicas, caching | Tech Lead | Open |

## How to add a risk

1. Add a row with the next ID.
2. Score it and name one owner.
3. Raise anything scoring 15 or more at the next steering meeting.
