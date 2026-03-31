## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Dashboard** for the **POS/Sales** module — "The Outflow" — showing today's sales performance, top products, cashier status, and revenue trends.

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

Give the Store Manager an instant view of daily sales performance, cashier shift status, top-selling items, and revenue trends to monitor store operations in real-time.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: POS/Sales | **Active Page**: Dashboard
- **Sidebar**: Dashboard, Transaction, Transaction History, Returns, Customers, Pricing, Cashier Mgmt, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Revenue Cards (4 cards)
| Metric | Icon | Example |
|--------|------|---------|
| Today's Sales | 💰 | ₱28,450.00 |
| Transactions Today | 🧾 | 42 |
| Average Transaction | 📊 | ₱677.38 |
| Returns Today | ↩️ | 2 (₱1,200.00) |

### Component: Daily Sales Chart
- Line chart: hourly revenue for today (7AM–7PM). Shows peak hours.
- Position: Left ~55%, below cards.

### Component: Top Selling Items
- Table: Top 10 items by quantity sold today.
- Columns: Rank, Item Name, Qty Sold, Revenue.
- Position: Right ~45%, top half.

### Component: Cashier Status Widget
- Active cashiers with: Name, Shift Start, Transactions, Total Sales.
- Green dot = active shift. Gray = off duty.
- Position: Right ~45%, bottom half.

---

## §6. UI Generation Scope

### Page Layout

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ [Today's Sales] [Transactions] [Avg Transaction] [Returns]    │
├────────────────────────────────┬────────────────────────────────┤
│                                │ Top Selling Items Today         │
│ Daily Sales Chart              │ #│Item        │Qty│Revenue     │
│ (Hourly: 7AM–7PM)             │ 1│NPK 14-14-14│ 8 │₱6,800      │
│                                │ 2│Tomato Seeds │15 │₱675        │
│ Line chart with ₱ values      │ ...                             │
│                                ├────────────────────────────────┤
│                                │ Cashier Status                  │
│                                │ 🟢 Ana Reyes    │₱18,200      │
│                                │ 🟢 Carlos M.    │₱10,250      │
│                                │ ⚫ Pedro Lim    │ Off          │
└────────────────────────────────┴────────────────────────────────┘
```

---

## §8. Component Expectations

### Revenue Cards
1. 💰 Today's Sales: **₱28,450.00** (↑ 12% vs yesterday)
2. 🧾 Transactions: **42** (↑ 5)
3. 📊 Avg Transaction: **₱677.38** (↑ 3%)
4. ↩️ Returns: **2** (₱1,200.00)

### Top Selling Items (5 rows)
| # | Item | Qty Sold | Revenue |
|---|------|----------|---------|
| 1 | NPK Fertilizer 14-14-14 | 8 | ₱6,800.00 |
| 2 | Tomato Seeds (Diamante) | 15 | ₱675.00 |
| 3 | Urea Fertilizer 46-0-0 | 6 | ₱4,320.00 |
| 4 | Insecticide (Karate) 1L | 5 | ₱2,400.00 |
| 5 | Work Gloves (Leather) | 12 | ₱1,440.00 |

### Cashier Status (3 entries)
| Status | Name | Shift Start | Txns | Total |
|--------|------|-------------|------|-------|
| 🟢 Active | Ana Reyes | 07:00 AM | 25 | ₱18,200.00 |
| 🟢 Active | Carlos Mendoza | 12:00 PM | 17 | ₱10,250.00 |
| ⚫ Off Duty | Pedro Lim | — | — | — |

---

## §10. Do Not Assume

- Do NOT add real-time live-updating ticker.
- Do NOT add "quick sale" shortcut buttons.
- Do NOT add goal/target indicators.

---

## §11. Required Output Quality Standard

- Production-ready dashboard. ₱ values. Agricultural products.
- "POS/Sales" module active, "Dashboard" page active.

---

## §12. UI Consistency Rules

- Typography: Inter. Cards: white bg, 8px radius. Charts: primary green for revenue.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
