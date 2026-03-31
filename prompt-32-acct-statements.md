## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Generate the **Financial Statements** page — displaying the Income Statement (P&L), Balance Sheet, and Cash Flow Statement with the **MANDATORY Interpretation Panel**.

> **NON-NEGOTIABLE**: This page MUST include an Interpretation Panel providing insights, analytics, and visual graphs alongside the raw financial data.

## §1.5. Reference-Driven Shell Consistency (REQUIRED)

> **A canvas reference of the previously generated App Shell is attached to this generation request.**

This page screen renders *inside* the VISTA App Shell. The shell has already been visually designed and approved. Your task is to **preserve it exactly** and only generate new UI for the content area.

### Shell Preservation Rules — STRICT, NO EXCEPTIONS

**DO NOT** redesign, reinterpret, re-render, or stylistically deviate from any shell component shown in the reference canvas.

**MATCH EXACTLY** from the reference canvas:

| Shell Component | What to Match |
|----------------|---------------|
| **Top Bar** | Exact height (~48px), `#2C3E2C` background, logo placement (left), module tab layout (center), user/role display (right), tab active-state style |
| **Left Sidebar** | Exact width (~200px), `#2C3E2C` background, module name header, page item height (36px), left padding (12px), active item highlight color (`#4A6741`), inactive text color (`#E8EDE8`) |
| **Status Bar** | Exact height (~32px), `#2C3E2C` background, sync indicator (left), last sync text (center), version text (right) |

**ONLY generate new UI** for the **CONTENT AREA** — the `#FAFAF5` region to the right of the sidebar and above the status bar.

**Active state updates allowed (and required):**
- Set the module tab specified in §3 Navigation Context as active (highlighted).
- Set the sidebar page specified in §3 Navigation Context as active (highlighted with `#4A6741` background, white text).
- All other shell elements must be visually identical to the reference.

### Why This Matters
Shell inconsistency across screens breaks the illusion of a unified application. Every pixel of the shell that differs from the reference degrades the prototype quality. Treat the reference canvas as ground truth.

## §2. System Objective

Present the core financial statements in proper merchandising format with automated insights that help the Store Owner understand financial health without requiring accounting expertise.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: Accounting | **Active Page**: Financial Statements
- **Sidebar**: Dashboard, Chart of Accounts, Journal Entries, General Ledger, AP Ledger, AR Ledger, **Financial Statements**, Financial Reports, Period Close, Audit Trail
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online

### Accounting Reports Requirement (from `context-villon-vista-2026-03-28.md`)
> All accounting reports and financial statements include an additional **Interpretation Panel** that provides textual insights, contextual charts, and highlighted anomalies.

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Statement Selector
**Tabs:** Income Statement (P&L), Balance Sheet, Cash Flow Statement.

### Component: Period Selector
- Dropdown: Month, Quarter, Year. Current selection: March 2026.
- Comparison toggle: "Compare with previous period" checkbox.

### Component: Statement Display
#### Income Statement (Merchandising Format)
```
INCOME STATEMENT
Villon Farm Supply
For the Month Ended March 31, 2026

Sales Revenue                          ₱285,450.00
Less: Sales Returns & Allowances        -₱12,300.00
NET SALES                              ₱273,150.00

Cost of Goods Sold:
  Beginning Inventory    ₱1,180,000.00
  + Purchases             ₱193,900.00
  = Goods Available      ₱1,373,900.00
  - Ending Inventory     ₱1,245,600.00
COST OF GOODS SOLD                     ₱128,300.00

GROSS PROFIT                           ₱144,850.00
  Gross Margin:                         53.0%

Operating Expenses:
  Salaries & Wages         ₱35,000.00
  Utilities                 ₱8,500.00
  Rent                     ₱15,000.00
  Supplies                  ₱2,800.00
  Inventory Shrinkage        ₱856.00
TOTAL OPERATING EXPENSES                ₱62,156.00

NET INCOME                              ₱82,694.00
  Net Margin:                            30.3%
```

### Component: Interpretation Panel
**MANDATORY SECTIONS:**
1. **Key Insights** (3-5 bullet points):
   - "Gross margin of 53% is healthy for agricultural retail."
   - "Inventory shrinkage represents only 0.07% of COGS — well controlled."
   - "Net income improved 92% vs February (₱42,980 → ₱82,694)."
2. **Trend Chart**: Small line chart showing 3-month Net Income trend.
3. **Anomaly Flags**: Highlighted warnings if ratios are outside expected ranges.
4. **COGS Breakdown**: Mini donut chart showing COGS composition.

### Component: Export Actions
- PDF, Print.

---

## §6. UI Generation Scope

### Page Layout (Primary State: Income Statement with Interpretation Panel)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ [Income Statement] [Balance Sheet] [Cash Flow]                 │
│ Period: [March 2026 ▾]  ☐ Compare with February               │
├────────────────────────────────┬────────────────────────────────┤
│                                │ INTERPRETATION                 │
│ INCOME STATEMENT               │                                │
│ Villon Farm Supply             │ 📊 Key Insights               │
│ March 31, 2026                 │ • Gross margin 53% — healthy  │
│                                │ • Shrinkage 0.07% — excellent  │
│ Sales Revenue    ₱285,450      │ • Net income +92% vs Feb       │
│ - Returns         -₱12,300     │                                │
│ NET SALES        ₱273,150      │ 📈 Net Income Trend            │
│                                │ [Jan ₱38K │ Feb ₱43K │Mar ₱83K]│
│ COGS             ₱128,300      │                                │
│ GROSS PROFIT     ₱144,850      │ ⚠️ Anomalies                  │
│  (Margin: 53%)                 │ None detected this period.     │
│                                │                                │
│ Op. Expenses      ₱62,156      │ 🍩 COGS Breakdown             │
│ NET INCOME        ₱82,694      │ [Purchases 95% │ Shrinkage 5%]│
│  (Margin: 30.3%)               │                                │
├────────────────────────────────┴────────────────────────────────┤
│                                    [📄 PDF] [🖨️ Print]        │
└─────────────────────────────────────────────────────────────────┘
```

---

## §7. Layout Expectations

- **Left (55%)**: Financial statement in standard accounting format (indented line items).
- **Right (45%)**: Interpretation Panel with insights, charts, and anomaly flags.
- Statement uses monospaced numbers right-aligned for accounting readability.

---

## §10. Do Not Assume

- Do NOT omit the Interpretation Panel — it is non-negotiable.
- Do NOT use generic placeholder text for insights — use realistic analytical statements.
- Do NOT add budget vs actual columns (not in v1 scope).

---

## §11. Required Output Quality Standard

- Production-ready. Proper merchandising P&L format. ₱ values right-aligned.
- Interpretation Panel must contain at least 3 insights, 1 trend chart, and 1 composition chart.
- "Financial Statements" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Statement amounts: monospaced (JetBrains Mono). Insights: regular Inter.
- Bold for totals (NET SALES, GROSS PROFIT, NET INCOME). Subtotals indented.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
