## §1. Role & Instruction

Generate the **AR Ledger** (Accounts Receivable Subsidiary Ledger) — showing all customer receivables with a payment recording modal and GL reconciliation.

---

## §2. System Objective

Provide a customer-level view of all receivables from credit sales, enable payment collection recording, and reconcile against the GL AR control account (Account 1130).

---

## §3–§4. Context & Documentation

### Navigation: Accounting → AR Ledger

**AR Subsidiary Table:** Customer, Opening, Charges (credit sales), Collections, Closing Balance, Aging.
**Payment Recording Modal:** Customer (display), Outstanding Balance, Payment Amount (≤ outstanding), Date, Method, Reference.
**Reconciliation Panel:** Subsidiary Total vs GL Balance (1130).
**Customer Filter:** Filter by customer. Date range.

---

## §6. UI Generation Scope

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ AR Subsidiary Ledger                [March 2026 ▾]             │
├─────────────────────────────────────────────────────────────────┤
│ Customer       │Opening│Charges│Collected│Balance │ Aging       │
│────────────────┼───────┼───────┼─────────┼────────┼─────────────│
│ Pedro Reyes    │₱2,000 │₱3,200 │₱1,400   │₱3,800  │ 1-30 days  │
│ Roberto Garcia │₱3,500 │₱2,500 │₱1,000   │₱5,000  │ 31-60 days │
│ Julio Santos   │₱4,000 │₱3,400 │₱2,200   │₱5,200  │ Current    │
│ Carmen Tan     │₱1,500 │₱0     │₱0       │₱1,500  │ 61-90 days │
│────────────────┼───────┼───────┼─────────┼────────│            │
│ TOTAL          │₱11,000│₱9,100 │₱4,600   │₱15,500 │            │
├─────────────────────────────────────────────────────────────────┤
│ RECONCILIATION                                                  │
│ Subsidiary: ₱15,500 │ GL (1130): ₱15,500 │ ✅ RECONCILED      │
└─────────────────────────────────────────────────────────────────┘
```

Actions per row: [Record Payment] [View History]

---

## §8. Component Expectations

Sample data as shown above. Aging column color-coded (Current=green, 1-30=blue, 31-60=amber, 61-90=orange, 90+=red).

---

## §10–§14. Standard Rules

- Do NOT add interest/late fees calculation.
- Do NOT allow overpayment.
- Production-ready. ₱ values. Reconciliation visible. "AR Ledger" active.
- Do NOT generate backend code. Do NOT generate mobile layouts.
