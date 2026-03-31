## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Dashboard** page for the **Inventory** module of VISTA. This module is called "The Core" — it tracks all merchandise stock for Villon Farm Supply.

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

Give the user an instant operational view of inventory health: total items and value, low-stock alerts, recent stock movements, and category distribution — enabling proactive restocking decisions.

---

## §3. Application Context (Embedded)

### System Identity
- **Application**: VISTA | **Entity**: Villon Farm Supply | **Platform**: WPF Desktop (1366×768)

### Navigation Context
- **Active Module**: Inventory | **Active Page**: Dashboard
- **Sidebar**: Dashboard, Item Master, Categories, Stock on Hand, Stock Adjustments, Stock Movements, Physical Count, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online

### Color Palette
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`
- Low Stock: `#FFF3E0`/amber | Out of Stock: `#FFEBEE`/red | Healthy: `#E8F5E9`/green

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Summary Cards
4 cards at the top:

| Metric | Icon | Example |
|--------|------|---------|
| Total SKUs | 📦 | 342 |
| Total Stock Value | 💰 | ₱1,245,600.00 |
| Low Stock Alerts | ⚠️ | 18 items |
| Out of Stock | 🔴 | 5 items |

### Component: Low Stock Alerts Table
**Columns:** Item Code, Item Name, Category, Current Qty, Reorder Level, Status (Low/Out).
- Top 15 items sorted by (Current Qty / Reorder Level) ascending.
- Position: Left side, ~55% width.

### Component: Stock Movement Chart
- Bar or line chart showing stock in (receiving) vs stock out (sales) over last 30 days.
- Position: Right side top, ~45% width.

### Component: Category Distribution Chart
- Donut/pie chart showing stock value by category.
- Top 8 categories. "Others" for remainder.
- Position: Right side bottom, ~45% width.

---

## §5. Business Rules (Extracted)

- Low Stock: Current Qty ≤ Reorder Level (amber badge).
- Out of Stock: Current Qty = 0 (red badge).
- Stock value = quantity × last purchase cost per item.

---

## §6. UI Generation Scope

### Page Layout

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ [Total SKUs]  [Stock Value]  [Low Stock]  [Out of Stock]       │
├────────────────────────────────┬────────────────────────────────┤
│                                │  Stock Movement Chart          │
│  Low Stock Alerts Table        │  (In vs Out, 30 days)          │
│  (15 items, sorted by          ├────────────────────────────────┤
│   urgency)                     │  Category Distribution         │
│                                │  (Donut chart)                 │
├────────────────────────────────┴────────────────────────────────┤
└─────────────────────────────────────────────────────────────────┘
```

---

## §7. Layout Expectations

- Cards: 4 across, full width, ~100px tall.
- Left 55%: Low Stock table. Right 45%: Two charts stacked vertically.

---

## §8. Component Expectations

### Sample Cards
1. 📦 Total SKUs: **342** (↑ 5% vs last month)
2. 💰 Stock Value: **₱1,245,600.00** (↑ 12%)
3. ⚠️ Low Stock: **18 items** (↑ 3 from last week)
4. 🔴 Out of Stock: **5 items** (↓ 2 from last week)

### Sample Low Stock Table (8 rows)
| Code | Item | Category | Qty | Reorder Level | Status |
|------|------|----------|-----|---------------|--------|
| ITM-0042 | NPK 14-14-14 (50kg) | Fertilizers | 3 | 10 | ⚠️ Low |
| ITM-0089 | Machete #5 | Farm Tools | 0 | 5 | 🔴 Out |
| ITM-0023 | Tomato Seeds (Diamante) | Seeds | 2 | 15 | ⚠️ Low |
| ITM-0156 | Knapsack Sprayer 16L | Equipment | 0 | 3 | 🔴 Out |
| ITM-0067 | Urea 46-0-0 (50kg) | Fertilizers | 5 | 15 | ⚠️ Low |
| ITM-0034 | Ampalaya Seeds | Seeds | 4 | 10 | ⚠️ Low |
| ITM-0112 | Work Gloves (pair) | Safety | 0 | 20 | 🔴 Out |
| ITM-0078 | Insecticide 1L | Pesticides | 6 | 10 | ⚠️ Low |

### Sample Charts
- **Movement**: In (blue bars): 150, 120, 180 units over 3 weeks. Out (green bars): 130, 145, 160.
- **Category Donut**: Fertilizers 35%, Seeds 20%, Pesticides 15%, Tools 12%, Equipment 8%, Safety 5%, Others 5%.

---

## §9. Interaction Expectations

- Cards: Read-only. Low Stock table rows: clickable to navigate to Item Master.
- Charts: Hover shows tooltip with value.

---

## §10. Do Not Assume

- Do NOT add stock forecasting or prediction features.
- Do NOT add quick-reorder buttons from the dashboard.
- Do NOT add inventory valuation method selector (FIFO/Avg) on the dashboard.

---

## §11. Required Output Quality Standard

- Production-ready dashboard. Agricultural items. ₱ values. Color-coded alerts.
- "Inventory" module active, "Dashboard" page active.

---

## §12. UI Consistency Rules

- Typography: Inter. Cards: white bg, 8px radius, border `#D4D4C8`. Tables: alternating rows.

---

## §13. Fallback Behavior If Context Is Missing

- If charts cannot render, show numeric summaries instead.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
