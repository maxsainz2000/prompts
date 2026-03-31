## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate a single, complete page layout for the **Dashboard** page within the **Purchase/Procurement** module of the VISTA application.

This module is called "The Inflow" — it manages how goods enter the business from suppliers. The Dashboard provides an at-a-glance operational overview of procurement activity.

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

Give the Purchasing Manager an immediate snapshot of procurement health: how many open orders exist, what needs approval, how much is owed to suppliers, and what activity has occurred recently — all without navigating to individual pages.

---

## §3. Application Context (Embedded)

### System Identity
- **Application**: VISTA — Villon's Integrated Supply and Trade Application
- **Entity**: Villon Farm Supply (agricultural retail, MSME)
- **Platform**: Windows desktop (WPF) — design for 1366×768 minimum
- **Design Language**: Professional, functional, data-dense. Not decorative.

### Navigation Context
- **Active Module**: Purchasing (highlighted in top module switcher)
- **Active Page**: Dashboard (highlighted in left sidebar)
- **Sidebar Pages**: Dashboard, Suppliers, Purchase Requests, Purchase Orders, Receiving, Payables, Reports
- **Global Elements**: User "Maria Santos" / Role "Manager" (top-right), Sync 🟢 Online (footer)

### Color Palette
- **Primary**: `#4A6741` (sage green)
- **Sidebar**: `#2C3E2C` (dark forest green)
- **Content Background**: `#FAFAF5` (warm off-white)
- **Status Colors**: Draft=`#E0E0E0`, Pending=`#FFF3E0`, Approved=`#E8F5E9`, Partially Received=`#E3F2FD`, Fully Received=`#E0F2F1`, Void=`#F5F5F5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Module Purpose (from `modules/purchase-procurement/spec.md`)

The Purchase/Procurement module manages the entire supplier-facing lifecycle of merchandise acquisition — from identifying suppliers, requesting goods, raising formal purchase orders, receiving shipments, to tracking payment obligations.

### User Roles

| Role | Access Level |
|------|-------------|
| Store Owner / Manager | Full access — create, edit, approve, void, view reports |
| Purchasing Clerk | Operational — create suppliers, PRs, POs, record receiving |
| Accountant | Read-only + Payables |
| Cashier | No access to this module |

### Component: Summary Cards

Provides an at-a-glance numeric overview. Displays 4 key metric cards at the top of the dashboard in a full-width row.

**Cards Displayed:**

| # | Metric | Icon | Example Value | Trend Context |
|---|--------|------|---------------|---------------|
| 1 | Open Purchase Orders | 📋 | 12 | vs. last 30 days |
| 2 | Pending Approvals | ⏳ | 3 | vs. last 30 days |
| 3 | Outstanding Payables | 💰 | ₱145,230.00 | vs. last 30 days |
| 4 | Deliveries This Month | 📦 | 8 | vs. last month |

Each card shows: Icon, Label, Value (large font), Trend indicator (↑/↓ with %).
Cards are not clickable. Values refresh on page load.
Monetary values use ₱ with 2 decimal places and comma separators.

### Component: Recent Orders Table

Displays the most recent 10 Purchase Orders for quick reference. Takes ~50% width (left side), alongside Pending Approvals Widget.

**Columns:**

| Column | Type | Width |
|--------|------|-------|
| PO # | Text (link) | 120px |
| Supplier | Text | 200px |
| Date | Date (DD/MM/YYYY) | 100px |
| Total | Currency (₱) | 120px |
| Status | Badge | 120px |

- Fixed 10 rows maximum, no pagination.
- PO # is a clickable link. "View All" link at bottom.
- Status uses standard badges (Draft=gray, Pending=amber, Approved=green, etc.).

### Component: Pending Approvals Widget

Displays PRs and POs awaiting approval. Takes ~50% width (right side).

**Each item shows:**
- Type icon: 📝 (PR) or 📋 (PO)
- Reference #: PR-2026-0015 or PO-2026-0042
- Submitted By: User name
- Submitted On: Relative time ("2 hours ago")
- Total Amount: ₱ value
- "Review" button

Maximum 5 items. FIFO ordering (oldest first). If >5 pending, show "3 more pending" with "View All" link.
Empty state: "✅ All caught up — no pending approvals!"

### Component: Supplier Activity Feed

Chronological feed of recent supplier-related activities. Full-width, below the Recent Orders and Pending Approvals.

**Activity Types:**

| Activity | Icon | Example |
|----------|------|---------|
| Supplier Created | 🏪 | "New supplier 'Agri-Plus Supplies' added by Juan" |
| PO Created | 📋 | "Purchase Order PO-2026-0042 created for Agri-Plus Supplies" |
| PO Approved | ✅ | "PO-2026-0042 approved by Maria" |
| Goods Received | 📦 | "Delivery RCV-2026-0018 received against PO-2026-0042" |
| Payment Made | 💳 | "Payment of ₱25,000.00 made to Agri-Plus Supplies" |

Each item: Timestamp (relative) + Icon + Description + Actor.
Last 15 activities, most recent first. Fixed-height container (~300px) with scroll.

---

## §5. Business Rules (Extracted)

- BR-P2: Purchase Requests require approval. Pending count contributes to Pending Approvals card and widget.
- BR-P3: Purchase Orders require approval. Pending count contributes to Pending Approvals card and widget.
- BR-P7: Outstanding Payables = total received goods value, not PO value.
- BR-P9: Reference numbers use format PR-YYYY-NNNN, PO-YYYY-NNNN.

---

## §6. UI Generation Scope

### Page Layout

```
SHELL (top bar + sidebar + footer):

CONTENT AREA:
┌─────────────────────────────────────────────────────────────┐
│ [Summary Card 1] [Summary Card 2] [Summary Card 3] [Card 4]│  ← Row 1 (cards)
├────────────────────────┬────────────────────────────────────┤
│                        │                                    │
│  Recent Orders Table   │   Pending Approvals Widget         │  ← Row 2 (50/50)
│  (last 10 POs)         │   (up to 5 pending items)         │
│                        │                                    │
├────────────────────────┴────────────────────────────────────┤
│                                                             │
│  Supplier Activity Feed (last 15, scrollable)               │  ← Row 3 (full width)
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Component Composition

1. **Summary Cards** — 4 cards in a horizontal row (top, full-width)
2. **Recent Orders Table** — Left 50% of middle row
3. **Pending Approvals Widget** — Right 50% of middle row
4. **Supplier Activity Feed** — Full-width bottom section

---

## §7. Layout Expectations

- **Summary Cards Row**: 4 cards evenly distributed in one row. Each card ~25% width with 12px gap. Card height ~100px. White card background with subtle border.
- **Middle Row**: Two panels side-by-side, each ~50% width with 12px gap. Each ~350px tall.
- **Activity Feed**: Full width, ~300px tall with internal scroll. Below the middle row with 16px gap.
- **Overall**: Page content uses 16px padding from shell edges.

---

## §8. Component Expectations

### Summary Cards (with sample data)
1. 📋 Open Purchase Orders: **12** (↑ 15% vs last 30 days, green arrow)
2. ⏳ Pending Approvals: **3** (↓ 25% vs last 30 days, green arrow because fewer = better)
3. 💰 Outstanding Payables: **₱145,230.00** (↑ 8% vs last 30 days, amber arrow)
4. 📦 Deliveries This Month: **8** (↑ 33% vs last month, green arrow)

### Recent Orders Table (sample data — 7 rows)
| PO # | Supplier | Date | Total | Status |
|------|----------|------|-------|--------|
| PO-2026-0048 | Agri-Plus Supplies | 28/03/2026 | ₱45,200.00 | Pending |
| PO-2026-0047 | Manila Seed Corp | 27/03/2026 | ₱28,500.00 | Approved |
| PO-2026-0046 | FarmTech Solutions | 26/03/2026 | ₱15,800.00 | Partially Received |
| PO-2026-0045 | Green Valley Agri | 25/03/2026 | ₱62,100.00 | Fully Received |
| PO-2026-0044 | Crop Care Inc. | 24/03/2026 | ₱8,900.00 | Approved |
| PO-2026-0043 | Agri-Plus Supplies | 22/03/2026 | ₱33,400.00 | Fully Received |
| PO-2026-0042 | BioGrow Philippines | 20/03/2026 | ₱19,750.00 | Void |

### Pending Approvals Widget (sample data — 3 items)
1. 📝 PR-2026-0015 — Submitted by Juan Dela Cruz — "2 hours ago" — ₱18,500.00 — [Review]
2. 📋 PO-2026-0048 — Submitted by Ana Reyes — "Yesterday" — ₱45,200.00 — [Review]
3. 📝 PR-2026-0014 — Submitted by Carlos Mendoza — "2 days ago" — ₱7,200.00 — [Review]

### Supplier Activity Feed (sample data — 8 items)
1. 💳 "Payment of ₱25,000.00 made to Agri-Plus Supplies" — Maria Santos — 1 hour ago
2. 📦 "Delivery RCV-2026-0023 received against PO-2026-0045" — Juan Dela Cruz — 3 hours ago
3. ✅ "PO-2026-0047 approved by Maria Santos" — 5 hours ago
4. 📋 "Purchase Order PO-2026-0048 created for Agri-Plus Supplies" — Ana Reyes — Yesterday
5. 📝 "Purchase Request PR-2026-0015 submitted by Juan Dela Cruz" — Yesterday
6. 🏪 "New supplier 'BioGrow Philippines' added by Carlos Mendoza" — 2 days ago
7. 💳 "Payment of ₱15,800.00 made to FarmTech Solutions" — Maria Santos — 3 days ago
8. 📦 "Delivery RCV-2026-0022 received against PO-2026-0044" — Juan Dela Cruz — 3 days ago

---

## §9. Interaction Expectations

- Summary cards: read-only, no click interaction.
- PO # in Recent Orders: clickable link appearance (underline on hover).
- "Review" buttons in Pending Approvals: primary button style, clickable.
- "View All" links: text link style below both the table and widget.
- Activity feed: scrollable within fixed container.

---

## §10. Do Not Assume

- Do NOT invent additional summary cards beyond the 4 specified.
- Do NOT add charts or graphs to the dashboard — the Activity Feed is a text list, not a chart.
- Do NOT add inline approval buttons — approvals happen on the dedicated PR/PO pages.
- Do NOT add search functionality to the dashboard.
- Do NOT create drill-down modals for any component.
- Do NOT assume this page has tabbed views — it is a single scrollable dashboard.

---

## §11. Required Output Quality Standard

- The screen must look like a production-ready desktop application dashboard.
- All text must be realistic sample data with Filipino names and agricultural suppliers.
- Philippine Peso (₱) for all currency values with comma separators and 2 decimal places.
- Status badges must use the documented color palette.
- Tables must show 5–8 rows of sample data.
- The "Purchasing" module tab must be highlighted. "Dashboard" must be highlighted in the sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter (fallback: Segoe UI).
- Status colors: Draft=`#E0E0E0`, Pending=`#FFF3E0`/amber, Approved=`#E8F5E9`/green, Rejected=red, Void=`#F5F5F5`/black.
- Layout: Sidebar left ~200px, content fills remaining width.
- Tables: alternating row colors, header row with `#F5F5EE` background.
- Cards: White background, 1px `#D4D4C8` border, 8px border radius.
- Buttons: Primary `#4A6741` background, white text, 4px border radius.
- Footer: Sync indicator always visible.

---

## §13. Fallback Behavior If Context Is Missing

- If summary card icons are not available, use colored circles or text-only labels.
- If trend indicators cannot be rendered as arrows, use text "+15%" or "-25%".
- If a sample supplier name seems too long, truncate with ellipsis.
- If the activity feed exceeds the container, enable vertical scrolling.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code, API endpoints, or database schemas.
- Do NOT generate HTML/CSS/XAML implementation code.
- Do NOT generate mobile or tablet layouts.
- Do NOT design screens for modules other than Purchase/Procurement.
- Do NOT modify or extend the documented component specifications.
