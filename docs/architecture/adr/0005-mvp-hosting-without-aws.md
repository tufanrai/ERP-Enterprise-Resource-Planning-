# ADR-0005: Docker hosting on Contabo Linux VPS for the MVP, no AWS

- **Status:** Accepted
- **Date:** 2026-11-26
- **Deciders:** Project owner, Tech Lead

## Context

The MVP must be cheap to run and simple for a small team to operate. AWS-specific managed services (ECS, RDS, ElastiCache, Secrets Manager) add cost, learning time and lock-in before we have paying customers. The stack in [ADR-0003](0003-technology-stack.md) is already fully containerized.

## Decision

- **Do not use AWS for the MVP.**
- Run the whole system as **Docker containers** described by Docker Compose: `web`, `api`, `worker`, `postgres`, `redis`, `minio` (S3-compatible storage) and a reverse proxy (Caddy or Nginx) for TLS.
- Host on **Contabo Linux VPS** servers (Ubuntu LTS recommended), one for production and a smaller one for staging.
- Run **PostgreSQL in a container** on the production VPS (or on a dedicated database VPS once load grows), with automated backups shipped off the server. Contabo does not offer a managed PostgreSQL service at the time of writing, so backups, restore tests and upgrades are our responsibility.
- Store files in **MinIO** on the VPS for the MVP, or in **Contabo Object Storage** (S3-compatible) if we want files off the app server. Keep backups in object storage in a **different region** from the VPS, or with a second provider.
- Use only **portable interfaces** in code: the S3 API for files, standard PostgreSQL, standard Redis, SMTP or a provider-neutral email API, and environment variables for configuration. No cloud-vendor SDKs in application code.
- A CDN/WAF in front (for example Cloudflare) is optional but recommended.

## Consequences

- ✅ Low monthly cost (Contabo VPS pricing is well suited to an early-stage product) and fast to set up.
- ✅ The same `docker-compose.yml` runs locally, in staging and in production, so environments stay alike.
- ✅ No lock-in: moving from Contabo to AWS, GCP, Azure or another VPS provider later is a hosting change, not a code change.
- ⚠️ More operational work falls on us: server hardening, backups, restore tests, OS patching, monitoring and TLS renewal must be set up and owned (see the server checklist in [Infrastructure and deployment](../05-infrastructure-and-deployment.md#3-contabo-server-setup-checklist)).
- ⚠️ A single VPS is a single point of failure. Keep provisioning scripted so a replacement server can be built quickly.
- ⚠️ Fewer built-in high-availability options. The MVP availability target is relaxed to **99.5%** (see [Infrastructure and deployment](../05-infrastructure-and-deployment.md)); the 99.9% target applies from Beta.
- 🔁 Revisit this decision before Beta, or when any of these is true: more than ~200 active tenants, a customer requires certified cloud hosting, or ops work takes more than a day a week.
