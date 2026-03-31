## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Purchase Requests** list page within the **Purchase/Procurement** module. This is an approval-workflow page showing internal requests for goods with status tracking.

---

## §2. System Objective

Enable staff to create internal requests for merchandise and track their approval status. The Purchasing Clerk creates requests; the Manager reviews and approves or rejects them.

---

## §3. Application Context (Embedded)

### System Identity
- **Application**: VISTA — Villon's Integrated Supply and Trade Application
- **Entity**: Villon Farm Supply (agricultural retail, MSME)
- **Platform**: Windows desktop (WPF) — 1366×768 minimum
- **Design Language**: Professional, functional, data-dense.

### Navigation Context
- **Active Module**: Purchasing | **Active Page**: Purchase Requests
- **Sidebar Pages**: Dashboard, Suppliers, **Purchase Requests**, Purchase Orders, Receiving, Payables, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online

### Color Palette
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`
- Status: Draft=`#E0E0E0`, Pending Approval=`#FFF3E0`, Approved=`#E8F5E9`, Rejected=`#FFEBEE`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Request List Table
**Columns:**

| Column | Sortable | Width |
|--------|----------|-------|
| PR # | Yes | 130px |
| Date | Yes | 100px |
| Requested By | Yes | 150px |
| Description | No | 200px |
| Total Estimate | Yes | 120px |
| Status | Yes | 120px |
| Actions | No | 100px |

- Default sort: Date descending. Pagination: 20 rows/page.
- Actions: View, Edit (Draft only), Convert to PO (Approved only).
- Row click: opens PR detail or form in read-only mode.

### Component: Request Filters
| Filter | Type | Default |
|--------|------|---------|
| Status | Dropdown (All, Draft, Pending, Approved, Rejected) | All |
| Date Range | Date picker | Last 30 days |
| Requested By | Dropdown | All |

### Component: Request Form (Create/Edit)
**Fields:**

| Field | Required |
|-------|----------|
| PR # (auto: PR-YYYY-NNNN) | Read-only |
| Date (default: today) | Yes |
| Description/Purpose | Yes |
| Priority (Low/Medium/High) | No (default: Medium) |
| Notes | No |

Below the form header: **Request Line Items** component.
Bottom action bar: Save Draft, Submit for Approval, Cancel.

### Component: Request Line Items
**Columns:**

| Column | Width |
|--------|-------|
| Item Name (searchable from Item Master) | 200px |
| Description | 150px |
| Estimated Qty | 80px |
| Estimated Unit Price | 100px |
| Estimated Total (calculated) | 100px |
| Remove row | 40px |

- Add row button. Tab navigation between fields. At least 1 line item required.

### Component: Request Approval Panel
- Visible when status = Pending Approval
- Shows: Approve / Reject buttons, mandatory reason on reject, approval history
- Visibility: Manager can approve. Clerk cannot self-approve.
- On approve: status → Approved. On reject: status → Rejected with reason.

### Component: Request Status Badge
- Draft (gray), Pending Approval (amber), Approved (green), Rejected (red)
- Displayed in table rows and on the form header.

---

## §5. Business Rules (Extracted)

- BR-P2: Purchase Requests require approval before conversion to PO.
- BR-P9: PR reference numbers: PR-YYYY-NNNN format, auto-generated, sequential.
- Approved PRs can be converted to PO via "Convert to PO" action.
- Rejected PRs require a mandatory reason text.

---

## §6. UI Generation Scope

### Page Layout (Primary State: List View)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ Purchase Requests                        [+ New Request]        │
├─────────────────────────────────────────────────────────────────┤
│ [All ▾] [Last 30 Days ▾] [All Users ▾]           [Clear All]   │
├─────────────────────────────────────────────────────────────────┤
│ PR #    │ Date     │ Requested By │ Description │ Total│ Status │
│─────────┼──────────┼──────────────┼─────────────┼──────┼────────│
│ PR-2026-│28/03/2026│ Juan Dela    │ Fertilizer  │₱18.5K│Pending │
│ ...     │          │ Cruz         │ restock     │      │        │
├─────────────────────────────────────────────────────────────────┤
│ Showing 1-20 of 32                            ← 1 2 → (pages)  │
└─────────────────────────────────────────────────────────────────┘
```

---

## §7. Layout Expectations

- Page header with title "Purchase Requests" and "+ New Request" button top-right.
- Filter bar below header. Table fills remaining vertical space.
- Alternating row colors. Status badges inline.

---

## §8. Component Expectations

### Sample Data — Table (7 rows)
| PR # | Date | Requested By | Description | Estimate | Status |
|------|------|-------------|-------------|----------|--------|
| PR-2026-0015 | 28/03/2026 | Juan Dela Cruz | Fertilizer restock for planting season | ₱18,500.00 | Pending |
| PR-2026-0014 | 27/03/2026 | Carlos Mendoza | Seed inventory replenishment | ₱7,200.00 | Pending |
| PR-2026-0013 | 25/03/2026 | Ana Reyes | Pesticide supplies — pest outbreak | ₱12,400.00 | Approved |
| PR-2026-0012 | 23/03/2026 | Juan Dela Cruz | Garden tools restocking | ₱5,800.00 | Approved |
| PR-2026-0011 | 20/03/2026 | Carlos Mendoza | Knapsack sprayers (customer demand) | ₱9,600.00 | Rejected |
| PR-2026-0010 | 18/03/2026 | Ana Reyes | Animal feed — poultry line | ₱22,100.00 | Draft |
| PR-2026-0009 | 15/03/2026 | Juan Dela Cruz | Irrigation supplies | ₱14,350.00 | Approved |

---

## §9. Interaction Expectations

- "+ New Request" opens the PR form (full-page or modal).
- Row click opens PR in read-only detail view.
- "Edit" action available only for Draft status.
- "Convert to PO" action available only for Approved status.
- Filter changes immediately update the table.
- `Ctrl+N` for new request.

---

## §10. Do Not Assume

- Do NOT add bulk approval functionality — each PR is approved individually.
- Do NOT add attachment/file upload to purchase requests.
- Do NOT create a kanban/board view — list table only.
- Do NOT assume the form and list view are split-screen — the form replaces the list.

---

## §11. Required Output Quality Standard

- Production-ready desktop page. Filipino names. Agricultural product descriptions.
- ₱ currency format. Status badges with documented colors. 5–8 rows sample data.
- "Purchasing" module active, "Purchase Requests" page active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Status: Draft=`#E0E0E0`, Pending=`#FFF3E0`, Approved=`#E8F5E9`, Rejected=`#FFEBEE`.
- Tables: alternating rows, `#F5F5EE` headers. Buttons: Primary `#4A6741`. Sidebar: `#2C3E2C`.

---

## §13. Fallback Behavior If Context Is Missing

- If line items cannot be shown in the list view, display only the estimated total.
- If a user name is too long, truncate with ellipsis.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
- Do NOT design screens for other modules.
