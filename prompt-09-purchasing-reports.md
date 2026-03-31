## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Purchase Reports** page following the universal 5-component reporting structure defined across all VISTA modules.

---

## §2. System Objective

Provide the Manager and Accountant with analytical purchase reports — spending patterns, supplier analysis, AP aging, and discount tracking — with both tabular data and visual charts. Export to CSV/PDF/Print.

---

## §3. Application Context (Embedded)

### System Identity & Navigation
- **Application**: VISTA | **Module**: Purchasing | **Page**: Reports
- **Sidebar**: Dashboard, Suppliers, Purchase Requests, Purchase Orders, Receiving, Payables, **Reports**
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- **Colors**: Primary `#4A6741` | Sidebar `#2C3E2C` | Background `#FAFAF5`

### Universal Reporting Standard (from `modules/spec.md` §9)
All reporting pages follow a uniform 5-component structure:
1. **Report Selector** — Tabs to choose which report to view
2. **Report Filters** — Date range, category, status filters
3. **Report Table** — Tabular data with sortable columns
4. **Report Chart** — Visual representation (bar, line, pie)
5. **Export Actions** — CSV, PDF, Print

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Report Selector
**Available Reports:**

| Report | Description |
|--------|-------------|
| Purchases Journal | Chronological list of all purchases from suppliers |
| AP Aging Report | Outstanding payables by age (30/60/90 days) |
| Purchase Discounts Report | Savings from early payment terms |
| Supplier Spend Analysis | Spending by supplier over time |

### Component: Report Filters
- Common: Date Range (default: This Month)
- Purchases Journal: Supplier, Status
- AP Aging: Supplier, Aging Bucket
- Discounts: Supplier, Discount Type
- Supplier Spend: Top N suppliers

### Component: Report Table
- **Purchases Journal**: Date, PO #, Supplier, Items, Total, Status
- **AP Aging**: Supplier, Current, 1-30, 31-60, 61-90, 90+, Total
- **Discounts**: PO #, Supplier, Gross, Discount, Net, Discount %
- **Supplier Spend**: Supplier, Orders, Total Spend, Avg Order, Last Order

Features: Sortable, summary row at bottom, pagination. Read-only.

### Component: Report Chart
| Report | Chart Type |
|--------|-----------|
| Purchases Journal | Line chart — monthly purchase trend |
| AP Aging | Stacked bar — aging distribution |
| Discounts | Bar chart — savings by supplier |
| Supplier Spend | Pie chart — spend by supplier (top 10) |

### Component: Report Export Actions
- Export CSV (📊), Export PDF (📄), Print (🖨️)
- WYSIWYG export of current filtered data.

---

## §5. Business Rules (Extracted)

- Reports are read-only — no edit actions.
- All monetary values in ₱ with 2 decimal places.
- Date ranges default to current month.
- AP Aging uses the same 5-bucket structure as the Payables page.

---

## §6. UI Generation Scope

### Page Layout (Primary State: Purchases Journal)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ [Purchases Journal] [AP Aging] [Discounts] [Supplier Spend]   │  ← Tabs
├─────────────────────────────────────────────────────────────────┤
│ [This Month ▾] [All Suppliers ▾]    [📊 CSV] [📄 PDF] [🖨️]   │  ← Filters + Export
├────────────────────────────────┬────────────────────────────────┤
│                                │                                │
│  Report Table                  │  Report Chart                  │
│  (Purchases Journal data)      │  (Monthly purchase trend)      │
│                                │                                │
│  6-8 rows with summary row     │  Line chart with ₱ amounts     │
│                                │                                │
├────────────────────────────────┴────────────────────────────────┤
│ Summary: Total Purchases: ₱285,450.00  │  Avg Order: ₱14,272   │
└─────────────────────────────────────────────────────────────────┘
```

---

## §7. Layout Expectations

- **Tabs**: Top of content. Active tab underlined with primary color.
- **Filters + Export**: Single row below tabs. Filters left, export buttons right.
- **Table + Chart**: Side-by-side, 55% table / 45% chart. Or stacked (table top, chart bottom).
- **Summary Row**: Bottom of table with totals.

---

## §8. Component Expectations

### Sample: Purchases Journal (6 rows)
| Date | PO # | Supplier | Items | Total | Status |
|------|------|----------|-------|-------|--------|
| 28/03/2026 | PO-2026-0048 | Agri-Plus | 3 | ₱45,200.00 | Pending |
| 27/03/2026 | PO-2026-0047 | Manila Seed | 5 | ₱28,500.00 | Approved |
| 26/03/2026 | PO-2026-0046 | FarmTech | 2 | ₱15,800.00 | Received |
| 25/03/2026 | PO-2026-0045 | Green Valley | 8 | ₱62,100.00 | Received |
| 24/03/2026 | PO-2026-0044 | Crop Care | 4 | ₱8,900.00 | Approved |
| 22/03/2026 | PO-2026-0043 | Agri-Plus | 6 | ₱33,400.00 | Received |

**Summary**: Total: ₱193,900.00 | Count: 6 | Avg: ₱32,316.67

### Chart: Monthly trend line (Jan–Mar 2026)
- Jan: ₱185,000 | Feb: ₱210,500 | Mar: ₱285,450

---

## §9. Interaction Expectations

- Tab click switches report view. Filters update. Table and chart reload.
- Export buttons export current filtered data.
- Table columns sortable via header click.

---

## §10. Do Not Assume

- Do NOT add an Interpretation Panel — that is Accounting-module only.
- Do NOT add drill-down from chart to table.
- Do NOT add scheduled/automated reports.

---

## §11. Required Output Quality Standard

- Production-ready report page. ₱ values. Agricultural suppliers. Realistic chart data.
- "Reports" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Tables: alternating rows, `#F5F5EE` headers. Buttons: Primary `#4A6741`.

---

## §13. Fallback Behavior If Context Is Missing

- If chart cannot render, show table only at full width.
- If a report type has no data, show "No data for the selected period."

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
