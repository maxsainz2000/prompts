## §1. Role & Instruction

Generate the **Audit Trail** page — the immutable, cross-module log of all data changes in the system. This is OWASP DA10 (Insufficient Logging) compliance and the system's forensic investigation tool.

---

## §2. System Objective

Provide a complete, tamper-proof audit log of every create, update, and delete operation across all 4 modules — enabling security review, regulatory compliance, and forensic investigation of data discrepancies.

---

## §3–§4. Context & Documentation

### Navigation: Accounting → Audit Trail

### Component: Audit Log Table
**Columns:**

| Column | Sortable | Width |
|--------|----------|-------|
| Timestamp | Yes | 140px |
| Module | Yes | 100px |
| Entity | Yes | 120px |
| Action | Yes | 70px |
| Record ID | No | 130px |
| User | Yes | 120px |
| Summary | No | flex |

- Actions: Created, Updated, Deleted, Approved, Rejected, Voided, Posted.
- Module: Purchasing, Inventory, POS, Accounting.
- Color-coded action badges.

### Component: Audit Filters
| Filter | Default |
|--------|---------|
| Date Range | Today |
| Module | All |
| Action | All |
| User | All |
| Entity | All |

### Component: Audit Detail Modal
- Opened on row click.
- Shows: Full record before/after change, field-level diff (old value → new value), timestamp, user, IP/session info.
- Before/after displayed in a side-by-side diff view with highlights on changed fields.

---

## §6. UI Generation Scope

### Page Layout

```
CONTENT AREA:
┌─────────────────────────────────────────────────────────────────┐
│ Audit Trail                                                     │
│ [Today ▾] [All Modules ▾] [All Actions ▾] [All Users ▾]       │
├─────────────────────────────────────────────────────────────────┤
│ Timestamp     │Module │Entity  │Action │Record      │User      │Summary│
│───────────────┼───────┼────────┼───────┼────────────┼──────────┼───────│
│30/03 14:22:05│Invent.│Item    │Updated│ITM-0042    │Maria S.  │Price changed│
│30/03 14:20:30│Purch. │PO      │Approved│PO-2026-0047│Maria S. │Approved PO  │
│30/03 11:05:12│POS    │Sale    │Created│SALE-0893   │Ana R.    │New sale     │
│30/03 10:45:00│Acct.  │JE      │Posted │JE-2026-0145│Maria S. │JE posted    │
│30/03 09:30:22│Invent.│Stock   │Updated│ITM-0089    │System    │Stock adj.   │
│30/03 08:55:10│POS    │Sale    │Voided │SALE-0887   │Ana R.    │Sale voided  │
│ ...                                                             │
├─────────────────────────────────────────────────────────────────┤
│ Showing 1-50 of 2,341 entries               ← 1 2 3 … → pages │
└─────────────────────────────────────────────────────────────────┘
```

### Detail Modal (on click — shows old → new values)
```
┌─────────────────────────────────────────────────────────────────┐
│ Audit Detail: ITM-0042 Updated by Maria Santos                 │
│ Timestamp: 30/03/2026 14:22:05                                 │
├──────────────────────────┬──────────────────────────────────────┤
│ BEFORE                   │ AFTER                                │
│ Selling Price: ₱820.00   │ Selling Price: ₱850.00 ← Changed   │
│ Updated At: 28/03/2026   │ Updated At: 30/03/2026              │
│ (all other fields same)  │                                      │
├──────────────────────────┴──────────────────────────────────────┤
│                                                      [Close]   │
└─────────────────────────────────────────────────────────────────┘
```

---

## §5. Business Rules (Extracted)

- Audit logs are **append-only** — never modified or deleted.
- Every create, update, delete records: timestamp, user, module, entity, action, old value, new value.
- Accessible centrally from the Accounting module.

---

## §10. Do Not Assume

- Do NOT add audit log editing or deletion.
- Do NOT add log export (that's via reports).
- Do NOT add real-time streaming — logs refresh on page load.
- Do NOT add an "undo" action from the audit trail.

---

## §11. Required Output Quality Standard

- Production-ready. Cross-module entries. Action badges color-coded.
- Before/after diff clearly highlighted in detail modal.
- "Audit Trail" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Action: Created=green, Updated=blue, Deleted=red, Approved=green, Voided=black.
- Module badges: Purchasing=blue, Inventory=green, POS=orange, Accounting=purple.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
