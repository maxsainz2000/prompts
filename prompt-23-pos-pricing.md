## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Pricing** management page — where the Manager sets and updates selling prices, views cost/margin info, and tracks price history.

---

## §2. System Objective

Enable the Manager to review and update selling prices across the product catalog, compare prices against costs (margin analysis), apply bulk price changes, and maintain a price change audit trail.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: POS/Sales | **Active Page**: Pricing
- **Sidebar**: Dashboard, Transaction, Transaction History, Returns, Customers, **Pricing**, Cashier Mgmt, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Price List Table
**Columns:**

| Column | Width |
|--------|-------|
| Item Code | 90px |
| Item Name | 200px |
| Category | 120px |
| Cost (₱) | 100px |
| Current Price (₱, editable) | 100px |
| Margin % (calculated) | 80px |
| Last Changed | 100px |

- Inline editing: click the Price cell to edit directly.
- Margin = (Price - Cost) / Price × 100. Color: >20% green, 10-20% amber, <10% red.
- Pagination: 25/page. Sortable.

### Component: Price Filters
| Filter | Default |
|--------|---------|
| Category | All |
| Margin Range | All (All, <10%, 10-20%, >20%) |

### Component: Bulk Update Modal
- Select category or all items. Apply: +/- %, +/- fixed amount.
- Preview changes before confirm. Shows affected item count.

### Component: Price History Timeline
- Per-item: slide-in panel showing all price changes with: Date, Old Price, New Price, Changed By.

---

## §6. UI Generation Scope

### Page Layout (Primary State: Price List with inline editing)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ Pricing Management                         [Bulk Update]       │
│ [All Categories ▾] [All Margins ▾]                [Clear All]  │
├─────────────────────────────────────────────────────────────────┤
│ Code │ Item           │Category  │Cost   │Price  │Margin │Last │
│──────┼────────────────┼──────────┼───────┼───────┼───────┼─────│
│ 0042 │NPK 14-14-14    │Fert.     │₱780   │₱850   │ 8.2%  │28/03│
│ 0023 │Tomato Seeds     │Seeds     │₱38    │₱45    │15.6%  │15/03│
│ 0089 │Machete #5       │Tools     │₱320   │₱420   │23.8%  │01/03│
│ ...                                                            │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample Data (6 rows)
| Code | Item | Category | Cost | Price | Margin | Last Changed |
|------|------|----------|------|-------|--------|-------------|
| ITM-0042 | NPK 14-14-14 (50kg) | Fertilizers | ₱780.00 | ₱850.00 | 8.2% 🔴 | 28/03/2026 |
| ITM-0023 | Tomato Seeds (Diamante) | Seeds | ₱38.00 | ₱45.00 | 15.6% 🟡 | 15/03/2026 |
| ITM-0089 | Machete #5 HD | Farm Tools | ₱320.00 | ₱420.00 | 23.8% 🟢 | 01/03/2026 |
| ITM-0067 | Urea 46-0-0 (50kg) | Fertilizers | ₱650.00 | ₱720.00 | 9.7% 🔴 | 20/03/2026 |
| ITM-0156 | Knapsack Sprayer 16L | Equipment | ₱1,200.00 | ₱1,550.00 | 22.6% 🟢 | 10/02/2026 |
| ITM-0078 | Insecticide (Karate) 1L | Pesticides | ₱380.00 | ₱480.00 | 20.8% 🟢 | 05/03/2026 |

---

## §10. Do Not Assume

- Do NOT add volume-based pricing tiers.
- Do NOT add time-based promotions or sale pricing.
- Do NOT add competitor price comparison.

---

## §11. Required Output Quality Standard

- Production-ready. Inline edit cells clearly indicated. Margin color coding.
- "Pricing" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Margin: >20%=green, 10-20%=amber, <10%=red.
- Editable cells: subtle pencil icon or different background.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
