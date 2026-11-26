# Vision and Business Case

> **Status:** Draft · **Owner:** Founder / Product Lead · **Audience:** Stakeholders, investors, leadership, all teams
> **Last reviewed:** 2026-11-26

> Items marked **[TBD]** are placeholders. Replace them with confirmed figures before sharing outside the team.

## 1. Vision statement

Give growing businesses one cloud system that runs their whole operation (finance, inventory, sales, purchasing, HR and reporting) without the cost, consultants and long rollout that traditional ERP needs.

## 2. Mission

Ship a modular, multi-tenant ERP SaaS that a small or mid-sized company can sign up for, configure and use in days, not months. Customers start with one module and add more as they grow.

## 3. The problem

Small and mid-sized businesses (SMBs) usually run on a patchwork of tools:

| Pain | What it looks like today | Cost to the business |
|---|---|---|
| Disconnected data | Sales in spreadsheets, stock in another app, accounts in desktop software | Manual re-entry, errors, no single truth |
| No real-time view | Month-end reports built by hand | Slow decisions, cash surprises |
| Legacy ERP is too heavy | Big-vendor ERP needs consultants, servers and 6–18 month rollouts | Out of reach for SMB budgets |
| Compliance burden | Tax, invoicing and audit rules handled manually | Penalties, audit risk |
| Poor scalability | Tools break when the company adds a branch, warehouse or currency | Re-platforming every few years |

## 4. The solution

A cloud ERP with:

- **Modular design.** Core platform plus pluggable modules (Finance, Inventory, Sales, Purchasing, HR & Payroll, Reporting). Customers pay for what they use.
- **Multi-tenant SaaS.** No servers to manage. Updates ship continuously.
- **Fast onboarding.** Guided setup, data import templates and industry presets.
- **Open integration.** REST API, webhooks and connectors for payments, e-commerce and banks.
- **Built-in compliance.** Audit trail on every record, role-based access, configurable tax rules and localization.

## 5. Target market

| Segment | Size (employees) | Priority | Notes |
|---|---|---|---|
| Small businesses | 10–50 | Primary (launch) | Outgrowing spreadsheets and basic accounting tools |
| Mid-market | 50–500 | Secondary (year 2) | Multi-branch, multi-warehouse, approval workflows |
| Enterprise | 500+ | Later | Requires SSO, custom SLAs, dedicated hosting |

Initial industries: **[TBD]** (suggested: retail and wholesale distribution, light manufacturing, professional services).
Initial geography: **[TBD]**.

## 6. Business model

- **Subscription (SaaS), billed per user per month**, with module-based tiers. See [Go-to-market](../marketing/04-go-to-market.md) for tiers.
- **Annual contracts** at a discount for mid-market.
- **Add-on revenue:** premium support, implementation packages, extra storage, marketplace integrations.

## 7. Value to customers (expected outcomes)

| Outcome | Target | How we measure |
|---|---|---|
| Time to go live | < 14 days for Starter tier | Signup to first posted invoice |
| Month-end close time | Reduced by 50% | Customer survey and in-app close timestamps |
| Manual data entry | Reduced by 60% | Imported/automated vs manually entered records |
| Stock accuracy | > 98% | Cycle count variance |

## 8. Success metrics for the business

| Metric | Year 1 target | Year 2 target |
|---|---|---|
| Paying tenants | [TBD] | [TBD] |
| Annual recurring revenue (ARR) | [TBD] | [TBD] |
| Monthly logo churn | < 2% | < 1.5% |
| Net revenue retention | > 100% | > 110% |
| Customer acquisition cost payback | < 12 months | < 9 months |
| Platform uptime | 99.9% | 99.95% |

## 9. High-level cost drivers

- Engineering team (largest cost)
- Cloud infrastructure (scales with tenants; target < 15% of revenue)
- Customer success and support
- Sales and marketing
- Compliance and security audits (for example SOC 2)

## 10. Key assumptions

1. SMBs in the target segment will pay a monthly subscription for an integrated system.
2. A modular entry point (one module first) lowers the barrier to buy.
3. Self-serve onboarding can handle most Starter customers without a consultant.
4. A modular monolith can serve the first several thousand tenants before services need to be split out (see [ADR-0001](../architecture/adr/0001-modular-monolith.md)).

## 11. Related documents

- [Stakeholder overview](02-stakeholder-overview.md)
- [Project charter](03-project-charter.md)
- [Product requirements](../product/01-product-requirements.md)
