# Product Requirements Document (PRD)

> **Status:** Draft · **Owner:** Product Lead · **Audience:** Product, engineering, design, QA, leadership
> **Version:** 0.1

## 1. Overview

A multi-tenant cloud ERP for small and mid-sized businesses. This document defines **what** we build and **why**. **How** we build it is covered in [System architecture](../architecture/01-system-architecture.md).

## 2. Goals

1. One integrated system for finance, inventory, sales, purchasing and HR.
2. Self-serve setup in under 14 days for a typical small business.
3. Accurate, auditable financial records (double-entry, immutable audit trail).
4. Open API so customers can connect their other tools.

### Non-goals (this version)
- Native mobile apps, on-premise hosting, full MRP, CRM marketing automation.

## 3. Users

Full detail in [Personas and user journeys](02-personas-and-user-journeys.md).

| Persona | Primary modules |
|---|---|
| Business owner / CEO | Dashboards, reports |
| Finance manager / accountant | Finance, reporting |
| Operations / warehouse manager | Inventory, purchasing |
| Sales representative | Sales, customers |
| HR manager | HR & payroll |
| Tenant administrator | Users, roles, settings |
| Internal support agent (us) | Admin back-office |

## 4. Functional requirements

Priority uses MoSCoW: **M**ust, **S**hould, **C**ould, **W**on't (this release).

### 4.1 Platform core

| ID | Requirement | Priority |
|---|---|---|
| CORE-01 | Organizations can sign up and create a tenant with a guided setup wizard | M |
| CORE-02 | Users sign in with email/password and optional MFA (TOTP) | M |
| CORE-03 | SSO via SAML/OIDC for higher tiers | S |
| CORE-04 | Role-based access control with predefined and custom roles; permissions per module and action | M |
| CORE-05 | Multi-company and multi-branch within a tenant | S |
| CORE-06 | Every create/update/delete is written to an immutable audit log (who, what, when, before/after) | M |
| CORE-07 | In-app and email notifications | M |
| CORE-08 | Configurable base currency, fiscal year, time zone, locale, number and date formats | M |
| CORE-09 | CSV/Excel import with validation and error report; export of any list view | M |
| CORE-10 | Document attachments on records | S |
| CORE-11 | Approval workflows (configurable steps and thresholds) | S |
| CORE-12 | Global search across records | S |
| CORE-13 | Subscription and billing management for the tenant | M |

### 4.2 Finance & Accounting

| ID | Requirement | Priority |
|---|---|---|
| FIN-01 | Chart of accounts with templates per industry | M |
| FIN-02 | Manual journal entries; system rejects unbalanced entries | M |
| FIN-03 | Customer invoices and credit notes (generated from sales or standalone) | M |
| FIN-04 | Supplier bills and debit notes | M |
| FIN-05 | Record payments received and made; partial payments; allocation to invoices | M |
| FIN-06 | Tax rates and rules (VAT/GST/sales tax), tax reports | M |
| FIN-07 | Multi-currency transactions with exchange rates and realized/unrealized gains | S |
| FIN-08 | Bank accounts, bank statement import and reconciliation | S |
| FIN-09 | Financial reports: trial balance, P&L, balance sheet, cash flow, aged receivables/payables | M |
| FIN-10 | Period close and lock dates | M |
| FIN-11 | Budgets vs actuals | C |
| FIN-12 | Fixed assets and depreciation | C |

### 4.3 Inventory

| ID | Requirement | Priority |
|---|---|---|
| INV-01 | Products and services with SKUs, units of measure, categories, variants | M |
| INV-02 | Multiple warehouses and bin locations | M |
| INV-03 | Stock movements: receipts, deliveries, transfers, adjustments | M |
| INV-04 | Valuation methods: FIFO and weighted average; postings to finance | M |
| INV-05 | Reorder points and low-stock alerts | M |
| INV-06 | Batch/lot and serial number tracking | S |
| INV-07 | Stock counts (cycle counts) | S |
| INV-08 | Barcode scanning in the web app | C |

### 4.4 Sales

| ID | Requirement | Priority |
|---|---|---|
| SAL-01 | Customer records with contacts, addresses, credit limits, payment terms | M |
| SAL-02 | Quotations convertible to sales orders | M |
| SAL-03 | Sales orders reserve stock and create deliveries | M |
| SAL-04 | Invoicing from orders or deliveries | M |
| SAL-05 | Price lists and discounts | S |
| SAL-06 | Returns (RMA) | S |
| SAL-07 | Sales reports by customer, product, rep and period | M |

### 4.5 Purchasing (Phase 2)

| ID | Requirement | Priority |
|---|---|---|
| PUR-01 | Supplier records | M |
| PUR-02 | Purchase requisitions with approval | S |
| PUR-03 | Purchase orders; partial receipts | M |
| PUR-04 | Three-way match (PO, receipt, bill) | S |
| PUR-05 | Supplier price lists | C |

### 4.6 HR & Payroll (Phase 3)

| ID | Requirement | Priority |
|---|---|---|
| HR-01 | Employee records and org structure | M |
| HR-02 | Leave requests and approvals | M |
| HR-03 | Attendance / timesheets | S |
| HR-04 | Payroll runs with configurable earnings, deductions and tax; payslips | M |
| HR-05 | Employee self-service portal | S |

### 4.7 Reporting & Analytics

| ID | Requirement | Priority |
|---|---|---|
| REP-01 | Role-based home dashboards with key KPIs | M |
| REP-02 | Standard reports per module with filters and export (PDF, CSV, Excel) | M |
| REP-03 | Custom report builder | C |
| REP-04 | Scheduled report emails | S |

### 4.8 Integrations

| ID | Requirement | Priority |
|---|---|---|
| INT-01 | Public REST API covering all major entities (see [API design](../architecture/03-api-design.md)) | M |
| INT-02 | Webhooks for key events (invoice created, payment received, stock low, etc.) | M |
| INT-03 | API keys and OAuth2 client credentials per tenant | M |
| INT-04 | Payment gateway integration | S |
| INT-05 | E-commerce connectors | C |

## 5. Non-functional requirements

| ID | Category | Requirement |
|---|---|---|
| NFR-01 | Availability | 99.5% monthly uptime during MVP; 99.9% from Beta (excluding announced maintenance) |
| NFR-02 | Performance | p95 API response < 300 ms for standard reads; < 800 ms for writes; reports < 5 s for 1M rows |
| NFR-03 | Scalability | Support 5,000 tenants and 100 concurrent users per tenant without redesign |
| NFR-04 | Security | OWASP ASVS Level 2; encryption in transit (TLS 1.2+) and at rest (AES-256) |
| NFR-05 | Tenant isolation | No tenant can read or modify another tenant's data; verified by automated tests |
| NFR-06 | Data durability | RPO ≤ 15 minutes, RTO ≤ 4 hours |
| NFR-07 | Auditability | Financial records immutable after posting; corrections via reversing entries |
| NFR-08 | Accessibility | WCAG 2.1 AA |
| NFR-09 | Localization | UI translatable; currency, date, number formats per locale |
| NFR-10 | Browser support | Latest two versions of Chrome, Edge, Firefox, Safari |
| NFR-11 | Privacy | GDPR-style data subject rights: export and deletion per tenant |
| NFR-12 | Observability | Logs, metrics and traces for every request, correlated by request ID |

## 6. Success metrics

| Metric | Target |
|---|---|
| Activation (tenant posts first invoice within 7 days) | > 60% |
| Weekly active users per tenant | > 70% of seats |
| Support tickets per tenant per month | < 2 |
| NPS | > 40 |

## 7. Open questions

1. Launch geography and its tax/payroll requirements? **[TBD]**
2. Which payment gateway and banks to integrate first? **[TBD]**
3. Will we offer a free tier or only a trial? **[TBD]**

## 8. Change log

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-11-26 | Product | Initial draft |
