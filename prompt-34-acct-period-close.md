## §1. Role & Instruction

Generate the **Period Close** page — a multi-step wizard that guides the Accountant through the monthly closing process: pre-close checklist, review, generate closing entries, and lock the period.

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

Ensure proper month-end closing: verify all transactions are posted, reconcile subsidiary ledgers, generate closing entries for revenue/expense accounts, and lock the period to prevent further modifications.

---

## §3–§4. Context & Documentation

### Navigation: Accounting → Period Close

### Component: Period Close Wizard (4 steps)

**Step 1 — Pre-Close Checklist:**
- ☑ All journal entries posted
- ☑ AP ledger reconciled
- ☑ AR ledger reconciled
- ☑ Physical count completed
- ☑ Bank reconciliation done
- ☐ items block progression until resolved.

**Step 2 — Review:**
- Summary: Revenue, Expenses, Net Income preview.
- Outstanding items warning list.

**Step 3 — Generate Closing Entries:**
- System generates: Revenue → Income Summary, Expense → Income Summary, Income Summary → Retained Earnings.
- Preview closing JEs before posting.

**Step 4 — Lock Period:**
- Confirm lock. Once locked, no JEs can be created/edited in this period.
- Shows: Period locked date, locked by user.

### Component: Period Timeline
- Visual timeline showing past closed periods and current open period.
- Jan ✅ → Feb ✅ → Mar 🔓 (current, open).

### Component: Period History Table
- Past closings: Period, Closed Date, Closed By, Net Income, Status.

---

## §6. UI Generation Scope

### Page Layout (Primary State: Step 1 — Pre-Close Checklist)

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ Period Close — March 2026                                      │
│ [Step 1: Checklist] → [Step 2: Review] → [Step 3: Close] → [4]│
├─────────────────────────────────────────────────────────────────┤
│ PRE-CLOSE CHECKLIST                                            │
│                                                                 │
│ ☑ All journal entries posted          (142 JEs, all posted)    │
│ ☑ AP subsidiary reconciled            (₱101,200 = ₱101,200 ✅)│
│ ☑ AR subsidiary reconciled            (₱15,500 = ₱15,500 ✅)  │
│ ☑ Physical count completed            (CNT-2026-0004, 30/03)  │
│ ☐ Bank reconciliation completed       ⚠️ Not yet done         │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│ Period Timeline: Jan ✅ → Feb ✅ → Mar 🔓 (open)              │
├─────────────────────────────────────────────────────────────────┤
│ [Cancel]                                 [Next: Review →]      │
│                              (blocked — 1 checklist item open)  │
└─────────────────────────────────────────────────────────────────┘
```

---

## §10. Do Not Assume

- Do NOT allow skipping checklist items.
- Do NOT allow period re-opening after lock (reversing entries for corrections).
- Do NOT add year-end close (v1 is monthly only).

---

## §11. Required Output Quality Standard

- Production-ready wizard. Clear step progression. Blocked state visible.
- "Period Close" active in sidebar.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
