## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Receiving (Goods Receipt) form view** — the page where staff records incoming merchandise deliveries against approved Purchase Orders, with variance tracking.

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

Enable the Purchasing Clerk to accurately record goods received from suppliers, compare received quantities against ordered quantities, and trigger inventory stock increases and accounts payable creation.

---

## §3. Application Context (Embedded)

### System Identity
- **Application**: VISTA — Villon's Integrated Supply and Trade Application
- **Entity**: Villon Farm Supply (agricultural retail, MSME)
- **Platform**: Windows desktop (WPF) — 1366×768 minimum

### Navigation Context
- **Active Module**: Purchasing | **Active Page**: Receiving
- **Sidebar Pages**: Dashboard, Suppliers, Purchase Requests, Purchase Orders, **Receiving**, Payables, Reports
- **User**: Juan Dela Cruz / Purchasing Clerk | **Sync**: 🟢 Online

### Color Palette
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`
- Variance: Exact=`#E8F5E9`/green, Under=`#FFF3E0`/amber, Over=`#FFEBEE`/red

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Receiving Form
**Fields:**

| Field | Required |
|-------|----------|
| Receiving # (auto: RCV-YYYY-NNNN) | Read-only |
| PO Reference (searchable dropdown) | Yes |
| Delivery Date (default: today) | Yes |
| Delivery Note # (supplier's document) | No |
| Received By (auto: current user) | Read-only |
| Notes | No |

- On PO selection: supplier name, PO date, PO items auto-populate into line items.
- Only Approved and Partially Received POs appear in the dropdown.

### Component: Receiving Line Items
**Columns:**

| Column | Width |
|--------|-------|
| Item | 200px |
| Ordered Qty | 80px |
| Previously Received | 80px |
| Remaining | 80px |
| Received Now (editable) | 100px |
| Variance (calculated) | 80px |
| Status Icon | 40px |

- Ordered Qty, Previously Received, Remaining are read-only (from PO data).
- Received Now is editable. Variance = Received Now - Remaining.
- Variance status icon: ✅ (exact), ⚠️ (under), ❌ (over — blocked by BR-P4).

### Component: Variance Indicator
**Color coding:**

| Variance | Color | Icon | Meaning |
|----------|-------|------|---------|
| 0 (Exact) | Green | ✅ | Received exactly what was remaining |
| < 0 (Under) | Amber | ⚠️ | Received less — partial delivery |
| > 0 (Over) | Red | ❌ | Cannot exceed remaining — blocked |

### Component: Receiving Confirmation Modal
- Title: "Confirm Goods Receipt"
- Summary: X items, total received, variance summary.
- Warning if any under-deliveries: "X items have partial delivery."
- "Confirm Receipt" button (primary) + "Cancel" button.
- On confirm: triggers `GoodsReceived` event → stock increase + AP creation.

### Component: Receiving List Table
**Columns:** RCV #, PO #, Supplier, Date, Received By, Status (Complete/Partial), Actions.

---

## §5. Business Rules (Extracted)

- BR-P4: Receiving quantity cannot exceed PO remaining quantity.
- BR-P5: Receiving confirmation triggers stock increase in Inventory and AP creation in Accounting.
- BR-P9: RCV-YYYY-NNNN format.
- Partial receiving: single PO may be received in multiple shipments.

---

## §6. UI Generation Scope

### Page Layout (Primary State: Receiving Form)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ New Goods Receipt                        [RCV-2026-0024]       │
├───────────────────────────┬─────────────────────────────────────┤
│ PO Reference: [▾ PO-2026-│ Delivery Date: 30/03/2026           │
│   0047 - Manila Seed Corp]│ Delivery Note #: [DN-88421]        │
│ Supplier: Manila Seed Corp│ Received By: Juan Dela Cruz         │
├───────────────────────────┴─────────────────────────────────────┤
│ RECEIVING LINE ITEMS                                            │
│ Item          │Ordered│Prev│Remain│Recv Now│Variance│Status    │
│───────────────┼───────┼────┼──────┼────────┼────────┼──────────│
│ NPK 14-14-14  │  20   │  0 │  20  │  20    │   0    │ ✅ Exact │
│ Urea 46-0-0   │  15   │  0 │  15  │  12    │  -3    │ ⚠️ Under│
│ Tomato Seeds   │ 100   │  0 │ 100  │ 100    │   0    │ ✅ Exact │
├─────────────────────────────────────────────────────────────────┤
│ Total Items: 3  │ Full: 2  │ Partial: 1  │ Over: 0             │
├─────────────────────────────────────────────────────────────────┤
│ [Cancel]                                    [Confirm Receipt]   │
└─────────────────────────────────────────────────────────────────┘
```

---

## §7. Layout Expectations

- Form header: 2-column. PO reference and supplier left. Dates and receiver right.
- Line items: Full-width table. Variance column uses colored backgrounds.
- Summary row: Below line items showing totals by category.
- Action bar: bottom-pinned.

---

## §8. Component Expectations

### Sample Data
- RCV #: RCV-2026-0024
- PO: PO-2026-0047 (Manila Seed Corp)
- Date: 30/03/2026
- Receiver: Juan Dela Cruz

### Sample Line Items
| Item | Ordered | Prev | Remaining | Received | Variance | Status |
|------|---------|------|-----------|----------|----------|--------|
| NPK Fertilizer 14-14-14 (50kg) | 20 | 0 | 20 | 20 | 0 | ✅ Exact |
| Urea Fertilizer 46-0-0 (50kg) | 15 | 0 | 15 | 12 | -3 | ⚠️ Under |
| Tomato Seeds (Diamante F1) | 100 | 0 | 100 | 100 | 0 | ✅ Exact |

---

## §9. Interaction Expectations

- PO dropdown search filters by PO # or supplier name.
- "Received Now" column: Tab-navigable. Only column that is editable.
- Variance auto-calculates as user types in "Received Now".
- `Ctrl+S` saves. `Enter` on "Confirm Receipt" triggers confirmation modal.

---

## §10. Do Not Assume

- Do NOT allow received quantity greater than remaining (BR-P4 — hard block, not warning).
- Do NOT add quality inspection fields — not in v1 scope.
- Do NOT add barcode scanning interface — manual entry only.
- Do NOT show pricing in the receiving form — this is quantity tracking only.

---

## §11. Required Output Quality Standard

- Production-ready form. Agricultural products. Filipino names. Variance color coding clearly visible.
- "Receiving" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Forms: 2-column. Tables: alternating rows. Primary button: `#4A6741`.

---

## §13. Fallback Behavior If Context Is Missing

- If variance icons cannot render, use text labels: "Exact", "Under", "Over".
- If PO auto-populate fails, show empty editable line items.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
