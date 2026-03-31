### §1. Role & Instruction

Generate the **General Ledger** page — the master record of all financial transactions filtered by account, showing running balances.

---

## §2. System Objective

Provide a detailed, chronological ledger view of all transactions for any selected account, with running balance calculation, enabling full audit trail review.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: Accounting | **Active Page**: General Ledger
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Ledger Table
**Columns:** Date, JE #, Description, Debit, Credit, Running Balance.
- Filtered by account (dropdown at top). Date range filter.
- Shows opening balance as first row. Running balance calculated per row.

### Component: Account Selector
- Dropdown from COA. Shows account # and name. Updates table on change.

### Component: Ledger Detail Drawer
- Click a JE # to see the full journal entry context (all lines, not just this account's line).

---

## §6. UI Generation Scope

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ General Ledger                                                  │
│ Account: [1110 Cash on Hand ▾]  │ [March 2026 ▾]              │
├─────────────────────────────────────────────────────────────────┤
│ Date     │ JE #       │ Description       │ Debit  │Credit│Balance│
│──────────┼────────────┼───────────────────┼────────┼──────┼───────│
│          │            │ Opening Balance   │        │      │₱85,200│
│ 02/03/26 │ JE-0120    │ Sale cash receipt  │₱4,200  │      │₱89,400│
│ 05/03/26 │ JE-0125    │ AP Payment to Agri │       │₱25K  │₱64,400│
│ ...                                                            │
│ 30/03/26 │ JE-0145    │ Sale cash receipt  │₱3,835  │      │₱85,200│
└─────────────────────────────────────────────────────────────────┘
```

---

## §8. Component Expectations

### Sample: Account 1110 Cash on Hand (6 rows)
| Date | JE # | Description | Debit | Credit | Balance |
|------|------|-------------|-------|--------|---------|
| — | — | Opening Balance | — | — | ₱78,000.00 |
| 02/03/2026 | JE-2026-0120 | Sale cash receipt | ₱4,200.00 | — | ₱82,200.00 |
| 05/03/2026 | JE-2026-0125 | AP Payment (Agri-Plus) | — | ₱25,000.00 | ₱57,200.00 |
| 15/03/2026 | JE-2026-0132 | Sale cash receipt | ₱12,500.00 | — | ₱69,700.00 |
| 22/03/2026 | JE-2026-0138 | AP Payment (Manila Seed) | — | ₱13,500.00 | ₱56,200.00 |
| 30/03/2026 | JE-2026-0145 | Sale cash receipt | ₱29,000.00 | — | ₱85,200.00 |

---

## §10. Do Not Assume

- Do NOT add ledger editing — the GL is read-only (edits happen in JE).
- Do NOT add trial balance here — that's a separate report.

---

## §11–§14. Standard Rules

- Production-ready. ₱ values. Running balance always calculated. "General Ledger" active in sidebar.
- Typography: Inter. Tables: alternating rows. Debit=left, Credit=right.
- Do NOT generate backend code. Do NOT generate mobile layouts.
