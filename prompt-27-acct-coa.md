## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Generate the **Chart of Accounts** page — a tree-table displaying the hierarchical account structure with expandable account groups.

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

Enable the Accountant to manage the account hierarchy: view all accounts organized by type (Assets, Liabilities, Equity, Revenue, Expenses), create/edit accounts, and see account balances.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: Accounting | **Active Page**: Chart of Accounts
- **Sidebar**: Dashboard, **Chart of Accounts**, Journal Entries, General Ledger, AP Ledger, AR Ledger, Financial Statements, Financial Reports, Period Close, Audit Trail
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: COA Tree-Table
**Columns:** Account #, Account Name, Type, Normal Balance (Debit/Credit), Current Balance, Status.

Account hierarchy:
```
▼ 1000 Assets
  ├── 1100 Current Assets
  │   ├── 1110 Cash on Hand
  │   ├── 1120 Cash in Bank
  │   ├── 1130 Accounts Receivable
  │   └── 1140 Merchandise Inventory
  └── 1200 Non-Current Assets
      └── 1210 Equipment
▼ 2000 Liabilities
  ├── 2100 Current Liabilities
  │   ├── 2110 Accounts Payable
  │   └── 2120 VAT Payable
▼ 3000 Equity
  └── 3100 Owner's Equity
▼ 4000 Revenue
  ├── 4100 Sales Revenue
  └── 4200 Sales Returns & Allowances
▼ 5000 Expenses
  ├── 5100 Cost of Goods Sold
  ├── 5200 Operating Expenses
  └── 5300 Inventory Shrinkage
```

### Component: COA Form
**Fields:** Account # (required), Account Name (required), Parent Account (dropdown), Account Type, Normal Balance, Description, Status.

### Component: COA Detail Panel
- Shows: Full account details, recent journal entries (last 10), running balance chart (30 days).

### Component: COA Search
- Search by account number or name. Filters tree to matching accounts.

---

## §6. UI Generation Scope

### Page Layout (Primary State: Tree-Table View)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ Chart of Accounts                           [+ New Account]    │
│ [🔍 Search accounts...]                                        │
├─────────────────────────────────────────────────────────────────┤
│ Account # │ Account Name         │ Type     │ Balance │ Status │
│───────────┼──────────────────────┼──────────┼─────────┼────────│
│ ▼ 1000    │ Assets               │ Asset    │₱1,345K  │ Active │
│   ▼ 1100  │   Current Assets     │ Asset    │₱1,320K  │ Active │
│     1110  │     Cash on Hand     │ Asset    │₱85,200  │ Active │
│     1120  │     Cash in Bank     │ Asset    │₱250,600 │ Active │
│     1130  │     Accounts Recv.   │ Asset    │₱45,200  │ Active │
│     1140  │     Merch. Inventory │ Asset    │₱1,245K  │ Active │
│   ▶ 1200  │   Non-Current        │ Asset    │₱25,000  │ Active │
│ ▼ 2000    │ Liabilities          │ Liab.    │₱121,200 │ Active │
│   ...                                                          │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample Accounts (top-level with 1 expanded)
| # | Account | Type | Balance | Status |
|---|---------|------|---------|--------|
| 1000 | Assets | Asset | ₱1,345,800.00 | Active |
| 1100 | Current Assets | Asset | ₱1,320,800.00 | Active |
| 1110 | Cash on Hand | Asset | ₱85,200.00 | Active |
| 1120 | Cash in Bank | Asset | ₱250,600.00 | Active |
| 1130 | Accounts Receivable | Asset | ₱45,200.00 | Active |
| 1140 | Merchandise Inventory | Asset | ₱1,245,600.00 | Active |
| 2000 | Liabilities | Liability | ₱121,200.00 | Active |
| 3000 | Equity | Equity | ₱1,133,050.00 | Active |
| 4000 | Revenue | Revenue | ₱285,450.00 | Active |
| 5000 | Expenses | Expense | ₱193,900.00 | Active |

---

## §10. Do Not Assume

- Do NOT add multi-currency accounts.
- Do NOT add account templates or import.
- Do NOT allow deletion of system accounts (AP, AR, Inventory, COGS).

---

## §11. Required Output Quality Standard

- Production-ready. Proper indentation shows hierarchy. ₱ balances.
- "Chart of Accounts" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Tree indentation: 24px per level. Account # monospaced.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
