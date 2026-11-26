# Infrastructure and Deployment

> **Status:** Draft · **Owner:** Tech Lead / DevOps · **Audience:** Engineers, DevOps
> **MVP decision:** no AWS. Everything runs as Docker containers on **Contabo Linux VPS** servers ([ADR-0005](adr/0005-mvp-hosting-without-aws.md)).

## 1. Environments

| Environment | Purpose | Data | Deploys |
|---|---|---|---|
| Local | Development | Seed data | Developer machine (Docker Compose) |
| Staging | Integration and QA, mirrors production | Synthetic | Automatically on merge to `main` |
| Production | Customers | Real | Manual approval after staging checks |
| Preview (later) | Review a pull request | Seed data | Per PR, once the team grows |

## 2. MVP hosting layout

```mermaid
flowchart TB
  user[Users' browsers] --> cdn[CDN / WAF<br/>optional, e.g. Cloudflare]
  cdn --> proxy

  subgraph Server["Production: Contabo Linux VPS (Ubuntu LTS)"]
    proxy[Reverse proxy<br/>Caddy or Nginx, automatic TLS]
    web[web container<br/>Next.js]
    api[api container<br/>NestJS]
    wrk[worker container<br/>BullMQ]
    redis[(redis container)]
    minio[(minio container<br/>S3-compatible files)]
    pg[(postgres container)]
  end

  backup[(Off-site backups<br/>Contabo Object Storage in another region,<br/>or a second provider)]
  mon[Monitoring and error tracking]

  proxy --> web & api
  api --> pg & redis & minio
  wrk --> pg & redis & minio
  pg -. nightly + WAL backups .-> backup
  minio -. daily sync .-> backup
  api & wrk & web -.-> mon
```

- **Start small:** one Contabo VPS for production (for example 6+ vCPU / 12+ GB RAM / NVMe; size to the current Contabo plans) and a smaller VPS for staging.
- **Next step when load grows:** move PostgreSQL to its own Contabo VPS on the private network, then add a second app VPS behind the proxy.
- **Scale up first, then out:** add CPU/RAM, then run several `api` and `worker` replicas behind the proxy.
- Server setup is scripted (for example Ansible or a cloud-init script) and kept in `infra/`, so a server can be rebuilt from scratch.

## 3. Contabo server setup checklist

Contabo provides unmanaged VPS servers, so we harden and maintain them ourselves. Script every step in `infra/` (Ansible or cloud-init).

- [ ] Ubuntu LTS image; automatic security updates (`unattended-upgrades`)
- [ ] Non-root sudo user; SSH key login only; root login and password login disabled
- [ ] Firewall (`ufw`): allow only 22 (ideally from known IPs), 80 and 443
- [ ] `fail2ban` for SSH
- [ ] Docker Engine and Docker Compose plugin installed from the official repository
- [ ] PostgreSQL, Redis and MinIO bound to the Docker network only, never exposed publicly (note: Docker port mappings bypass `ufw`, so don't publish these ports)
- [ ] Caddy (or Nginx + certbot) for automatic TLS certificates
- [ ] DNS through Cloudflare (optional proxy/WAF in front of the VPS IP)
- [ ] Secrets in a root-only `.env` file on the server (or an encrypted file decrypted at deploy, e.g. SOPS); never in git
- [ ] Backup jobs scheduled and their first restore tested
- [ ] Monitoring agent (node exporter / Grafana Alloy) and uptime check configured
- [ ] Contabo snapshot taken after initial setup (a convenience, not a replacement for off-site backups)

## 4. CI/CD pipeline (GitHub Actions)

```mermaid
flowchart LR
  pr[Pull request] --> checks[Lint, type check,<br/>unit + integration tests,<br/>security scans]
  checks --> review[Code review approved]
  review --> merge[Merge to main]
  merge --> build[Build Docker images<br/>push to GitHub Container Registry]
  build --> stg[Deploy to staging<br/>docker compose pull && up -d]
  stg --> e2e[E2E + smoke tests]
  e2e --> approve[Manual approval]
  approve --> prod[Deploy to production]
  prod --> smoke[Smoke tests + monitoring]
```

- Images are tagged with the commit SHA and stored in **GitHub Container Registry**.
- Deploy = SSH (or the platform's deploy hook) → `docker compose pull` → run migrations → `docker compose up -d`.
- Migrations must be **backward compatible** (expand, then contract), so rolling back the app never needs a schema rollback.
- Rollback = redeploy the previous image tag.

## 5. Backups and disaster recovery

| Item | MVP policy |
|---|---|
| Database | Nightly `pg_dump` plus continuous WAL archiving (pgBackRest or WAL-G) to Contabo Object Storage in a different region, or to a second provider |
| Files (MinIO) | Daily sync to off-site S3-compatible storage in a different region or provider |
| Server config | Scripted in `infra/`; no hand-made changes. Contabo snapshots before risky changes |
| Restore test | Monthly during MVP, documented |
| Targets | MVP: RPO ≤ 1 h, RTO ≤ 8 h. From Beta: RPO ≤ 15 min, RTO ≤ 4 h |

## 6. Observability (provider-neutral)

| Signal | Tool (proposed) | Notes |
|---|---|---|
| Logs | Grafana Loki (self-hosted or Grafana Cloud free tier) | Structured JSON, `requestId`, `tenantId`, no secrets or personal data |
| Metrics | Prometheus + Grafana | RED metrics per endpoint, queue depth, DB and host health |
| Traces | OpenTelemetry → Grafana Tempo | Added once the MVP is stable |
| Errors | Sentry (cloud or self-hosted) | Frontend and backend |
| Uptime | External checks (e.g. UptimeRobot / Better Stack) | Public status page |

## 7. Alerting (starting set)

| Alert | Threshold | Severity |
|---|---|---|
| Site down | Uptime check fails twice | SEV1 |
| API error rate | > 2% for 5 min | SEV2 |
| Backup job failed | Any failure | SEV2 |
| Disk usage | > 80% | SEV3 |
| API p95 latency | > 1 s for 10 min | SEV3 |
| Queue backlog | Oldest job > 10 min | SEV3 |
| TLS certificate | Expires in < 14 days | SEV3 |

## 8. Availability targets

| Phase | Target | Why |
|---|---|---|
| MVP (pilots) | 99.5% monthly | Single server; pilots are told about planned maintenance |
| Beta onward | 99.9% monthly | Requires redundancy (second app server, managed DB with standby); see ADR-0005 revisit triggers |

## 9. Moving off Contabo later

Because the code uses only portable interfaces (S3 API, PostgreSQL, Redis, SMTP, env vars), moving to AWS, GCP or Azure is a hosting project: provision equivalents, restore the database, sync files, switch DNS. Write a new ADR that supersedes ADR-0005 when that happens.

## 10. Cost management

- Track monthly hosting cost per environment.
- Review cost per tenant monthly once there are paying customers.
