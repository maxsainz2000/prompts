## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Stock Adjustments** form view — where staff records non-transactional stock changes (damage, theft, spoilage, correction) that require approval.

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

Enable staff to record and justify corrections to stock quantities outside the normal Purchasing (in) and Sales (out) flows, with mandatory reason tracking and approval workflow for audit integrity.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: Inventory | **Active Page**: Stock Adjustments
- **Sidebar**: Dashboard, Item Master, Categories, Stock on Hand, **Stock Adjustments**, Stock Movements, Physical Count, Reports
- **User**: Juan Dela Cruz / Purchasing Clerk | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Adjustment Form
**Fields:**

| Field | Required |
|-------|----------|
| Adjustment # (auto: ADJ-YYYY-NNNN) | Read-only |
| Date (default: today) | Yes |
| Direction (Increase ↑ / Decrease ↓) | Yes (toggle) |
| Reason (dropdown: Damage, Theft, Spoilage, Correction, Other) | Yes |
| Reason Details | Yes (if "Other") |
| Notes | No |
| Adjusted By | Auto (current user) |

Below: Adjustment Line Items. Bottom: Save Draft, Submit for Approval.

### Component: Adjustment Line Items
**Columns:**

| Column | Width |
|--------|-------|
| Item (searchable) | 200px |
| Current Qty (read-only) | 80px |
| Adjustment Qty | 80px |
| New Qty (calculated) | 80px |
| Remove | 40px |

- New Qty = Current Qty ± Adjustment Qty (based on direction).
- New Qty cannot be negative.

### Component: Adjustment Approval Panel
- Approve/Reject. Mandatory reason on reject.
- On approve: stock quantities updated + `InventoryAdjusted` event → Accounting.

### Component: Adjustment List Table
**Columns:** ADJ #, Date, Direction, Reason, Items, Total Qty, Status (Draft/Pending/Approved/Rejected, Actions.

### Component: Direction Toggle
- Visual toggle: ↑ Increase (green) / ↓ Decrease (red).
- Affects all line items — single direction per adjustment.

---

## §5. Business Rules (Extracted)

- Stock Adjustments require approval (same rules as PR/PO).
- Approved adjustments trigger `InventoryAdjusted` event → Accounting records shrinkage/loss.
- Reason is mandatory for audit trail.
- New Qty cannot be negative.

---

## §6. UI Generation Scope

### Page Layout (Primary State: Adjustment Form — Create)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ New Stock Adjustment                       [ADJ-2026-0008]     │
├───────────────────────────┬─────────────────────────────────────┤
│ Date: 30/03/2026          │ Direction: [↓ Decrease]  (toggle)  │
│ Reason: [Spoilage ▾]     │ Adjusted By: Juan Dela Cruz        │
│ Notes: [...]              │                                     │
├───────────────────────────┴─────────────────────────────────────┤
│ ADJUSTMENT LINES                                   [+ Add Row]  │
│ Item            │ Current Qty │ Adj Qty │ New Qty │ Remove      │
│─────────────────┼─────────────┼─────────┼─────────┼─────────────│
│ NPK 14-14-14    │     3       │    1    │    2    │    🗑️       │
│ Tomato Seeds    │     2       │    2    │    0    │    🗑️       │
├─────────────────────────────────────────────────────────────────┤
│ [Cancel]                        [Save Draft] [Submit for Appr.] │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample Data
- ADJ #: ADJ-2026-0008
- Direction: ↓ Decrease (red toggle)
- Reason: Spoilage
- Adjusted By: Juan Dela Cruz

### Line Items
| Item | Current | Adj Qty | New Qty |
|------|---------|---------|---------|
| NPK 14-14-14 (50kg) | 3 | 1 | 2 |
| Tomato Seeds (Diamante F1) | 2 | 2 | 0 |

---

## §9. Interaction Expectations

- Direction toggle: switches between ↑/↓ and changes color (green/red).
- Item search: debounced autocomplete from Item Master.
- New Qty auto-calculates. Negative result shows error.

---

## §10. Do Not Assume

- Do NOT add cost impact calculation on the form (that goes to Accounting).
- Do NOT add image/photo evidence upload.
- Do NOT allow mixed directions in one adjustment.

---

## §11. Required Output Quality Standard

- Production-ready form. Agricultural items. Direction toggle clearly visible.
- "Stock Adjustments" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Forms: 2-column. Increase toggle: green. Decrease: red.

---

## §13. Fallback Behavior If Context Is Missing

- If toggle cannot render, use radio buttons "Increase / Decrease".

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
