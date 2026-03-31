## §1. Role & Instruction

Generate the **Financial Reports** page — following the 5-component reporting structure PLUS the **mandatory Interpretation Panel** required for all Accounting reports.

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

Provide analytical financial reports (Trial Balance, Sales Journal accounting view, Purchases Journal accounting view, AR Aging, AP Aging, VAT Report, Shrinkage) with interpretation insights.

---

## §3–§4. Context & Documentation

### Navigation: Accounting → Financial Reports

### Available Reports
| Report | Chart | Interpretation |
|--------|-------|---------------|
| Trial Balance | Bar (Debits vs Credits by account type) | Balance verification insights |
| AR Aging | Stacked bar by customer | Collection risk analysis |
| AP Aging | Stacked bar by supplier | Payment obligation analysis |
| VAT Summary | Table only | Tax liability insights |
| Inventory Valuation (Acct view) | Pie by category | Inventory quality insights |
| COGS Analysis | Waterfall | Margin analysis |

### Universal Structure + Interpretation Panel
1. Report Selector tabs
2. Report Filters
3. Report Table
4. Report Chart
5. Export Actions
6. **Interpretation Panel** (Accounting-specific requirement)

---

## §6. UI Generation Scope

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ [Trial Balance] [AR Aging] [AP Aging] [VAT] [Inventory] [COGS]│
├─────────────────────────────────────────────────────────────────┤
│ [March 2026 ▾]                        [📊][📄][🖨️]           │
├──────────────────────┬──────────────────────────────────────────┤
│ Trial Balance Table  │ Chart + Interpretation Panel             │
│ Acct │Debit │Credit  │ [Bar chart: D vs C by type]              │
│──────┼──────┼────────│                                          │
│ 1110 │₱85K  │        │ 📊 Insights:                            │
│ 1130 │₱45K  │        │ • Total D = Total C ✅ Balanced         │
│ 1140 │₱1,245K│       │ • Asset-heavy B/S (typical retail)      │
│ 2110 │      │₱101K   │ • AP/AR ratio: 2.24 — monitor payables  │
│ ...                   │                                          │
│──────┼──────┼────────│                                          │
│TOTAL │₱1,564K│₱1,564K│                                          │
└──────────────────────┴──────────────────────────────────────────┘
```

---

## §10. Do Not Assume

- The Interpretation Panel is MANDATORY — do NOT omit it.
- Do NOT add custom report builder.

---

## §11. Required Output Quality Standard

- Production-ready. ₱ values. Trial Balance must balance. Interpretation present.
- "Financial Reports" active in sidebar.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
