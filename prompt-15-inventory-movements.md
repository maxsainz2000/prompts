## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Stock Movements** page — a read-only audit log of all stock quantity changes (receiving, sales, adjustments, returns).

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

Provide a chronological audit trail of every stock quantity change — who changed what, when, why, and from which module — enabling the Manager to trace any discrepancy back to its source.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: Inventory | **Active Page**: Stock Movements
- **Sidebar**: Dashboard, Item Master, Categories, Stock on Hand, Stock Adjustments, **Stock Movements**, Physical Count, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Movement Log Table
**Columns:**

| Column | Sortable | Width |
|--------|----------|-------|
| Date/Time | Yes | 140px |
| Item Code | Yes | 90px |
| Item Name | Yes | 180px |
| Type | Yes | 100px |
| Direction | No | 60px |
| Qty | No | 60px |
| Before | No | 60px |
| After | No | 60px |
| Reference | No | 130px |
| User | No | 120px |

- **Type Icons**: 📦 Receiving, 🛒 Sale, ↩️ Return, 📉 Adjustment, 📋 Count.
- **Direction**: ↑ In (green text), ↓ Out (red text).
- Default sort: Date/Time descending. Read-only log — no edit actions.

### Component: Movement Filters
| Filter | Default |
|--------|---------|
| Date Range | Last 7 days |
| Item | All |
| Type | All (Receiving, Sale, Return, Adjustment, Count) |
| User | All |

### Component: Movement Detail Modal
- Opened on row click.
- Shows: Full record details, source document link (PO/Sale/Adjustment reference), before/after, reason (if adjustment).

### Component: Movement Type Icons
- Color-coded icons per type for quick visual scanning.

---

## §5. Business Rules (Extracted)

- Movement log is append-only — never edited or deleted.
- All movements are system-generated from module events (not manually created).
- References link back to source: RCV-YYYY-NNNN, SALE-YYYY-NNNN, ADJ-YYYY-NNNN.

---

## §6. UI Generation Scope

### Page Layout (Primary State: Movement Log)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ Stock Movements                                                 │
├─────────────────────────────────────────────────────────────────┤
│ [Last 7 Days ▾] [All Items ▾] [All Types ▾] [All Users ▾]     │
├─────────────────────────────────────────────────────────────────┤
│ Date/Time    │Code │Item        │Type    │Dir│Qty│Before│After│Ref       │User    │
│──────────────┼─────┼────────────┼────────┼───┼───┼──────┼─────┼──────────┼────────│
│ 30/03 14:22  │0042 │NPK 14-14-14│📦 Recv │ ↑ │+20│  3   │ 23  │RCV-0024  │Juan    │
│ 30/03 11:05  │0023 │Tomato Seeds│🛒 Sale │ ↓ │ -5│  7   │  2  │SALE-0892 │Ana     │
│ 29/03 16:30  │0089 │Machete #5  │📉 Adj  │ ↓ │ -2│  2   │  0  │ADJ-0007  │Carlos  │
│ ...          │     │            │        │   │   │      │     │          │        │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample Data (8 rows)
| Date/Time | Code | Item | Type | Dir | Qty | Before | After | Reference | User |
|-----------|------|------|------|-----|-----|--------|-------|-----------|------|
| 30/03 14:22 | ITM-0042 | NPK 14-14-14 | 📦 Receiving | ↑ | +20 | 3 | 23 | RCV-2026-0024 | Juan Dela Cruz |
| 30/03 11:05 | ITM-0023 | Tomato Seeds | 🛒 Sale | ↓ | -5 | 7 | 2 | SALE-2026-0892 | Ana Reyes |
| 30/03 09:40 | ITM-0067 | Urea 46-0-0 | 🛒 Sale | ↓ | -3 | 8 | 5 | SALE-2026-0891 | Ana Reyes |
| 29/03 16:30 | ITM-0089 | Machete #5 | 📉 Adjustment | ↓ | -2 | 2 | 0 | ADJ-2026-0007 | Carlos Mendoza |
| 29/03 14:10 | ITM-0034 | Ampalaya Seeds | 📦 Receiving | ↑ | +50 | 12 | 62 | RCV-2026-0023 | Juan Dela Cruz |
| 29/03 10:20 | ITM-0078 | Insecticide 1L | 🛒 Sale | ↓ | -2 | 30 | 28 | SALE-2026-0890 | Ana Reyes |
| 28/03 15:45 | ITM-0042 | NPK 14-14-14 | 🛒 Sale | ↓ | -5 | 8 | 3 | SALE-2026-0889 | Ana Reyes |
| 28/03 09:00 | ITM-0112 | Work Gloves | ↩️ Return | ↑ | +3 | 0 | 3 | RTN-2026-0012 | Ana Reyes |

---

## §9. Interaction Expectations

- Row click: opens detail modal. Filters: immediate table update.
- Read-only — no edit, delete, or manual creation.

---

## §10. Do Not Assume

- Do NOT add manual movement creation — movements are system-generated.
- Do NOT add export/download on this page (that's in Reports).
- Do NOT add timeline/graph view — table only.

---

## §11. Required Output Quality Standard

- Production-ready. Type icons clearly distinguishable. Direction arrows color-coded.
- "Stock Movements" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Tables: alternating rows. In=green text, Out=red text.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
