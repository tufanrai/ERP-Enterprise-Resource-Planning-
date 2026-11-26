# Release and Operations

> **Status:** Draft · **Owner:** Tech Lead · **Audience:** Engineers, on-call, support

## Release process

- Continuous delivery: every merge to `main` deploys to staging; production deploys are approved by the on-call engineer or Tech Lead.
- Versioning: date-based release tags (`2026.11.26-1`) for the app; semantic versioning for the public API.
- Release notes are generated from Conventional Commit messages and edited for customers.
- Risky features ship behind feature flags and roll out to internal tenant → pilot tenants → everyone.

### Deployment checklist
- [ ] Staging E2E and smoke tests green
- [ ] Migrations are backward compatible
- [ ] Feature flags set
- [ ] Monitoring dashboard open during rollout
- [ ] Rollback plan known (previous image tag)

## On-call

- Weekly rotation among backend engineers once there are paying customers.
- Pager for SEV1/SEV2 alerts; SEV3+ handled in working hours.
- Hand-over note at the end of each rotation.

## Incident management

| Severity | Definition | Response |
|---|---|---|
| SEV1 | Platform down or data leak/loss | Immediate, all hands, status page updated within 15 min |
| SEV2 | Major feature broken for many tenants | Within 30 min |
| SEV3 | Minor feature broken or degraded performance | Same working day |
| SEV4 | Cosmetic / low impact | Normal backlog |

Steps: declare → assign incident lead → communicate (status page, support) → mitigate → resolve → post-incident review within 5 working days.

## Runbooks (to be written as the system is built)

| Runbook | Covers |
|---|---|
| `runbooks/database-failover.md` | Database restore and failover to a standby/replica |
| `runbooks/restore-from-backup.md` | Point-in-time restore of one tenant or all |
| `runbooks/queue-backlog.md` | Draining stuck BullMQ jobs |
| `runbooks/rotate-secrets.md` | Rotating database, API and signing secrets |
| `runbooks/tenant-data-export.md` | Exporting and deleting a tenant's data |

## Service level objectives

| SLO | Target |
|---|---|
| Availability | 99.5% monthly (MVP), 99.9% (Beta onward) |
| API p95 latency | < 300 ms (reads) |
| Webhook delivery | 99% within 1 minute |
| Support first response | < 4 working hours (Business), < 1 hour (Enterprise) |
