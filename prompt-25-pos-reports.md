## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Sales Reports** page following the universal 5-component reporting structure.

---

## §2. System Objective

Provide sales analytics — daily/weekly/monthly revenue, product performance, cashier performance, payment method breakdown — with tabular data, charts, and export.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: POS/Sales | **Active Page**: Reports
- **Sidebar**: Dashboard, Transaction, Transaction History, Returns, Customers, Pricing, Cashier Mgmt, **Reports**
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Available Reports

| Report | Description | Chart Type |
|--------|-------------|-----------|
| Sales Journal | Chronological list of all sales | Line chart (daily trend) |
| Product Performance | Sales by item — qty, revenue, margin | Bar chart |
| Cashier Performance | Sales by cashier — txns, revenue, avg | Horizontal bar |
| Payment Summary | Breakdown by method (Cash vs Credit) | Pie chart |

### Universal Reporting Structure
1. Report Selector tabs
2. Report Filters (Date Range, Cashier, Category, Payment)
3. Report Table
4. Report Chart
5. Export (CSV, PDF, Print)

---

## §6. UI Generation Scope

### Page Layout (Primary State: Sales Journal)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ [Sales Journal] [Products] [Cashier] [Payment]                 │
├─────────────────────────────────────────────────────────────────┤
│ [This Month ▾] [All Cashiers ▾]         [📊][📄][🖨️]         │
├────────────────────────────────┬────────────────────────────────┤
│ Report Table                   │ Report Chart                   │
│ Date│Txn #│Cashier│Total│Status│ Daily revenue line chart       │
│─────┼─────┼───────┼─────┼──────│                                │
│ rows...                        │                                │
├────────────────────────────────┴────────────────────────────────┤
│ Total Sales: ₱285,450.00  │  Transactions: 423               │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample: Sales Journal (6 rows)
| Date | Txn # | Cashier | Items | Total | Payment |
|------|-------|---------|-------|-------|---------|
| 30/03/2026 | SALE-0893 | Ana Reyes | 4 | ₱3,835.00 | Cash |
| 30/03/2026 | SALE-0892 | Ana Reyes | 3 | ₱1,280.00 | Cash |
| 30/03/2026 | SALE-0891 | Ana Reyes | 2 | ₱2,450.00 | Cash |
| 30/03/2026 | SALE-0890 | Carlos M. | 1 | ₱890.00 | Cash |
| 30/03/2026 | SALE-0889 | Carlos M. | 5 | ₱4,200.00 | Credit |
| 30/03/2026 | SALE-0888 | Carlos M. | 3 | ₱1,650.00 | Cash |

---

## §10. Do Not Assume

- Do NOT add Interpretation Panel — Accounting-only.
- Do NOT add auto-scheduled reports or email delivery.

---

## §11. Required Output Quality Standard

- Production-ready. ₱ values. Filipino names. Realistic chart.
- "Reports" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Tables: alternating rows. Report tabs: underline active.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
