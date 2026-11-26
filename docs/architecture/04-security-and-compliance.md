# Security and Compliance

> **Status:** Draft · **Owner:** Security Lead / Tech Lead · **Audience:** Engineering, leadership, enterprise customers (summarized), auditors

## 1. Principles

1. **Least privilege** for users, services and engineers.
2. **Defense in depth.** Never rely on one control, especially for tenant isolation.
3. **Secure by default.** MFA available to all, strong defaults, no public buckets.
4. **Everything audited.** Business changes and admin access are logged.

## 2. Threat model summary (STRIDE)

| Threat | Example | Key controls |
|---|---|---|
| Spoofing | Stolen password | MFA, rate limiting, breached-password check, SSO |
| Tampering | Changing a posted invoice | Immutable postings, audit log, permissions |
| Repudiation | "I didn't approve that" | Audit log with actor, time, IP |
| Information disclosure | Tenant A sees tenant B data | RLS, tenant-scoped repositories, isolation tests, 404 for foreign IDs |
| Denial of service | API flooding | WAF, rate limits, autoscaling |
| Elevation of privilege | User grants themselves admin | Permission checks server-side, role changes audited and restricted |

## 3. Controls

### Identity and access
- Passwords hashed with Argon2id; minimum length 12; breached-password check.
- TOTP MFA; enforced for tenant admins; enforceable per tenant for all users.
- SSO (SAML 2.0 / OIDC) for Business and Enterprise plans.
- Session timeout and device/session list with remote sign-out.
- Our staff access customer data only through the support back-office, with tenant consent ("support access" toggle), time-limited and audited.

### Data protection
- TLS 1.2+ everywhere; HSTS.
- Encryption at rest for database, backups and object storage (AWS KMS).
- Application-level encryption for sensitive fields (bank accounts, national IDs, salaries).
- Secrets in AWS Secrets Manager; never in code or environment files committed to git.

### Application security
- Follow OWASP ASVS Level 2 and OWASP Top 10.
- Input validation on every endpoint; parameterized queries only (ORM/query builder).
- Output encoding in the frontend (React default); strict Content Security Policy.
- CSRF protection for cookie-based auth.
- File uploads: type and size checks, malware scan, served from a separate domain.

### Secure development lifecycle
- Code review required for every change.
- CI runs SAST, dependency scanning, secret scanning and container image scanning.
- Security-relevant changes (auth, permissions, tenancy) need a second reviewer.
- Annual third-party penetration test; before GA as a minimum.

### Infrastructure
- Private subnets for databases and workers; no public database endpoints.
- Infrastructure as code with peer review.
- Engineers use SSO with MFA into cloud accounts; production access is just-in-time and logged.

## 4. Compliance roadmap

| Framework | Why | Target |
|---|---|---|
| GDPR (and similar local privacy laws) | Customers' personal data | Before GA |
| SOC 2 Type I, then Type II | Mid-market and enterprise buyers ask for it | Type I in year 2 |
| ISO 27001 | International enterprise customers | Later |
| Local e-invoicing / tax authority rules | Legal requirement per launch country | Per market [TBD] |

## 5. Privacy

- We are the **data processor**; customers are **data controllers**. A Data Processing Agreement (DPA) is offered.
- Data subject requests: export and delete personal data per tenant.
- List of sub-processors (cloud provider, email provider, etc.) is published and kept current.

## 6. Incident response

1. **Detect** via alerts, reports or customer contact.
2. **Triage** severity (SEV1–SEV4) and appoint an incident lead.
3. **Contain and fix.**
4. **Notify** affected customers within contractual/legal timelines (for example 72 hours for personal data breaches under GDPR).
5. **Post-incident review** within 5 working days, blameless, with action items.

Details: [Release and operations](../engineering/05-release-and-operations.md#incident-management).

## 7. Reporting a vulnerability

Report security issues privately to **[security contact TBD]**. Do not open a public issue.
