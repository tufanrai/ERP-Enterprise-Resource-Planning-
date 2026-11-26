# New Developer Guide

> **Status:** Draft · **Owner:** Tech Lead · **Audience:** New engineers
> Welcome! This guide replaces the "let me walk you through the project" meeting. Work through it in order. Ask questions in the team channel; if the answer isn't in the docs, add it.

## Day 1: Understand the product

Read, in this order (about 1.5 hours):

1. [Stakeholder overview](../business/02-stakeholder-overview.md): what we're building and why (5 min)
2. [Vision and business case](../business/01-vision-and-business-case.md) (15 min)
3. [Personas and user journeys](../product/02-personas-and-user-journeys.md) (15 min)
4. [Product requirements](../product/01-product-requirements.md): skim, focus on the module you'll work on (30 min)
5. [Glossary](02-glossary.md): ERP and accounting terms you'll hear daily (15 min)

**Check yourself:** Can you explain order-to-cash and why every journal entry must balance?

## Day 2: Understand the system

1. [System architecture](../architecture/01-system-architecture.md) (30 min)
2. All [ADRs](../architecture/adr/README.md) (30 min)
3. [Data model](../architecture/02-data-model.md) (20 min)
4. [API design](../architecture/03-api-design.md) (20 min)
5. [Security and compliance](../architecture/04-security-and-compliance.md) (20 min)

**Check yourself:** How does the system keep tenant A from seeing tenant B's data? (Three layers. See ADR-0002.)

## Day 3: Get it running

1. Follow [Development setup](../engineering/01-development-setup.md).
2. Sign in to the local demo tenant and walk through journey J1 (sign up to first invoice).
3. Read [Coding standards](../engineering/02-coding-standards.md) and [Git workflow](../engineering/03-git-workflow-and-contributing.md).
4. Read [Testing strategy](../engineering/04-testing-strategy.md).

## Week 1: First contribution

- Pick a ticket labelled `good first issue`.
- Pair with your onboarding buddy for the first PR.
- Ship it to staging.
- Fix one thing in these docs that confused you. That's part of onboarding.

## Accounts and access checklist

| Access | Who grants it | Done |
|---|---|---|
| GitHub organization and repo | Tech Lead | ☐ |
| Project tracker | Project Manager | ☐ |
| Team chat | Project Manager | ☐ |
| Cloud (staging, read-only at first) | Tech Lead | ☐ |
| Error tracking and monitoring | Tech Lead | ☐ |
| Design files | Design Lead | ☐ |
| Password manager | Tech Lead | ☐ |

## Who to ask

| Topic | Person |
|---|---|
| Product and requirements | Product Lead [TBD] |
| Architecture and code | Tech Lead [TBD] |
| Infrastructure and access | DevOps [TBD] |
| Design | Design Lead [TBD] |
| Your onboarding buddy | [Assigned on day 1] |

## 30 / 60 / 90 days

| By | You should be able to |
|---|---|
| 30 days | Ship small features in one module end to end, with tests |
| 60 days | Own a feature across modules; review others' PRs |
| 90 days | Join on-call; lead the design of a medium feature, including an ADR if needed |
