# Development Setup

> **Status:** Draft · **Owner:** Tech Lead · **Audience:** All engineers
> Goal: a new developer runs the app locally in under 30 minutes. If it takes longer, fix this page.

> The codebase does not exist yet. Commands below describe the **planned** setup from [ADR-0003](../architecture/adr/0003-technology-stack.md). Update them when the scaffold lands.

## 1. Prerequisites

| Tool | Version | Install |
|---|---|---|
| Git | 2.40+ | https://git-scm.com |
| Node.js | Current LTS (use `.nvmrc`) | `nvm install` |
| pnpm | 9+ | `corepack enable` |
| Docker Desktop / Docker Engine | Latest | https://docs.docker.com/get-docker |
| An editor | VS Code recommended (extensions list in `.vscode/extensions.json`) | |

## 2. Planned repository layout

```
.
├── apps/
│   ├── web/              # Next.js frontend
│   └── api/              # NestJS backend (modular monolith)
│       └── src/modules/  # core, finance, inventory, sales, purchasing, hr, reporting
├── packages/
│   ├── ui/               # shared React components (design system)
│   ├── contracts/        # shared types and validation schemas (zod)
│   ├── config/           # shared eslint, tsconfig, prettier
│   └── testing/          # test utilities, factories
├── infra/                # Terraform
├── docs/                 # this documentation
├── docker-compose.yml    # local PostgreSQL, Redis, MinIO (S3), Mailpit
└── turbo.json
```

## 3. First run

```bash
git clone https://github.com/tufanrai/ERP-Enterprise-Resource-Planning-.git
cd ERP-Enterprise-Resource-Planning-
nvm use
corepack enable
pnpm install
cp .env.example .env          # local defaults, no real secrets
docker compose up -d          # PostgreSQL, Redis, MinIO, Mailpit
pnpm db:migrate
pnpm db:seed                  # demo tenant + demo users
pnpm dev                      # starts web (http://localhost:3000) and api (http://localhost:4000)
```

Demo login (local only): `admin@demo.local` / `Password123!`

## 4. Useful commands

| Command | What it does |
|---|---|
| `pnpm dev` | Run web and API in watch mode |
| `pnpm test` | Unit tests |
| `pnpm test:int` | Integration tests (uses Docker via Testcontainers) |
| `pnpm test:e2e` | Playwright end-to-end tests |
| `pnpm lint` / `pnpm typecheck` | Static checks |
| `pnpm db:migrate` | Apply migrations |
| `pnpm db:migration:new <name>` | Create a migration |
| `pnpm db:reset` | Drop, migrate and seed the local database |

## 5. Local services

| Service | URL |
|---|---|
| Web app | http://localhost:3000 |
| API | http://localhost:4000 |
| API docs (OpenAPI) | http://localhost:4000/docs/api |
| Mailpit (catches emails) | http://localhost:8025 |
| MinIO console (files) | http://localhost:9001 |

## 6. Troubleshooting

| Problem | Fix |
|---|---|
| Port already in use | Stop the other process or change the port in `.env` |
| Migrations fail | `pnpm db:reset` |
| Docker containers not healthy | `docker compose down -v && docker compose up -d` |
| Type errors after pulling | `pnpm install` then restart the TypeScript server in your editor |
