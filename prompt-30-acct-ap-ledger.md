## §1. Role & Instruction

Generate the **AP Ledger** (Accounts Payable Subsidiary Ledger) — showing all payable obligations by supplier with reconciliation against the General Ledger AP control account.

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

Provide a supplier-level view of all payables, enable reconciliation of the subsidiary ledger total against the GL AP control account (Account 2110), and flag discrepancies.

---

## §3–§4. Context & Documentation

### Navigation: Accounting → AP Ledger
### Components

**AP Subsidiary Table:** Supplier, Opening, Charges (new AP), Payments, Closing Balance.
**Reconciliation Panel:** Subsidiary Total vs GL Balance (2110). Match=green, Mismatch=red with difference.
**Supplier Filter:** Filter by supplier. Date range.

---

## §6. UI Generation Scope

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ AP Subsidiary Ledger                [March 2026 ▾]             │
├─────────────────────────────────────────────────────────────────┤
│ Supplier      │Opening  │Charges  │Payments │Closing Balance    │
│───────────────┼─────────┼─────────┼─────────┼──────────────────│
│ Agri-Plus     │₱20,000  │₱45,200  │₱25,000  │₱40,200          │
│ Manila Seed   │₱15,000  │₱28,500  │₱13,500  │₱30,000          │
│ FarmTech      │₱10,000  │₱15,800  │₱0       │₱25,800          │
│ Others (4)    │₱8,000   │₱12,200  │₱15,000  │₱5,200           │
│───────────────┼─────────┼─────────┼─────────┼──────────────────│
│ TOTAL         │₱53,000  │₱101,700 │₱53,500  │₱101,200         │
├─────────────────────────────────────────────────────────────────┤
│ RECONCILIATION                                                  │
│ Subsidiary Total: ₱101,200.00                                  │
│ GL Account 2110: ₱101,200.00                                   │
│ Difference: ₱0.00  ✅ RECONCILED                               │
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

As shown in layout above. Summary row at bottom. Reconciliation panel prominent.

---

## §10–§14. Standard Rules

- Do NOT add payment processing here (that's in Purchasing → Payables).
- Production-ready. ₱ values. Reconciliation status prominent.
- Typography: Inter. Reconciled=green, Unreconciled=red with difference amount.
- Do NOT generate backend code. Do NOT generate mobile layouts.
