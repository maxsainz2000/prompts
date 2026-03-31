## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Transaction History** page — a searchable, filterable log of all completed, voided, and returned sales transactions.

---

## §2. System Objective

Enable the Manager to review all past sales transactions, view transaction details (items, payment, cashier), void completed sales if needed, and reprint receipts.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: POS/Sales | **Active Page**: Transaction History
- **Sidebar**: Dashboard, Transaction, **Transaction History**, Returns, Customers, Pricing, Cashier Mgmt, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: History List Table
**Columns:**

| Column | Sortable | Width |
|--------|----------|-------|
| Transaction # | Yes | 130px |
| Date/Time | Yes | 140px |
| Cashier | Yes | 120px |
| Customer | No | 130px |
| Items | No | 50px |
| Total | Yes | 110px |
| Payment | No | 80px |
| Status | Yes | 90px |

- Status: Completed (green), Voided (black/gray), Returned (amber).
- Default sort: Date/Time descending. Pagination: 25 rows/page.

### Component: History Filters
| Filter | Default |
|--------|---------|
| Date Range | Today |
| Cashier | All |
| Status | All |
| Payment Method | All |
| Customer | All |

### Component: History Detail Drawer
- Slides from right (~40%) on row click.
- Sections: Transaction header (date, cashier, customer), Line items (with prices), Payment details, Receipt reprint button.
- Actions: Void Transaction (Manager only), Reprint Receipt.

### Component: Void Modal
- Triggered from detail drawer. Mandatory reason.
- "Void Transaction" + "Cancel" buttons.

### Component: Reprint Action
- Button in detail drawer. Regenerates receipt for the selected transaction.

---

## §6. UI Generation Scope

### Page Layout (Primary State: List with Detail Drawer Open)

```
CONTENT AREA:
┌──────────────────────────────────────────────────────────────────┐
│ Transaction History                                              │
│ [Today ▾] [All Cashiers ▾] [All Status ▾] [All Payment ▾]      │
├──────────────────────────────────────┬───────────────────────────┤
│ Txn #       │Time    │Cashier│Total │ SALE-2026-0892            │
│─────────────┼────────┼───────┼──────│ 30/03/2026 10:15 AM      │
│SALE-2026-0893│10:42AM│Ana   │₱3,835│ Cashier: Ana Reyes        │
│SALE-2026-0892│10:15AM│Ana   │₱1,280│ Customer: Walk-in         │
│SALE-2026-0891│09:40AM│Ana   │₱2,450│                            │
│SALE-2026-0890│09:12AM│Carlos│₱890  │ Items:                     │
│SALE-2026-0889│08:55AM│Carlos│₱4,200│ • NPK 14-14-14 ×1 ₱850   │
│SALE-2026-0888│08:30AM│Carlos│₱1,650│ • Tomato Seeds ×5 ₱225    │
│VOID-2026-0887│08:10AM│Ana   │₱520  │ • Work Gloves ×2 ₱240    │  
│                                      │                            │
│                                      │ Total: ₱1,315.00          │
│                                      │ Payment: Cash ₱1,500      │
│                                      │ Change: ₱185.00           │
│                                      │                            │
│                                      │ [Void] [Reprint Receipt]  │
├──────────────────────────────────────┴───────────────────────────┤
│ Showing 1-25 of 893 transactions         ← 1 2 3 … 36 → pages  │
└──────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample Table (7 rows)
| Txn # | Date/Time | Cashier | Customer | Items | Total | Payment | Status |
|-------|-----------|---------|----------|-------|-------|---------|--------|
| SALE-2026-0893 | 30/03 10:42 | Ana Reyes | Walk-in | 4 | ₱3,835.00 | Cash | ✅ Complete |
| SALE-2026-0892 | 30/03 10:15 | Ana Reyes | Walk-in | 3 | ₱1,280.00 | Cash | ✅ Complete |
| SALE-2026-0891 | 30/03 09:40 | Ana Reyes | Walk-in | 2 | ₱2,450.00 | Cash | ✅ Complete |
| SALE-2026-0890 | 30/03 09:12 | Carlos M. | Walk-in | 1 | ₱890.00 | Cash | ✅ Complete |
| SALE-2026-0889 | 30/03 08:55 | Carlos M. | J. Santos | 5 | ₱4,200.00 | Credit | ✅ Complete |
| SALE-2026-0888 | 30/03 08:30 | Carlos M. | Walk-in | 3 | ₱1,650.00 | Cash | ✅ Complete |
| VOID-2026-0887 | 30/03 08:10 | Ana Reyes | Walk-in | 1 | ₱520.00 | — | ⬛ Voided |

---

## §10. Do Not Assume

- Do NOT add transaction editing — completed sales are immutable.
- Do NOT add refund processing here — that's in Returns page.
- Do NOT add batch void functionality.

---

## §11. Required Output Quality Standard

- Production-ready. ₱ values. Filipino names. Status badges.
- "Transaction History" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Complete=green, Voided=gray/black, Returned=amber.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
