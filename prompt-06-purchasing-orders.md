## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Purchase Orders form view** — the most component-dense page in the Purchasing module (8 components). This is the primary state because the PO creation/editing form is the highest-value operational screen.

---

## §2. System Objective

Enable the Purchasing Clerk or Manager to create a formal Purchase Order to a supplier — specifying items, quantities, prices, and delivery expectations — and submit it for approval before sending to the supplier.

---

## §3. Application Context (Embedded)

### System Identity
- **Application**: VISTA — Villon's Integrated Supply and Trade Application
- **Entity**: Villon Farm Supply (agricultural retail, MSME)
- **Platform**: Windows desktop (WPF) — 1366×768 minimum

### Navigation Context
- **Active Module**: Purchasing | **Active Page**: Purchase Orders
- **Sidebar Pages**: Dashboard, Suppliers, Purchase Requests, **Purchase Orders**, Receiving, Payables, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online

### Color Palette
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`
- Status: Draft=`#E0E0E0`, Pending=`#FFF3E0`, Approved=`#E8F5E9`, Partially Received=`#E3F2FD`, Fully Received=`#E0F2F1`, Void=`#F5F5F5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: PO Form (Create/Edit)
**Fields — 2-column layout:**

| Field | Type | Required |
|-------|------|----------|
| PO # | Auto-generated (PO-YYYY-NNNN) | Read-only |
| PO Date | Date picker (default: today) | Yes |
| Supplier | Searchable dropdown | Yes |
| Expected Delivery | Date picker | No (must be ≥ PO Date) |
| Payment Terms | Text (auto-filled from supplier) | No |
| Shipping Address | Multiline (default: store address) | No |
| Notes | Multiline (max 500 chars) | No |

- "Quick Add Supplier" inline button next to supplier dropdown.
- From PR conversion: header pre-populated, source PR reference displayed.
- `Ctrl+S` to save, `Escape` to cancel.

### Component: PO Line Items
**Columns:**

| Column | Editable | Width |
|--------|----------|-------|
| # | No (auto) | 40px |
| Item | Yes (searchable from Item Master) | 200px |
| Description | Yes | 150px |
| Qty | Yes | 80px |
| Unit Price | Yes (₱) | 100px |
| Discount % | Yes | 80px |
| Line Total | No (calculated) | 120px |
| Remove | Yes | 40px |

- Add row button at bottom. Tab navigation: Item → Qty → Price → Discount → next row.
- At least 1 line item required. Qty ≥ 1, Price ≥ 0.
- Line Total = Qty × Unit Price × (1 - Discount%).

### Component: PO Summary Footer
- Pinned to bottom below line items.
- Shows: Subtotal, Discount Total, Tax (12% VAT), **Grand Total** (large, bold).
- Grand Total = Subtotal - Discount + Tax.

### Component: PO Approval Panel
- Visible for Pending/Approved/Rejected status.
- Approve/Reject buttons. Mandatory reason on reject. Approval history log.
- Manager can approve. Clerk cannot self-approve.

### Component: PO Status Badge
- Draft (gray), Pending Approval (amber), Approved (green), Partially Received (blue), Fully Received (teal), Void (black).

### Component: PO Print Action
- "Print PO" button generates A4 printable document.

### Component: PO Filters (for list view)
| Filter | Default |
|--------|---------|
| Status | All |
| Supplier | All |
| Date Range | Last 30 days |

### Component: PO List Table
**Columns:** PO #, Date, Supplier, Total, Status, Actions (View, Edit Draft, Void).

---

## §5. Business Rules (Extracted)

- BR-P1: Every PO must reference a valid Supplier.
- BR-P3: POs require approval before sending to supplier.
- BR-P6: Approved/Received POs cannot be edited — only voided with new PO raised.
- BR-P9: PO-YYYY-NNNN format, auto-generated.

---

## §6. UI Generation Scope

### Page Layout (Primary State: PO Form — Create)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ New Purchase Order                   [Status: Draft]            │
├───────────────────────────┬─────────────────────────────────────┤
│ PO #: PO-2026-0049       │ PO Date: 30/03/2026                │
│ Supplier: [▾ Search...]  │ Expected Delivery: [Date picker]    │
│ [+ Quick Add Supplier]   │ Payment Terms: Net 30               │
│ Shipping Address: [...]  │ Notes: [...]                        │
├───────────────────────────┴─────────────────────────────────────┤
│ LINE ITEMS                                          [+ Add Row] │
│ # │ Item          │ Desc     │ Qty │ Price   │ Disc │ Total    │
│ 1 │ NPK 14-14-14  │ 50kg bag │ 20  │ ₱850.00 │ 0%   │₱17,000  │
│ 2 │ Urea 46-0-0   │ 50kg bag │ 15  │ ₱720.00 │ 5%   │₱10,260  │
│ 3 │ Tomato Seeds   │ Pack 50g │ 100 │ ₱45.00  │ 0%   │₱4,500   │
├─────────────────────────────────────────────────────────────────┤
│                              Subtotal:     ₱31,760.00          │
│                              Discount:     -₱540.00            │
│                              VAT (12%):    ₱3,746.40           │
│                              GRAND TOTAL:  ₱34,966.40          │
├─────────────────────────────────────────────────────────────────┤
│ [Cancel]                         [Save Draft] [Submit for Approval] │
└─────────────────────────────────────────────────────────────────┘
```

---

## §7. Layout Expectations

- **Form Header**: 2-column grid. PO # and Supplier on left. Date and terms on right.
- **Line Items**: Full-width table below header. 36px row height. Tab-navigable.
- **Summary Footer**: Right-aligned with labels left and amounts right. Grand Total in 18px bold.
- **Action Bar**: Bottom-pinned. Cancel left, Save Draft + Submit right.

---

## §8. Component Expectations

### Sample PO Header
- PO #: PO-2026-0049 (auto)
- Supplier: Agri-Plus Supplies (selected)
- Date: 30/03/2026
- Expected Delivery: 15/04/2026
- Payment Terms: Net 30 (auto-filled from supplier)

### Sample Line Items (3 rows)
| # | Item | Description | Qty | Unit Price | Discount | Line Total |
|---|------|-------------|-----|-----------|----------|------------|
| 1 | NPK Fertilizer 14-14-14 | 50kg bag | 20 | ₱850.00 | 0% | ₱17,000.00 |
| 2 | Urea Fertilizer 46-0-0 | 50kg bag | 15 | ₱720.00 | 5% | ₱10,260.00 |
| 3 | Tomato Seeds (Diamante F1) | Pack 50g | 100 | ₱45.00 | 0% | ₱4,500.00 |

### Summary
- Subtotal: ₱31,760.00
- Discount: -₱540.00
- VAT (12%): ₱3,746.40
- **Grand Total: ₱34,966.40**

---

## §9. Interaction Expectations

- Tab navigation: PO Date → Supplier → Delivery → Item 1 → Qty 1 → Price 1 → next.
- `Ctrl+S` saves draft. `Escape` cancels. `Enter` on last row adds new row.
- Supplier dropdown search is debounced. "+ Quick Add Supplier" opens modal.

---

## §10. Do Not Assume

- Do NOT add attachment upload to POs.
- Do NOT add approval buttons on the create form — approval happens after submission.
- Do NOT show receiving information on the PO form — that is a separate page.
- Do NOT add a "Send to Supplier" email button — POs are printed, not emailed.

---

## §11. Required Output Quality Standard

- Production-ready form. Agricultural product names. Filipino supplier. ₱ values.
- Line items table must show 3+ rows. Summary footer must show calculated totals.
- "Purchase Orders" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Forms: 2-column, labels above. Tables: alternating rows.
- Primary button: `#4A6741`. Sidebar: `#2C3E2C`. Background: `#FAFAF5`.

---

## §13. Fallback Behavior If Context Is Missing

- If item search cannot populate, show text input for item name.
- If VAT calculation is unclear, use 12% as the fixed rate.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
- Do NOT design screens for other modules.
