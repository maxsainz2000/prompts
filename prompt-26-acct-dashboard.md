## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Dashboard** for the **Accounting** module — "The Final Result" — providing a financial health snapshot with KPI cards, revenue/expense trends, AR/AP gauges, and period comparison.

---

## §2. System Objective

Give the Manager and Accountant an instant view of the entity's financial position: revenue vs expenses, cash flow health, outstanding receivables and payables, and period-over-period trends.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: Accounting | **Active Page**: Dashboard
- **Sidebar**: Dashboard, Chart of Accounts, Journal Entries, General Ledger, AP Ledger, AR Ledger, Financial Statements, Financial Reports, Period Close, Audit Trail
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Financial Snapshot Cards (5 cards)
| Metric | Icon | Example |
|--------|------|---------|
| Revenue (MTD) | 📈 | ₱285,450.00 |
| Expenses (MTD) | 📉 | ₱193,900.00 |
| Net Income | 💰 | ₱91,550.00 |
| Total AR | 🔵 | ₱45,200.00 |
| Total AP | 🔴 | ₱101,200.00 |

### Component: Revenue/Expense Chart
- Line chart: Monthly revenue vs expenses (last 6 months).
- Two lines: Revenue (green), Expenses (red). Shaded area = net margin.
- Position: Left ~55%, below cards.

### Component: Cash Flow Waterfall
- Waterfall chart: Opening Balance → +Revenue → -Expenses → -AP Payments → +AR Collections → Closing Balance.
- Position: Right ~45%, top.

### Component: AR/AP Gauge
- Two semi-circle gauges showing AR and AP as proportion of revenue.
- AR: blue scale. AP: red scale.
- Position: Right ~45%, bottom.

### Component: Period Comparison Table
- This Month vs Last Month: Revenue, Expenses, Net Income, AR, AP.
- Change % column with color (green=better, red=worse).
- Position: Full-width bottom section.

---

## §6. UI Generation Scope

### Page Layout

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ [Revenue MTD] [Expenses] [Net Income] [Total AR] [Total AP]   │
├────────────────────────────────┬────────────────────────────────┤
│                                │ Cash Flow Waterfall             │
│ Revenue vs Expenses Chart      │ (Opening → Revenue → Expenses  │
│ (6-month trend, 2 lines)       │  → AP → AR → Closing)         │
│                                ├────────────────────────────────┤
│                                │ AR/AP Gauges                    │
│                                │ [AR: ₱45K] [AP: ₱101K]        │
├────────────────────────────────┴────────────────────────────────┤
│ Period Comparison: March vs February                            │
│ Metric      │ This Month │ Last Month │ Change │ Trend          │
│ Revenue     │ ₱285,450   │ ₱258,200   │ +10.6% │ ↑ 🟢           │
│ Expenses    │ ₱193,900   │ ₱210,500   │ -7.9%  │ ↑ 🟢 (lower)   │
│ Net Income  │ ₱91,550    │ ₱47,700    │ +91.9% │ ↑ 🟢           │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Financial Snapshot (5 cards)
1. 📈 Revenue (MTD): **₱285,450.00** (↑ 10.6%)
2. 📉 Expenses (MTD): **₱193,900.00** (↓ 7.9%)
3. 💰 Net Income: **₱91,550.00** (↑ 91.9%)
4. 🔵 Total AR: **₱45,200.00** (↑ 5.2%)
5. 🔴 Total AP: **₱101,200.00** (↓ 8.1%)

### Period Comparison
| Metric | March 2026 | February 2026 | Change | Trend |
|--------|-----------|---------------|--------|-------|
| Revenue | ₱285,450 | ₱258,200 | +10.6% | 🟢 |
| Expenses | ₱193,900 | ₱210,500 | -7.9% | 🟢 |
| Net Income | ₱91,550 | ₱47,700 | +91.9% | 🟢 |
| AR Outstanding | ₱45,200 | ₱42,900 | +5.4% | 🔴 |
| AP Outstanding | ₱101,200 | ₱110,100 | -8.1% | 🟢 |

---

## §10. Do Not Assume

- Do NOT add budget vs actual tracking.
- Do NOT add tax filing indicators.
- Do NOT add bank account balances.

---

## §11. Required Output Quality Standard

- Production-ready. ₱ values. Charts with meaningful data. Financial terminology correct.
- "Accounting" module active, "Dashboard" active.

---

## §12. UI Consistency Rules

- Typography: Inter. Revenue=green, Expenses=red. Cards: white, 8px radius.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
