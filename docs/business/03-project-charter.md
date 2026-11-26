# Project Charter

> **Status:** Draft · **Owner:** Project Sponsor · **Audience:** Leadership, project leads
> **Approval:** [TBD: sponsor signature and date]

## 1. Project name

ERP SaaS Platform (working name: **[Product name TBD]**)

## 2. Purpose

Build and launch a modular, multi-tenant cloud ERP for small and mid-sized businesses. Background: [Vision and business case](01-vision-and-business-case.md).

## 3. Objectives (SMART)

1. Deliver an MVP with Platform Core, Finance, Inventory and Sales modules to pilot customers by **[TBD]**.
2. Onboard **10–20 paying pilot tenants** during beta.
3. Reach **99.9% monthly uptime** from beta onward.
4. Pass an external security assessment before general availability.
5. Keep cloud cost below **15% of revenue** at general availability.

## 4. Scope

### In scope
- Web application (responsive, desktop-first)
- Modules: Core, Finance, Inventory, Sales, Purchasing, HR & Payroll, Reporting
- Public REST API and webhooks
- Self-serve signup, subscription billing, tenant administration
- Data import (CSV/Excel) and export
- Admin back-office for our support team

### Out of scope (for now)
- Native mobile apps (planned post-GA; the web app is responsive)
- On-premise installation
- Manufacturing resource planning (MRP), CRM marketing automation, e-commerce storefront
- Country-specific statutory payroll beyond launch markets

## 5. Deliverables

| Deliverable | Owner | Acceptance |
|---|---|---|
| Product requirements and designs | Product Lead | Signed off by sponsor |
| Architecture and ADRs | Tech Lead | Reviewed by engineering |
| MVP release | Engineering | Passes acceptance tests, pilot sign-off |
| Documentation set (this folder) | All leads | Reviewed per [docs index](../README.md) |
| Security assessment report | Security Lead | No open critical/high findings |
| Go-to-market plan | Marketing Lead | Approved by sponsor |

## 6. Milestones

| # | Milestone | Target date |
|---|---|---|
| M0 | Charter approved | [TBD] |
| M1 | Architecture and UX sign-off | [TBD] |
| M2 | MVP feature complete | [TBD] |
| M3 | Pilot customers live | [TBD] |
| M4 | Beta (billing, purchasing, integrations) | [TBD] |
| M5 | General availability | [TBD] |

## 7. Roles and responsibilities (RACI)

R = Responsible, A = Accountable, C = Consulted, I = Informed

| Activity | Sponsor | Product Lead | Tech Lead | Engineers | Design | QA | Marketing | Security |
|---|---|---|---|---|---|---|---|---|
| Business case & budget | A | R | C | I | I | I | C | I |
| Requirements (PRD) | C | A/R | C | C | C | C | C | C |
| Architecture & ADRs | I | C | A/R | R | I | C | I | C |
| UX/UI design | I | A | C | C | R | C | C | I |
| Implementation | I | C | A | R | C | C | I | C |
| Testing & quality | I | C | A | R | I | R | I | C |
| Security & compliance | I | I | C | R | I | C | I | A/R |
| Release | I | A | R | R | I | R | I | C |
| Marketing & launch | C | C | I | I | C | I | A/R | I |

## 8. Team (to be filled)

| Role | Name | Contact |
|---|---|---|
| Project Sponsor | [TBD] | [TBD] |
| Product Lead | [TBD] | [TBD] |
| Tech Lead | [TBD] | [TBD] |
| Design Lead | [TBD] | [TBD] |
| QA Lead | [TBD] | [TBD] |
| Marketing Lead | [TBD] | [TBD] |
| Security Lead | [TBD] | [TBD] |

## 9. Budget

| Category | Estimate |
|---|---|
| People | [TBD] |
| Cloud and tooling | [TBD] |
| Security audit | [TBD] |
| Marketing launch | [TBD] |
| Contingency (10–15%) | [TBD] |

## 10. Constraints and assumptions

- Small founding team; scope must be phased.
- Cloud-only delivery.
- Assumptions are listed in the [business case](01-vision-and-business-case.md#10-key-assumptions).

## 11. Risks

See the [Risk register](04-risk-register.md).

## 12. Governance

- Two-week sprints with demo and retrospective.
- Monthly steering committee reviews scope, budget, timeline and risks.
- Scope changes go through a change request reviewed by the Product Lead and Sponsor.
