## §1. Role & Instruction

Generate the **Financial Reports** page — following the 5-component reporting structure PLUS the **mandatory Interpretation Panel** required for all Accounting reports.

---

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
