## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate a single, complete page layout for the **Suppliers** page within the **Purchase/Procurement** module of the VISTA application.

This is a master data management page. It follows a **list-detail pattern**: a searchable table of suppliers on the left with a detail panel that slides in from the right when a supplier is selected.

---

## §2. System Objective

Enable the user to search, browse, create, edit, and view supplier records — the foundation of all procurement activity. Every Purchase Order references a supplier from this master list.

---

## §3. Application Context (Embedded)

### System Identity
- **Application**: VISTA — Villon's Integrated Supply and Trade Application
- **Entity**: Villon Farm Supply (agricultural retail, MSME)
- **Platform**: Windows desktop (WPF) — design for 1366×768 minimum
- **Design Language**: Professional, functional, data-dense. Not decorative.

### Navigation Context
- **Active Module**: Purchasing (highlighted in top module switcher)
- **Active Page**: Suppliers (highlighted in left sidebar)
- **Sidebar Pages**: Dashboard, Suppliers, Purchase Requests, Purchase Orders, Receiving, Payables, Reports
- **Global Elements**: User "Maria Santos" / Role "Manager" (top-right), Sync 🟢 Online (footer)

### Color Palette
- **Primary**: `#4A6741` (sage green) | **Sidebar**: `#2C3E2C` | **Background**: `#FAFAF5`
- **Status Colors**: Active=`#E8F5E9`/green, Inactive=`#E0E0E0`/gray

---

## §4. Referenced Documentation (Embedded Extracts)

### Module Context

The Purchase/Procurement module manages supplier-facing merchandise acquisition. Suppliers are referenced by Purchase Requests and Purchase Orders (BR-P1: Every PO must reference a valid Supplier).

### Component: Supplier Search Bar

- Position: Top of content area, full-width
- Debounced search (300ms delay), searches across supplier name, code, and contact info
- Right side: "+ New Supplier" button (primary style)
- Recent searches dropdown. `Ctrl+F` shortcut focus.

### Component: Supplier Filters

- Position: Below search bar
- Filters: Status (Active/Inactive/All, default: Active), City/Region (dropdown), Payment Terms (dropdown)
- Left-aligned filter chips. "Clear All" button right-aligned.
- Filters persist until explicitly cleared.

### Component: Supplier List Table

**Columns:**

| Column | Sortable | Width |
|--------|----------|-------|
| Supplier Code | Yes | 100px |
| Supplier Name | Yes | 200px |
| Contact Person | No | 150px |
| Phone | No | 120px |
| City | Yes | 120px |
| Status | Yes | 80px |
| Actions | No | 80px |

- Default sort: Supplier Name ascending.
- Row click opens detail panel.
- Actions: Edit, Deactivate.
- Status badges: Active (green), Inactive (gray).
- Pagination: 20 rows per page. Page navigation at bottom.

### Component: Supplier Form (Create/Edit)

**Fields:**

| Field | Type | Required |
|-------|------|----------|
| Supplier Code | Auto-generated (SUP-NNNN) | Yes (read-only) |
| Supplier Name | Text | Yes |
| Contact Person | Text | No |
| Phone | Text | No |
| Email | Text | No |
| Address | Multiline | No |
| City / Region | Dropdown | No |
| Payment Terms | Dropdown (Net 30, Net 60, COD, etc.) | No |
| Tax ID (TIN) | Text | No |
| Notes | Multiline | No |

- 2-column layout. Appears as a full-page form replacing the table, or as a modal.
- Validation: Name required, unique. Email format. Phone format.

### Component: Supplier Detail Panel

- Position: Slides in from right (~40% width) when a table row is clicked
- Sections:
  1. Header: Supplier name, code, status badge
  2. Contact: Person, phone, email, address
  3. Terms: Payment terms, tax ID
  4. Activity: Recent POs (last 5), total purchase amount (all-time), last order date
- Actions: Edit, Create PO for this Supplier
- Close via Escape key or X button.

---

## §5. Business Rules (Extracted)

- BR-P1: Every Purchase Order must reference a valid Supplier. Supplier master must exist before PO creation.
- BR-P9: Supplier codes use format SUP-NNNN (auto-generated, sequential).
- Suppliers are never physically deleted (soft delete — deactivated).
- Supplier quick-create is available inline from the PO form (modal).

---

## §6. UI Generation Scope

### Page Layout (Primary State: List View with Detail Panel Open)

```
CONTENT AREA:
┌──────────────────────────────────────────────────────────────────────┐
│ [🔍 Search suppliers...                    ] [+ New Supplier]       │
│ [Active ▾] [City ▾] [Payment Terms ▾]              [Clear All]     │
├──────────────────────────────────────────┬───────────────────────────┤
│                                          │                           │
│  Supplier List Table                     │  Detail Panel             │
│  (Supplier Code | Name | Contact |       │  Header: Agri-Plus       │
│   Phone | City | Status | Actions)       │  Contact info             │
│                                          │  Terms                    │
│  [20 rows, paginated]                    │  Recent POs               │
│                                          │  [Edit] [Create PO]       │
│                                          │                           │
├──────────────────────────────────────────┴───────────────────────────┤
│ Showing 1-20 of 45 suppliers                   ← 1 2 3 → (pages)   │
└──────────────────────────────────────────────────────────────────────┘
```

### Component Composition

1. **Supplier Search Bar** — top, full-width
2. **Supplier Filters** — below search, full-width
3. **Supplier List Table** — left ~60%, below filters
4. **Supplier Detail Panel** — right ~40%, slides in on row click

---

## §7. Layout Expectations

- **Search Bar**: Full content width, 36px height, magnifying glass icon left, "+ New Supplier" button right.
- **Filters**: Horizontal row of dropdowns below search. 8px gap between each. ~32px height.
- **Table**: 60% width when detail panel is open. Alternating row colors. 36px row height.
- **Detail Panel**: 40% width, white background, right-aligned with left border (`#D4D4C8`). Scrollable if content overflows.
- **Pagination**: Bottom of table area, right-aligned page numbers.

---

## §8. Component Expectations

### Sample Data — Table (8 rows)
| Code | Name | Contact | Phone | City | Status |
|------|------|---------|-------|------|--------|
| SUP-0001 | Agri-Plus Supplies | Roberto Santos | 0917-555-0101 | Manila | Active |
| SUP-0002 | Manila Seed Corp | Elena Villanueva | 0918-555-0202 | Quezon City | Active |
| SUP-0003 | FarmTech Solutions | Marco Tan | 0919-555-0303 | Cebu | Active |
| SUP-0004 | Green Valley Agri | Ana Reyes | 0920-555-0404 | Davao | Active |
| SUP-0005 | Crop Care Inc. | Pedro Lim | 0921-555-0505 | Batangas | Active |
| SUP-0006 | BioGrow Philippines | Rosa Hernandez | 0922-555-0606 | Laguna | Active |
| SUP-0007 | Pacific Agri Trading | Luis Garcia | 0923-555-0707 | Pampanga | Inactive |
| SUP-0008 | Golden Harvest Corp | Carmen Cruz | 0924-555-0808 | Tarlac | Active |

### Sample Data — Detail Panel (for SUP-0001 "Agri-Plus Supplies")
- **Header**: "Agri-Plus Supplies" / SUP-0001 / 🟢 Active
- **Contact**: Roberto Santos, 0917-555-0101, roberto@agriplus.ph, 123 Taft Ave, Manila
- **Terms**: Net 30, TIN: 123-456-789-000
- **Recent POs**: PO-2026-0048 (₱45,200, Pending), PO-2026-0043 (₱33,400, Received), PO-2026-0038 (₱27,800, Received)
- **Total Purchases**: ₱425,000.00 | Last Order: 28/03/2026

---

## §9. Interaction Expectations

- Search is debounced (300ms). Typing filters the table in real-time.
- Row click opens the detail panel from the right.
- Escape key or X button closes the detail panel.
- "+ New Supplier" opens the supplier form (full page or modal).
- "Edit" in detail panel opens the form pre-populated.
- `Ctrl+F` focuses the search bar.

---

## §10. Do Not Assume

- Do NOT add bulk import/export functionality.
- Do NOT add supplier rating or scoring features.
- Do NOT add multi-select checkboxes to the table.
- Do NOT create a separate "Supplier Categories" section.
- Do NOT assume the detail panel is always open — it slides in on row click.

---

## §11. Required Output Quality Standard

- The screen must look like a production-ready data management page.
- All text must be realistic with Filipino names and agricultural business names.
- Philippine Peso (₱) for all currency values.
- Status badges must use documented colors (Active=green, Inactive=gray).
- Table must show 6–8 rows of sample data.
- "Purchasing" module active, "Suppliers" page active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter (fallback: Segoe UI).
- Status colors: Active=`#E8F5E9`/green, Inactive=`#E0E0E0`/gray.
- Sidebar: `#2C3E2C`, active page: `#4A6741`.
- Tables: alternating row colors, `#F5F5EE` header background.
- Forms: 2-column, labels above fields, required fields marked *.
- Buttons: Primary `#4A6741`, Cancel neutral.

---

## §13. Fallback Behavior If Context Is Missing

- If the detail panel cannot slide in, render it as a right column always visible.
- If filter dropdowns cannot render inline, use stacked dropdowns.
- If sample phone numbers seem unrealistic, use generic Philippine mobile format.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code, API endpoints, or database schemas.
- Do NOT generate HTML/CSS/XAML implementation code.
- Do NOT generate mobile or tablet layouts.
- Do NOT design screens for modules other than Purchase/Procurement.
- Do NOT modify or extend the documented component specifications.
