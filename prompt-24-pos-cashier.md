## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Cashier Management** page — where cashiers open/close shifts and managers review shift summaries, cash counts, and variance reports.

---

## §2. System Objective

Manage the cashier shift lifecycle: open a shift (set opening cash), record transactions during the shift, close the shift (denomination cash count), calculate variance, and produce shift summary reports.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: POS/Sales | **Active Page**: Cashier Mgmt
- **Sidebar**: Dashboard, Transaction, Transaction History, Returns, Customers, Pricing, **Cashier Mgmt**, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Shift Open/Close Form
**Open Shift:** Cashier Name (auto), Date/Time (auto), Opening Cash (₱, required).
**Close Shift:** Denomination count table, System Total, Counted Total, Variance.

### Component: Denomination Cash Count Table
**Philippine denominations:**

| Denomination | Count | Subtotal |
|-------------|-------|----------|
| ₱1,000 | [input] | calculated |
| ₱500 | [input] | calculated |
| ₱200 | [input] | calculated |
| ₱100 | [input] | calculated |
| ₱50 | [input] | calculated |
| ₱20 | [input] | calculated |
| ₱10 | [input] | calculated |
| ₱5 | [input] | calculated |
| ₱1 | [input] | calculated |
| **Total** | | **calculated** |

### Component: Shift Summary
- Shows: Opening Cash, Total Sales (cash), Total Returns (cash), Expected Cash (Opening + Sales - Returns), Counted Cash, Variance.
- Variance: Exact=green, Over=blue, Under=red.

### Component: Shift History Table
- Past shifts: Cashier, Date, Open Time, Close Time, Sales, Counted, Variance, Status.

---

## §6. UI Generation Scope

### Page Layout (Primary State: Shift Close — Cash Count)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ Close Shift — Ana Reyes                    Shift: AM 30/03/2026│
├───────────────────────────┬─────────────────────────────────────┤
│ DENOMINATION COUNT        │ SHIFT SUMMARY                       │
│                           │                                     │
│ ₱1,000 × [3 ] = ₱3,000   │ Opening Cash:    ₱5,000.00         │
│ ₱500   × [5 ] = ₱2,500   │ + Cash Sales:    ₱18,200.00        │
│ ₱200   × [2 ] = ₱400     │ - Cash Returns:  -₱1,200.00        │
│ ₱100   × [8 ] = ₱800     │ = Expected:      ₱22,000.00        │
│ ₱50    × [4 ] = ₱200     │                                     │
│ ₱20    × [6 ] = ₱120     │ Counted Cash:    ₱21,970.00        │
│ ₱10    × [3 ] = ₱30      │                                     │
│ ₱5     × [2 ] = ₱10      │ Variance:        -₱30.00  ⚠️       │
│ ₱1     × [10] = ₱10      │ (Under by ₱30.00)                  │
│─────────────────────────  │                                     │
│ TOTAL:         ₱7,070     │                                     │
│ (+ Bills/Coins in drawer) │                                     │
├───────────────────────────┴─────────────────────────────────────┤
│ [Cancel]                                        [Close Shift]   │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample Shift Close
- Cashier: Ana Reyes | Shift: AM | Date: 30/03/2026
- Opening: ₱5,000 | Sales: ₱18,200 | Returns: ₱1,200 | Expected: ₱22,000
- Counted: ₱21,970 | **Variance: -₱30.00** (⚠️ Under)

---

## §10. Do Not Assume

- Do NOT add safe/bank deposit tracking.
- Do NOT add multiple cash drawers.
- Do NOT add petty cash management.

---

## §11. Required Output Quality Standard

- Production-ready. Philippine denominations correct. Variance color-coded.
- "Cashier Mgmt" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Variance: Exact=green, Over=blue, Under=red.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
