## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Stock on Hand** page — a real-time inventory snapshot showing current quantities, values, and stock status for every item.

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

Provide an accurate, filterable view of all current stock quantities with color-coded status indicators, enabling the Manager to identify items needing attention (low stock, out of stock).

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: Inventory | **Active Page**: Stock on Hand
- **Sidebar**: Dashboard, Item Master, Categories, **Stock on Hand**, Stock Adjustments, Stock Movements, Physical Count, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Stock Table
**Columns:**

| Column | Sortable | Width |
|--------|----------|-------|
| Item Code | Yes | 90px |
| Item Name | Yes | 200px |
| Category | Yes | 120px |
| Unit | No | 60px |
| Qty on Hand | Yes | 90px |
| Reorder Level | No | 90px |
| Unit Cost | Yes | 100px |
| Total Value | Yes | 110px |
| Status | Yes | 90px |

- Status: In Stock (green), Low Stock (amber), Out of Stock (red).
- Default sort: Status (Out first, Low second, In Stock last).

### Component: Stock Filters
| Filter | Default |
|--------|---------|
| Category | All |
| Status | All (In Stock, Low Stock, Out of Stock) |
| Supplier | All (last supplier for each item) |

### Component: Stock Detail Drawer
- Slides in from right on row click.
- Shows: Item details, stock history graph (30 days), recent movements (last 10), reorder info.

### Component: Sync Badge
- Per-row indicator showing if local stock matches central DB.
- 🟢 Synced, 🟡 Pending, 🔴 Conflict.

---

## §5. Business Rules (Extracted)

- Low Stock: Qty ≤ Reorder Level (amber).
- Out of Stock: Qty = 0 (red). In Stock: Qty > Reorder Level (green).
- Total Value = Qty × Unit Cost.
- Stock is read-only on this page. Changes occur via Receiving, Sales, or Adjustments.

---

## §6. UI Generation Scope

### Page Layout (Primary State: List View)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ Stock on Hand                               🕐 As of 30/03/2026│
├─────────────────────────────────────────────────────────────────┤
│ [All Categories ▾] [All Status ▾] [All Suppliers ▾] [Clear All]│
├─────────────────────────────────────────────────────────────────┤
│ Code │Name         │Category    │Unit│ Qty │Reorder│ Cost  │Value    │Status  │
│──────┼─────────────┼────────────┼────┼─────┼───────┼───────┼─────────┼────────│
│ rows with color-coded status badges and row highlighting       │
├─────────────────────────────────────────────────────────────────┤
│ Total Items: 342  │  Total Value: ₱1,245,600.00                │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample Table (8 rows)
| Code | Name | Category | Unit | Qty | Reorder | Cost | Value | Status |
|------|------|----------|------|-----|---------|------|-------|--------|
| ITM-0089 | Machete #5 | Farm Tools | pcs | 0 | 5 | ₱320.00 | ₱0.00 | 🔴 Out |
| ITM-0112 | Work Gloves | Safety | pair | 0 | 20 | ₱85.00 | ₱0.00 | 🔴 Out |
| ITM-0156 | Knapsack Sprayer 16L | Equipment | pcs | 0 | 3 | ₱1,200.00 | ₱0.00 | 🔴 Out |
| ITM-0042 | NPK 14-14-14 (50kg) | Fertilizers | bag | 3 | 10 | ₱780.00 | ₱2,340.00 | ⚠️ Low |
| ITM-0023 | Tomato Seeds (Diamante) | Seeds | pack | 2 | 15 | ₱38.00 | ₱76.00 | ⚠️ Low |
| ITM-0067 | Urea 46-0-0 (50kg) | Fertilizers | bag | 5 | 15 | ₱650.00 | ₱3,250.00 | ⚠️ Low |
| ITM-0034 | Ampalaya Seeds | Seeds | pack | 45 | 10 | ₱42.00 | ₱1,890.00 | ✅ In Stock |
| ITM-0078 | Insecticide (Karate) 1L | Pesticides | bottle | 28 | 10 | ₱380.00 | ₱10,640.00 | ✅ In Stock |

---

## §9. Interaction Expectations

- Row click: opens detail drawer. Filters: immediate update.
- Status filter: quick access to problem items.

---

## §10. Do Not Assume

- Do NOT add stock editing on this page — read-only.
- Do NOT add reorder/PO creation from this page.
- Do NOT add warehouse/location columns.

---

## §11. Required Output Quality Standard

- Production-ready. Color-coded rows. ₱ values. Summary totals.
- "Stock on Hand" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Status: Out=`#FFEBEE`/red, Low=`#FFF3E0`/amber, In Stock=`#E8F5E9`/green.
- Out-of-stock rows: left 3px red border.

---

## §13. Fallback Behavior If Context Is Missing

- If sync badges cannot render, omit them. Stock data is always local.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
