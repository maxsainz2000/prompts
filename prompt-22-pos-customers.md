## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Customers** page — a list-detail master data page for managing customer records, with an integrated AR (Accounts Receivable) widget showing outstanding credit balances.

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

Enable staff to manage customer records and monitor customer credit balances — supporting the credit sales workflow where customers can buy on account.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: POS/Sales | **Active Page**: Customers
- **Sidebar**: Dashboard, Transaction, Transaction History, Returns, **Customers**, Pricing, Cashier Mgmt, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Customer List Table
**Columns:** Customer Code, Name, Phone, Credit Limit, Outstanding Balance, Status.
- Default sort: Name ascending. Pagination: 20 rows/page.

### Component: Customer Search Bar
- Debounced search by name, code, phone. "+ New Customer" button.

### Component: Customer Form
**Fields:** Customer Code (auto: CUST-NNNN), Name (required), Phone, Email, Address, Credit Limit (₱), Notes, Status.

### Component: Customer Detail Panel
- Sections: Header (name, code, status), Contact info, Credit (limit, outstanding, available), Purchase History (last 10 transactions), AR Widget (aging: Current, 1-30, 31-60, 61-90, 90+).

### Component: AR Widget
- Mini aging buckets within the detail panel.
- Shows outstanding balance by aging period.
- Color-coded: green → red progression.

---

## §6. UI Generation Scope

### Page Layout (Primary State: List with Detail Panel)

```
CONTENT AREA:
┌───────────────────────────────────┬──────────────────────────────┐
│ [🔍 Search customers...] [+ New] │                               │
│ Customer List Table               │ Customer Detail               │
│ Code│Name        │Phone │Balance  │ CUST-0005 Julio Santos       │
│ 0001│Maria San...│0917..│₱0.00   │ Credit: ₱10,000 / ₱5,200 used│
│ 0005│Julio San...│0918..│₱5,200  │ AR Aging:                     │
│ ...                               │ [Current][1-30][31-60][61-90]│
│                                   │ ₱2,200  │₱1,800│₱800 │₱400  │
│                                   │ Purchase History...           │
└───────────────────────────────────┴──────────────────────────────┘
```

---

## §8. Component Expectations

### Sample Table (6 rows)
| Code | Name | Phone | Credit Limit | Outstanding | Status |
|------|------|-------|--------------|-------------|--------|
| CUST-0001 | Maria Santos | 0917-555-1001 | ₱15,000.00 | ₱0.00 | Active |
| CUST-0002 | Pedro Reyes | 0918-555-1002 | ₱10,000.00 | ₱3,800.00 | Active |
| CUST-0003 | Elena Cruz | 0919-555-1003 | ₱8,000.00 | ₱0.00 | Active |
| CUST-0004 | Roberto Garcia | 0920-555-1004 | ₱5,000.00 | ₱5,000.00 | Active |
| CUST-0005 | Julio Santos | 0921-555-1005 | ₱10,000.00 | ₱5,200.00 | Active |
| CUST-0006 | Carmen Tan | 0922-555-1006 | ₱12,000.00 | ₱1,500.00 | Inactive |

### Detail Panel (CUST-0005)
- Credit Limit: ₱10,000.00 | Outstanding: ₱5,200.00 | Available: ₱4,800.00
- AR: Current ₱2,200 | 1-30 ₱1,800 | 31-60 ₱800 | 61-90 ₱400

---

## §10. Do Not Assume

- Do NOT add loyalty/rewards points.
- Do NOT add customer groups or tiers.
- Do NOT add payment collection from this page.

---

## §11. Required Output Quality Standard

- Production-ready. Filipino names. ₱ values. AR aging visible.
- "Customers" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Lists: alternating rows. AR aging: green→red color scale.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
