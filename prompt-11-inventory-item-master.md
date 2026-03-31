## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Item Master** page — the central product catalog for Villon Farm Supply. This is a list-detail page with the most fields of any master data page in the system (7 components).

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

Enable staff to manage the complete product catalog — create, edit, search, and view items including pricing, categorization, stock levels, and reorder thresholds.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: Inventory | **Active Page**: Item Master
- **Sidebar**: Dashboard, **Item Master**, Categories, Stock on Hand, Stock Adjustments, Stock Movements, Physical Count, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Item Search Bar
- Full-width, debounced (300ms). Searches item code, name, barcode.
- Right side: "+ New Item" button. `Ctrl+F` shortcut.

### Component: Item Filters
| Filter | Default |
|--------|---------|
| Category | All |
| Status | Active |
| Stock Level | All (All, Low, Out of Stock, In Stock) |

### Component: Item List Table
**Columns:**

| Column | Sortable | Width |
|--------|----------|-------|
| Item Code | Yes | 100px |
| Item Name | Yes | 200px |
| Category | Yes | 120px |
| Unit | No | 60px |
| Cost | Yes | 100px |
| Selling Price | Yes | 100px |
| Qty on Hand | Yes | 80px |
| Status | Yes | 80px |

Default sort: Item Name ascending. Pagination: 25 rows/page. Row click opens detail.

### Component: Item Form (Create/Edit)
**Fields — 2-column layout:**

| Field | Required |
|-------|----------|
| Item Code (auto: ITM-NNNN) | Read-only |
| Barcode | No |
| Item Name | Yes |
| Description | No |
| Category (dropdown) | Yes |
| Unit of Measure (dropdown: pcs, kg, L, bag, pack, box) | Yes |
| Cost Price (₱) | Yes |
| Selling Price (₱) | Yes |
| Reorder Level | No (default: 0) |
| Minimum Qty | No |
| Image Upload | No |
| Status | Active/Inactive |
| Notes | No |

### Component: Item Detail Panel
- Slides in from right (~40% width) on row click.
- Sections: Header (name, code, image), Pricing (cost, selling, margin %), Stock Info (on-hand, reorder level, last restock date), Recent Transactions (last 5 stock movements).

### Component: Item Image Upload
- Square image area (~120×120px) in the form.
- Drag-and-drop or click to browse. Preview shown after upload.

### Component: Category Quick-Select
- Dropdown with "Create Category" option at bottom for inline category creation.

---

## §5. Business Rules (Extracted)

- Item codes are auto-generated: ITM-NNNN.
- Selling Price should be > Cost Price (warning, not block).
- Items are soft-deleted (deactivated, never removed).
- Category is required for every item.

---

## §6. UI Generation Scope

### Page Layout (Primary State: List with Detail Panel)

```
CONTENT AREA:
┌──────────────────────────────────────────────────────────────────┐
│ [🔍 Search items...                          ] [+ New Item]     │
│ [All Categories ▾] [Active ▾] [All Stock ▾]       [Clear All]  │
├──────────────────────────────────────┬───────────────────────────┤
│                                      │  Item Detail Panel        │
│  Item List Table                     │  [Image]                  │
│  (Code│Name│Category│Unit│           │  ITM-0042                 │
│   Cost│Price│Qty│Status)             │  NPK 14-14-14 (50kg)      │
│                                      │  Category: Fertilizers    │
│  25 rows/page                        │  Cost: ₱780 | Sell: ₱850 │
│                                      │  On Hand: 3 | Reorder: 10│
│                                      │  Recent movements...      │
├──────────────────────────────────────┴───────────────────────────┤
│ Showing 1-25 of 342 items                    ← 1 2 3 … → pages │
└──────────────────────────────────────────────────────────────────┘
```

---

## §7. Layout Expectations

- Search + filters: full width, top. Table: 60% when panel open. Panel: 40%.
- Pagination at bottom.

---

## §8. Component Expectations

### Sample Table (8 rows)
| Code | Name | Category | Unit | Cost | Price | Qty | Status |
|------|------|----------|------|------|-------|-----|--------|
| ITM-0042 | NPK Fertilizer 14-14-14 | Fertilizers | bag | ₱780.00 | ₱850.00 | 3 | Active |
| ITM-0023 | Tomato Seeds (Diamante F1) | Seeds | pack | ₱38.00 | ₱45.00 | 2 | Active |
| ITM-0089 | Machete #5 Heavy Duty | Farm Tools | pcs | ₱320.00 | ₱420.00 | 0 | Active |
| ITM-0067 | Urea Fertilizer 46-0-0 | Fertilizers | bag | ₱650.00 | ₱720.00 | 5 | Active |
| ITM-0112 | Work Gloves (Leather) | Safety | pair | ₱85.00 | ₱120.00 | 0 | Active |
| ITM-0156 | Knapsack Sprayer 16L | Equipment | pcs | ₱1,200.00 | ₱1,550.00 | 0 | Active |
| ITM-0034 | Ampalaya Seeds (Galaxy) | Seeds | pack | ₱42.00 | ₱55.00 | 4 | Active |
| ITM-0078 | Insecticide (Karate) 1L | Pesticides | bottle | ₱380.00 | ₱480.00 | 6 | Active |

### Sample Detail Panel (ITM-0042)
- **Image**: Fertilizer bag placeholder
- **Pricing**: Cost ₱780.00 | Selling ₱850.00 | Margin 8.97%
- **Stock**: On Hand 3 | Reorder Level 10 | ⚠️ Low Stock
- **Recent**: Received +20 (28/03), Sold -5 (27/03), Sold -8 (25/03)

---

## §9. Interaction Expectations

- Search: debounced filtering. Row click: opens detail panel (right slide-in).
- "+ New Item": opens full-page form. `Ctrl+N` shortcut.
- Escape: closes detail panel.

---

## §10. Do Not Assume

- Do NOT add barcode scanning interface.
- Do NOT add batch/lot tracking columns.
- Do NOT add multiple pricing tiers per item.
- Do NOT add import/export CSV for items.

---

## §11. Required Output Quality Standard

- Production-ready. Agricultural products. ₱ values. Stock alerts visible.
- "Item Master" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Tables: alternating rows. Status: Active=green, Inactive=gray.
- Low stock rows: amber left border indicator.

---

## §13. Fallback Behavior If Context Is Missing

- If image placeholder cannot render, use a colored initial square.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
