## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Inventory Reports** page following the universal 5-component reporting structure.

---

## §2. System Objective

Provide analytical inventory reports — valuation, turnover, dead stock, and shrinkage — with tabular data, visual charts, and export functionality.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: Inventory | **Active Page**: Reports
- **Sidebar**: Dashboard, Item Master, Categories, Stock on Hand, Stock Adjustments, Stock Movements, Physical Count, **Reports**
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Available Reports

| Report | Description | Chart Type |
|--------|-------------|-----------|
| Inventory Valuation | Total stock value by category | Stacked bar |
| Stock Turnover | Item turnover rate (sold qty / avg stock) | Bar chart |
| Dead Stock | Items with no movement in 60+ days | Table only |
| Shrinkage Report | Adjustments summary (damage, theft, spoilage) | Pie chart |

### Filters (Common)
- Date Range, Category, Item

### Universal Reporting Structure (5 components)
1. Report Selector tabs
2. Report Filters
3. Report Table
4. Report Chart
5. Export Actions (CSV, PDF, Print)

---

## §6. UI Generation Scope

### Page Layout (Primary State: Inventory Valuation)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ [Valuation] [Turnover] [Dead Stock] [Shrinkage]                │
├─────────────────────────────────────────────────────────────────┤
│ [This Month ▾] [All Categories ▾]         [📊][📄][🖨️]       │
├────────────────────────────────┬────────────────────────────────┤
│ Report Table                   │ Report Chart                   │
│ Category │ Items │ Qty │ Value │ (Stacked bar by category)      │
│──────────┼───────┼─────┼───────│                                │
│ Fertilizers│ 12 │ 180 │₱140K │                                │
│ Seeds      │ 25 │ 450 │₱18K  │                                │
│ ...        │    │     │       │                                │
├────────────────────────────────┴────────────────────────────────┤
│ Total: ₱1,245,600.00                                           │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample: Inventory Valuation
| Category | Items | Total Qty | Total Value |
|----------|-------|-----------|-------------|
| Fertilizers | 12 | 180 | ₱140,400.00 |
| Seeds | 25 | 450 | ₱18,900.00 |
| Pesticides | 8 | 120 | ₱45,600.00 |
| Farm Tools | 15 | 85 | ₱27,200.00 |
| Equipment | 6 | 22 | ₱26,400.00 |
| Safety | 10 | 310 | ₱26,350.00 |
| Feeds | 5 | 200 | ₱960,750.00 |

---

## §10. Do Not Assume

- Do NOT add Interpretation Panel — that is Accounting-only.
- Do NOT add inventory forecasting.

---

## §11. Required Output Quality Standard

- Production-ready. ₱ values. Agricultural categories. Chart data realistic.
- "Reports" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Tables: alternating rows. Report tabs: underline active.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
