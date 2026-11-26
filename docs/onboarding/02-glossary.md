# Glossary

> **Audience:** Everyone (engineering, product, marketing, support)
> Use these terms the same way in code, UI and conversation.

## Business and ERP terms

| Term | Meaning |
|---|---|
| **ERP** | Enterprise Resource Planning: software that runs a company's core processes in one system |
| **Tenant** | One customer organization using our SaaS. All its data is isolated from other tenants |
| **Company** | A legal entity inside a tenant. One tenant may have several companies |
| **Branch** | A location of a company (shop, office) |
| **Module** | A functional area: Finance, Inventory, Sales, Purchasing, HR, Reporting |
| **Order to cash (O2C)** | Quote → order → delivery → invoice → payment |
| **Procure to pay (P2P)** | Requisition → purchase order → receipt → bill → payment |
| **Master data** | Long-lived records: customers, suppliers, products, accounts |
| **Transaction / document** | Business events: invoices, orders, receipts, payments |
| **SKU** | Stock Keeping Unit: unique code for a product variant |
| **UoM** | Unit of Measure (piece, box, kg) |
| **Lot / batch** | A group of items produced or received together, tracked as one |
| **Reorder point** | Stock level that triggers a reorder alert |
| **Three-way match** | Checking that the purchase order, goods receipt and supplier bill agree |
| **RMA** | Return Merchandise Authorization: an approved customer return |

## Accounting terms

| Term | Meaning |
|---|---|
| **Chart of accounts (CoA)** | The list of all ledger accounts (assets, liabilities, equity, income, expenses) |
| **General ledger (GL)** | The complete record of all posted journal entries |
| **Double-entry** | Every transaction has equal debits and credits |
| **Journal entry** | A record of debits and credits that must balance |
| **Posting** | Making a document final, which creates its journal entry. Posted documents cannot be edited |
| **Reversal** | A new entry that cancels a posted one; used instead of editing |
| **Accounts receivable (AR)** | Money customers owe us |
| **Accounts payable (AP)** | Money we owe suppliers |
| **COGS** | Cost of goods sold |
| **FIFO** | First in, first out: stock valuation method |
| **Weighted average cost** | Stock valued at the average purchase cost |
| **Fiscal period** | An accounting period (usually a month); can be locked after close |
| **Trial balance** | List of all account balances; debits must equal credits |
| **P&L** | Profit and loss statement (income statement) |
| **Balance sheet** | Assets, liabilities and equity at a point in time |
| **Reconciliation** | Matching our records to an external source (e.g. bank statement) |
| **VAT / GST** | Value-added tax / goods and services tax |

## Technical terms

| Term | Meaning |
|---|---|
| **Modular monolith** | One deployable app split into strictly separated modules ([ADR-0001](../architecture/adr/0001-modular-monolith.md)) |
| **RLS** | Row-level security: PostgreSQL feature that filters rows per tenant ([ADR-0002](../architecture/adr/0002-multi-tenancy-strategy.md)) |
| **Outbox** | Table where events are stored in the same transaction as the change, then published ([ADR-0004](../architecture/adr/0004-event-driven-integration-with-outbox.md)) |
| **Domain event** | A record that something happened in a module, e.g. `sales.InvoicePosted` |
| **Use case** | An application-level operation, e.g. "post invoice" |
| **RBAC** | Role-based access control |
| **ADR** | Architecture Decision Record |
| **SLO / SLA** | Service level objective (internal target) / agreement (contractual promise) |
| **RPO / RTO** | Recovery point objective (max data loss) / recovery time objective (max downtime) |
| **Feature flag** | Switch to turn a feature on per tenant or environment |
