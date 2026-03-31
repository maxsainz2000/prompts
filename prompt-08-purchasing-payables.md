## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Payables (Accounts Payable)** page — showing what the business owes to suppliers, with aging analysis and payment tracking.

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

Enable the Accountant/Manager to see all outstanding supplier payables at a glance through aging buckets, track individual payable records, and record payments against outstanding balances.

---

## §3. Application Context (Embedded)

### System Identity & Navigation
- **Application**: VISTA | **Module**: Purchasing | **Page**: Payables
- **Sidebar**: Dashboard, Suppliers, Purchase Requests, Purchase Orders, Receiving, **Payables**, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- **Colors**: Primary `#4A6741` | Sidebar `#2C3E2C` | Background `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Aging Summary Cards
5 cards showing payable amounts by age bucket:

| Bucket | Color | Example |
|--------|-------|---------|
| Current (not overdue) | Green `#E8F5E9` | ₱45,200.00 |
| 1–30 Days Overdue | Blue `#E3F2FD` | ₱28,500.00 |
| 31–60 Days | Amber `#FFF3E0` | ₱15,800.00 |
| 61–90 Days | Orange `#FFF8E1` | ₱8,200.00 |
| 90+ Days | Red `#FFEBEE` | ₱3,500.00 |

Total Outstanding shown below cards.

### Component: Payables List Table
**Columns:**

| Column | Sortable | Width |
|--------|----------|-------|
| Payable # | Yes | 120px |
| Supplier | Yes | 180px |
| PO/RCV Reference | No | 130px |
| Invoice Date | Yes | 100px |
| Due Date | Yes | 100px |
| Amount | Yes | 110px |
| Paid | No | 100px |
| Balance | Yes | 110px |
| Status | Yes | 90px |
| Actions | No | 80px |

- Status: Open (amber), Partially Paid (blue), Paid (green), Overdue (red).
- Actions: Record Payment, View Details.

### Component: Payables Filters
| Filter | Default |
|--------|---------|
| Status | All (Open, Partially Paid, Paid, Overdue) |
| Supplier | All |
| Date Range | Last 90 days |
| Aging Bucket | All |

### Component: Payment Form (Modal)
**Fields:**

| Field | Required |
|-------|----------|
| Payable Reference | Display (pre-filled) |
| Supplier | Display |
| Outstanding Balance | Display |
| Payment Amount | Yes (≤ outstanding) |
| Payment Date | Yes (default: today) |
| Payment Method | Yes (Cash, Check, Bank Transfer) |
| Reference # | No |

### Component: Payment History Timeline
- Chronological list of payments against a specific payable.
- Each entry: Date, Amount, Method, Reference, Recorded By.

---

## §5. Business Rules (Extracted)

- BR-P7: Payable amount = total received goods value, not PO value.
- BR-P8: Overpayment is not allowed. Payment ≤ outstanding balance.

---

## §6. UI Generation Scope

### Page Layout (Primary State: List with Aging Cards)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ [Current]  [1-30 Days]  [31-60 Days]  [61-90 Days]  [90+ Days]│
│  ₱45,200    ₱28,500      ₱15,800       ₱8,200       ₱3,500   │
│                    Total Outstanding: ₱101,200.00               │
├─────────────────────────────────────────────────────────────────┤
│ [All ▾] [All Suppliers ▾] [Last 90 Days ▾]       [Clear All]  │
├─────────────────────────────────────────────────────────────────┤
│ Payable# │Supplier│ Ref    │ Due Date │Amount  │Balance│Status │
│──────────┼────────┼────────┼──────────┼────────┼───────┼───────│
│ PAY-0023 │Agri-Pl.│PO-0048 │15/04/2026│₱45,200 │₱45,200│Open   │
│ PAY-0022 │Manila S│PO-0047 │10/04/2026│₱28,500 │₱15,000│Partial│
│ ...      │        │        │          │        │       │       │
└─────────────────────────────────────────────────────────────────┘
```

---

## §7. Layout Expectations

- **Aging Cards**: 5 cards in one row, top of content. Color escalation left (green) to right (red). ~80px tall.
- **Total Outstanding**: Centered below cards in bold.
- **Filters**: Below aging cards. **Table**: Below filters, fills remaining space.

---

## §8. Component Expectations

### Sample Payables (6 rows)
| Payable # | Supplier | Ref | Due Date | Amount | Paid | Balance | Status |
|-----------|----------|-----|----------|--------|------|---------|--------|
| PAY-2026-0023 | Agri-Plus | PO-2026-0048 | 15/04/2026 | ₱45,200.00 | ₱0.00 | ₱45,200.00 | Open |
| PAY-2026-0022 | Manila Seed | PO-2026-0047 | 10/04/2026 | ₱28,500.00 | ₱13,500.00 | ₱15,000.00 | Partial |
| PAY-2026-0021 | FarmTech | PO-2026-0046 | 28/03/2026 | ₱15,800.00 | ₱0.00 | ₱15,800.00 | Overdue |
| PAY-2026-0020 | Crop Care | PO-2026-0044 | 25/03/2026 | ₱8,900.00 | ₱8,900.00 | ₱0.00 | Paid |
| PAY-2026-0019 | Green Valley | PO-2026-0043 | 20/03/2026 | ₱33,400.00 | ₱25,200.00 | ₱8,200.00 | Partial |
| PAY-2026-0018 | BioGrow | PO-2026-0042 | 01/03/2026 | ₱19,750.00 | ₱16,250.00 | ₱3,500.00 | Overdue |

---

## §9. Interaction Expectations

- Clicking an aging card filters the table to that bucket.
- "Record Payment" opens the payment form modal.
- "View Details" opens a detail drawer with payment history timeline.

---

## §10. Do Not Assume

- Do NOT add bank reconciliation features.
- Do NOT add automated payment scheduling.
- Do NOT show supplier credit limits — that is not tracked in v1.

---

## §11. Required Output Quality Standard

- Production-ready. Aging color escalation visually clear. ₱ amounts. Filipino suppliers.
- "Payables" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Tables: alternating rows. Status badges per documented colors.
- Aging cards: green→blue→amber→orange→red color progression.

---

## §13. Fallback Behavior If Context Is Missing

- If aging card colors cannot differentiate, use border colors with white backgrounds.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
