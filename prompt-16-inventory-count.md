## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Physical Count** page — where staff enters actual warehouse/shelf counts to reconcile against system quantities, identifying discrepancies.

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

Enable periodic inventory verification by comparing physical counts to system records, identifying variances, and generating reconciliation adjustments.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: Inventory | **Active Page**: Physical Count
- **Sidebar**: Dashboard, Item Master, Categories, Stock on Hand, Stock Adjustments, Stock Movements, **Physical Count**, Reports
- **User**: Juan Dela Cruz / Purchasing Clerk | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Count Session Header
**Fields:**

| Field | Required |
|-------|----------|
| Count # (auto: CNT-YYYY-NNNN) | Read-only |
| Count Date (default: today) | Yes |
| Category Filter (dropdown — count all or specific) | No |
| Counted By | Auto (current user) |
| Status | Draft / Submitted / Reconciled |
| Notes | No |

### Component: Count Entry Table
**Columns:**

| Column | Width |
|--------|-------|
| Item Code | 90px |
| Item Name | 200px |
| System Qty (read-only) | 90px |
| Counted Qty (editable) | 90px |
| Variance (calculated) | 90px |
| Variance % | 70px |
| Status Icon | 40px |

- Variance = Counted - System. Status: ✅ Match, ⚠️ Under, ❗ Over.
- Pre-loaded with all items (or filtered by category). Counted Qty starts empty.

### Component: Reconciliation Summary
- Total items counted, matches, unders, overs.
- Total value of variance (₱).
- "Generate Adjustments" button: creates Stock Adjustment records for all variances.

### Component: Count List Table
- Past count sessions: CNT #, Date, Counted By, Items, Matches, Variances, Status.

---

## §5. Business Rules (Extracted)

- Count sessions create Stock Adjustments on reconciliation.
- System Qty is frozen at count creation time (snapshot, not live).
- Variance tracking for audit trail.

---

## §6. UI Generation Scope

### Page Layout (Primary State: Active Count Entry)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ Physical Count Session                     [CNT-2026-0004]     │
│ Date: 30/03/2026 │ Category: All │ By: Juan │ Status: Draft   │
├─────────────────────────────────────────────────────────────────┤
│ Code  │ Item            │ System │ Counted │ Var  │ Var% │ St  │
│───────┼─────────────────┼────────┼─────────┼──────┼──────┼─────│
│ 0042  │ NPK 14-14-14    │   23   │   22    │  -1  │-4.3% │ ⚠️ │
│ 0023  │ Tomato Seeds     │    2   │    2    │   0  │ 0%   │ ✅ │
│ 0067  │ Urea 46-0-0     │    5   │    5    │   0  │ 0%   │ ✅ │
│ 0089  │ Machete #5       │    0   │    0    │   0  │ 0%   │ ✅ │
│ 0034  │ Ampalaya Seeds   │   45   │   43    │  -2  │-4.4% │ ⚠️ │
│ 0078  │ Insecticide 1L   │   28   │   30    │  +2  │+7.1% │ ❗ │
├─────────────────────────────────────────────────────────────────┤
│ Summary: 6 counted │ 3 match │ 2 under │ 1 over               │
│ Total Variance Value: -₱1,580.00                               │
├─────────────────────────────────────────────────────────────────┤
│ [Cancel]              [Save Draft] [Submit] [Generate Adj.]    │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample Data (6 items)
| Code | Item | System | Counted | Variance | Var% | Status |
|------|------|--------|---------|----------|------|--------|
| ITM-0042 | NPK 14-14-14 (50kg) | 23 | 22 | -1 | -4.3% | ⚠️ Under |
| ITM-0023 | Tomato Seeds (Diamante) | 2 | 2 | 0 | 0% | ✅ Match |
| ITM-0067 | Urea 46-0-0 (50kg) | 5 | 5 | 0 | 0% | ✅ Match |
| ITM-0089 | Machete #5 | 0 | 0 | 0 | 0% | ✅ Match |
| ITM-0034 | Ampalaya Seeds | 45 | 43 | -2 | -4.4% | ⚠️ Under |
| ITM-0078 | Insecticide (Karate) 1L | 28 | 30 | +2 | +7.1% | ❗ Over |

---

## §9. Interaction Expectations

- Tab through "Counted Qty" column sequentially for rapid data entry.
- Variance auto-calculates. Color-coded in real-time.
- "Generate Adjustments": creates ADJ records for all non-zero variances.

---

## §10. Do Not Assume

- Do NOT add barcode scanner integration in UI.
- Do NOT add partial count (must count all items in scope).

---

## §11. Required Output Quality Standard

- Production-ready. Variance color coding clear. ₱ variance value shown.
- "Physical Count" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Match=green, Under=amber, Over=red.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
