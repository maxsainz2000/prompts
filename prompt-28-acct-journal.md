## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Generate the **Journal Entries** form view — the core accounting data entry page with debit/credit line items and a real-time balance indicator.

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

Enable the Accountant to create, edit, and approve journal entries — the fundamental accounting records. Every financial transaction ultimately becomes a journal entry with balanced debits and credits.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: Accounting | **Active Page**: Journal Entries
- **Sidebar**: Dashboard, Chart of Accounts, **Journal Entries**, General Ledger, AP Ledger, AR Ledger, Financial Statements, Financial Reports, Period Close, Audit Trail
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: JE Form
**Fields:** JE # (auto: JE-YYYY-NNNN), Date, Description (required), Source (Manual/System-Generated), Reference, Notes.

### Component: Debit/Credit Line Items
**Columns:**

| Column | Width |
|--------|-------|
| Account (searchable from COA) | 200px |
| Description | 150px |
| Debit (₱) | 100px |
| Credit (₱) | 100px |
| Remove | 40px |

- Each line has either debit OR credit filled (not both).
- Tab navigation: Account → Description → Debit → Credit → next row.
- Add row button.

### Component: Balance Indicator
- Real-time bar showing: Total Debits vs Total Credits.
- **Balanced** (green bar, ✅): Debits = Credits. Post allowed.
- **Unbalanced** (red bar, ❌): Debits ≠ Credits. Difference shown. Post blocked.
- Position: Below line items, above action bar.

### Component: JE Approval Panel
- Approve/Reject. Mandatory reason on reject.
- System-generated JEs are auto-approved. Manual JEs require approval.

### Component: JE List Table
**Columns:** JE #, Date, Description, Source, Total, Status, Actions.

### Component: JE Status Badge
- Draft, Pending, Approved, Rejected, Posted.

---

## §5. Business Rules (Extracted)

- Debits must equal Credits (balanced entry).
- Posted entries are immutable — corrections require reversing entries.
- System-generated entries (from Sales, Receiving, Adjustments) are auto-posted.
- Manual entries require approval before posting.

---

## §6. UI Generation Scope

### Page Layout (Primary State: JE Form — Create)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ New Journal Entry                           [JE-2026-0145]     │
├───────────────────────────┬─────────────────────────────────────┤
│ Date: 30/03/2026          │ Source: Manual                      │
│ Description: [Record      │ Reference: [ADJ-2026-0008]         │
│  spoilage adjustment]     │                                     │
├───────────────────────────┴─────────────────────────────────────┤
│ JOURNAL LINES                                       [+ Add Row] │
│ Account            │ Description    │ Debit    │ Credit         │
│────────────────────┼────────────────┼──────────┼────────────────│
│ 5300 Inv. Shrinkage│ NPK spoilage   │₱780.00  │               │
│ 5300 Inv. Shrinkage│ Tomato spoilage│₱76.00   │               │
│ 1140 Merch. Inv.   │ Stock write-off│          │₱856.00        │
├─────────────────────────────────────────────────────────────────┤
│ ┃████████████████████████████████████████████████████┃  ✅      │
│ Total Debits: ₱856.00  │  Total Credits: ₱856.00  │ BALANCED  │
├─────────────────────────────────────────────────────────────────┤
│ [Cancel]                       [Save Draft] [Submit for Appr.] │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample JE
- JE #: JE-2026-0145 | Date: 30/03/2026 | Source: Manual
- Description: "Record spoilage adjustment from ADJ-2026-0008"

### Line Items
| Account | Description | Debit | Credit |
|---------|-------------|-------|--------|
| 5300 Inventory Shrinkage | NPK Fertilizer spoilage | ₱780.00 | — |
| 5300 Inventory Shrinkage | Tomato Seeds spoilage | ₱76.00 | — |
| 1140 Merchandise Inventory | Stock write-off | — | ₱856.00 |

### Balance: ₱856.00 = ₱856.00 ✅ BALANCED (green bar)

---

## §9. Interaction Expectations

- Account field: searchable dropdown from COA. Tab-navigable entire form.
- Balance indicator updates in real-time as amounts change.
- Unbalanced state blocks the Submit button (disabled with tooltip).

---

## §10. Do Not Assume

- Do NOT add multi-currency journal entries.
- Do NOT add recurring/template entries.
- Do NOT add file attachments to journal entries.

---

## §11. Required Output Quality Standard

- Production-ready. Balanced indicator is the signature UI element.
- Account numbers and names from the COA sample. ₱ values.
- "Journal Entries" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Balanced=green bar, Unbalanced=red bar. Forms: 2-column header.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
