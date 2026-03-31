## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Returns** form view — where staff processes merchandise returns against original sale transactions.

---

## §2. System Objective

Enable processing of customer returns: lookup the original sale, select items being returned, record the reason, calculate the refund, and trigger inventory re-entry and revenue reversal.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: POS/Sales | **Active Page**: Returns
- **Sidebar**: Dashboard, Transaction, Transaction History, **Returns**, Customers, Pricing, Cashier Mgmt, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Return Form
**Fields:**

| Field | Required |
|-------|----------|
| Return # (auto: RTN-YYYY-NNNN) | Read-only |
| Original Sale # (searchable) | Yes |
| Return Date (default: today) | Yes |
| Reason (dropdown: Defective, Wrong Item, Customer Changed Mind, Damaged, Other) | Yes |
| Reason Details | If "Other" |
| Processed By | Auto (current user) |

### Component: Return Line Items
- Pre-loaded from original sale.
- Checkbox per item to select which items are being returned.
- Editable return qty (≤ original qty - previously returned).
- Non-returnable items grayed out.

### Component: Refund Summary
- Total Refund Amount (sum of selected return items).
- Refund Method: Cash, Credit to Customer Account.
- Refund approval required for amounts > ₱5,000.

### Component: Return List Table
- Past returns: RTN #, Date, Original Sale #, Items, Refund Amount, Status.

### Component: Return Reason Dropdown
- Standardized reasons for reporting and analytics.

---

## §6. UI Generation Scope

### Page Layout (Primary State: Return Form)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ Process Return                              [RTN-2026-0013]    │
├───────────────────────────┬─────────────────────────────────────┤
│ Original Sale: [🔍 SALE- │ Return Date: 30/03/2026             │
│  2026-0889]              │ Reason: [Defective ▾]               │
│ Customer: Julio Santos    │ Processed By: Maria Santos          │
├───────────────────────────┴─────────────────────────────────────┤
│ SELECT ITEMS TO RETURN                                          │
│ ☑ │ Item                │ Orig Qty │ Returned │ Return Now │   │
│ ☑ │ NPK 14-14-14 (50kg) │    3     │    0     │    2       │   │
│ ☐ │ Machete #5           │    1     │    0     │    —       │   │
│ ☑ │ Tomato Seeds (50g)   │   10     │    0     │    5       │   │
├─────────────────────────────────────────────────────────────────┤
│ Refund Summary                                                  │
│ Items Returned: 2 items (7 units)                              │
│ Refund Amount: ₱1,925.00                                       │
│ Refund Method: [Cash ▾]                                        │
├─────────────────────────────────────────────────────────────────┤
│ [Cancel]                                   [Process Return]    │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample Data
- Return #: RTN-2026-0013
- Original Sale: SALE-2026-0889 (Julio Santos, ₱4,200.00)
- Reason: Defective

### Return Items
| Select | Item | Orig Qty | Previously Returned | Returning Now |
|--------|------|----------|--------------------|--------------:|
| ☑ | NPK Fertilizer 14-14-14 (50kg) | 3 | 0 | 2 |
| ☐ | Machete #5 Heavy Duty | 1 | 0 | — |
| ☑ | Tomato Seeds (Diamante F1) | 10 | 0 | 5 |

### Refund: ₱1,925.00 (2×₱850 + 5×₱45) via Cash

---

## §10. Do Not Assume

- Do NOT allow returns without original sale reference.
- Do NOT add exchange (return + new sale) as a single flow.
- Do NOT allow return qty > (original - previously returned).

---

## §11. Required Output Quality Standard

- Production-ready form. ₱ values. Checkbox selection clear.
- "Returns" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Forms: 2-column header. Checkboxes: standard WPF style.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
