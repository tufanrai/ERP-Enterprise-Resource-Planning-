# Project Documentation

This folder is the single source of truth for the ERP SaaS project: why we're building it, what it does, how it's built and how to sell it.

> **Status:** Initial draft (2026-11-26). Items marked **[TBD]** need a decision or real data. Technology choices are **proposals** until their [ADRs](architecture/adr/README.md) are accepted.

## Start here: reading paths by role

| You are... | Read these, in order |
|---|---|
| **Stakeholder / leadership / investor** | [Stakeholder overview](business/02-stakeholder-overview.md) → [Vision and business case](business/01-vision-and-business-case.md) → [Roadmap](product/03-roadmap.md) → [Risk register](business/04-risk-register.md) |
| **New developer** | [New developer guide](onboarding/01-new-developer-guide.md) (it walks you through everything else) |
| **Engineer (existing)** | [System architecture](architecture/01-system-architecture.md) → [ADRs](architecture/adr/README.md) → [Coding standards](engineering/02-coding-standards.md) |
| **Product / design** | [PRD](product/01-product-requirements.md) → [Personas and journeys](product/02-personas-and-user-journeys.md) → [Roadmap](product/03-roadmap.md) |
| **Marketing / sales** | [Positioning and messaging](marketing/01-positioning-and-messaging.md) → [Feature brief](marketing/02-product-feature-brief.md) → [Go-to-market](marketing/04-go-to-market.md) → [Competitive landscape](marketing/03-competitive-landscape.md) |
| **Support / customer success** | [Feature catalog](product/04-feature-catalog.md) → [Glossary](onboarding/02-glossary.md) → [FAQ](onboarding/03-faq.md) |
| **Security / compliance** | [Security and compliance](architecture/04-security-and-compliance.md) → [ADR-0002 Multi-tenancy](architecture/adr/0002-multi-tenancy-strategy.md) |

## All documents

### 1. Business — *why* we're doing this
| Document | Purpose | Owner |
|---|---|---|
| [Vision and business case](business/01-vision-and-business-case.md) | Problem, solution, market, business model, success metrics | Founder / Product |
| [Stakeholder overview](business/02-stakeholder-overview.md) | One-page summary, stakeholder map, communication plan | Project Manager |
| [Project charter](business/03-project-charter.md) | Objectives, scope, milestones, RACI, budget, governance | Sponsor |
| [Risk register](business/04-risk-register.md) | Risks, scores, mitigations, owners | Project Manager |

### 2. Product — *what* we're building
| Document | Purpose | Owner |
|---|---|---|
| [Product requirements (PRD)](product/01-product-requirements.md) | Functional and non-functional requirements by module | Product Lead |
| [Personas and user journeys](product/02-personas-and-user-journeys.md) | Who uses it and their key workflows | Product / Design |
| [Roadmap](product/03-roadmap.md) | Phases from discovery to GA and beyond | Product Lead |
| [Feature catalog](product/04-feature-catalog.md) | Plain-language list of features by module and phase | Product Lead |

### 3. Architecture — *how* it's built
| Document | Purpose | Owner |
|---|---|---|
| [System architecture](architecture/01-system-architecture.md) | C4 diagrams, modules, key flows, cross-cutting concerns | Tech Lead |
| [Data model](architecture/02-data-model.md) | Entities, conventions, accounting invariants | Tech Lead |
| [API design](architecture/03-api-design.md) | REST conventions, errors, pagination, webhooks | Tech Lead |
| [Security and compliance](architecture/04-security-and-compliance.md) | Threat model, controls, compliance roadmap, incident response | Security Lead |
| [Infrastructure and deployment](architecture/05-infrastructure-and-deployment.md) | Environments, cloud layout, CI/CD, backups, observability | DevOps |
| [Architecture Decision Records](architecture/adr/README.md) | Why each major technical decision was made | Tech Lead |

### 4. Engineering — *how we work*
| Document | Purpose | Owner |
|---|---|---|
| [Development setup](engineering/01-development-setup.md) | Run the project locally | Tech Lead |
| [Coding standards](engineering/02-coding-standards.md) | Conventions, module boundaries, naming | Tech Lead |
| [Git workflow and contributing](engineering/03-git-workflow-and-contributing.md) | Branching, commits, PRs, reviews, definition of done | Tech Lead |
| [Testing strategy](engineering/04-testing-strategy.md) | Test levels, tools, accounting correctness | QA Lead |
| [Release and operations](engineering/05-release-and-operations.md) | Releases, on-call, incidents, runbooks, SLOs | Tech Lead |

### 5. Marketing — *how we sell it*
| Document | Purpose | Owner |
|---|---|---|
| [Positioning and messaging](marketing/01-positioning-and-messaging.md) | Positioning statement, pillars, messages by audience | Marketing Lead |
| [Product feature brief](marketing/02-product-feature-brief.md) | Features translated into customer benefits, sales FAQ | Product Marketing |
| [Competitive landscape](marketing/03-competitive-landscape.md) | Competitor categories, differentiators | Marketing Lead |
| [Go-to-market plan](marketing/04-go-to-market.md) | ICP, pricing, launch phases, channels, funnel metrics | Marketing Lead |

### 6. Onboarding — *getting up to speed*
| Document | Purpose | Owner |
|---|---|---|
| [New developer guide](onboarding/01-new-developer-guide.md) | Day-by-day onboarding path, access checklist, 30/60/90 | Tech Lead |
| [Glossary](onboarding/02-glossary.md) | Business, accounting and technical terms | Everyone |
| [FAQ](onboarding/03-faq.md) | Common questions from the team | Everyone |

## Keeping docs alive

- Docs live next to the code and change in the same pull request as the code they describe.
- Every page lists an **owner** who reviews changes to it.
- Review the whole set at the end of each roadmap phase.
- Diagrams use [Mermaid](https://mermaid.js.org), which GitHub renders directly.
