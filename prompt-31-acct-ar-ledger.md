## §1. Role & Instruction

Generate the **AR Ledger** (Accounts Receivable Subsidiary Ledger) — showing all customer receivables with a payment recording modal and GL reconciliation.

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
