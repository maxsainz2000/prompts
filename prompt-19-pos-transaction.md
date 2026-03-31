## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **POS Transaction** screen — the single most critical and complex page in the entire VISTA system. This is where sales happen. It has 11 components and must support full keyboard-first workflow for rapid transaction processing.

**This screen determines whether the POS module is operationally viable.**

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

Exception: This screen operates in POS full-width mode. The sidebar is intentionally hidden. Preserve only the top bar and status bar from the reference.

## §2. System Objective

Enable a cashier to rapidly process sales transactions: scan/search items, build a cart, apply discounts, accept payment, calculate change, and generate receipts — all without requiring a mouse. Speed and accuracy are paramount.

---

## §3. Application Context (Embedded)

### System Identity
- **Application**: VISTA | **Entity**: Villon Farm Supply | **Platform**: WPF Desktop (1366×768)
- **Design Language**: High-density, keyboard-first, maximum throughput.

### Navigation Context
- **Active Module**: POS/Sales | **Active Page**: Transaction
- **Sidebar**: Dashboard, **Transaction**, Transaction History, Returns, Customers, Pricing, Cashier Mgmt, Reports
- **User**: Ana Reyes / Cashier | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

### Keyboard-First Design (from `modules/spec.md` §4.4)
All transactional pages must support full keyboard workflows. Mouse is optional, never required.

| Key | Action |
|-----|--------|
| `F1` | Help / shortcut reference |
| `F2` | Customer lookup |
| `F4` | Apply discount |
| `F5` | Void item |
| `F8` | Subtotal / payment |
| `F10` | Complete transaction |
| `F12` | Void transaction |
| `Enter` | Add item to cart |
| `Escape` | Cancel / back |

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Item Lookup Bar
- Position: Top of left panel, full-width.
- Search by item code, barcode, or name. Debounced (200ms — faster than standard 300ms).
- Autocomplete dropdown: shows Item Name, Code, Price, Stock Qty.
- `Enter` adds the selected item to cart with qty=1.
- Always focused when no modal is open.

### Component: Cart / Line Items
- Position: Left panel (~60%), below item lookup.
- **Columns:**

| Column | Width |
|--------|-------|
| # | 30px |
| Item Name | flex |
| Qty (editable) | 60px |
| Price | 80px |
| Discount | 60px |
| Total | 90px |
| Void | 30px |

- Tab selects qty field for editing. `+`/`-` keys adjust qty.
- Voided items show strikethrough, remain visible but excluded from total.
- Newest item at bottom. Scrollable.

### Component: Cart Summary
- Pinned below cart. Shows: Item Count, Subtotal, Discount Total, VAT, **Grand Total** (large, bold, 24px+).
- Grand Total is the most prominent element on the screen.

### Component: Payment Panel
- Position: Right panel (~40%).
- **Payment Methods:** Cash, Credit (customer account), Split Payment.
- **Cash flow:**
  1. Grand Total displayed prominently
  2. "Amount Tendered" input field (large, numeric)
  3. Quick amount buttons: ₱50, ₱100, ₱200, ₱500, ₱1000, Exact
  4. Change calculation (auto, large display)

### Component: Change Calculator
- Auto-calculates: Change = Amount Tendered - Grand Total.
- Displays in large, bold text (green if positive, red if insufficient).
- Shows denomination breakdown (optional): 1×₱500, 2×₱100, 1×₱50.

### Component: Customer Selector
- Optional customer assignment (F2 shortcut).
- Searchable dropdown. "Walk-in" (default — no customer).
- If customer selected: shows name, credit limit, outstanding balance.

### Component: Transaction Status Bar
- Position: Bottom of right panel.
- Shows: Transaction #, Cashier, Shift, Time, Items in cart.

### Component: Receipt Preview
- Modal shown after payment completion.
- Shows: Store name, date/time, items, totals, payment, change.
- "Print Receipt" button. "New Transaction" button.

### Component: Keyboard Shortcut Overlay
- `F1` toggles a semi-transparent overlay showing all shortcuts.
- Dismisses on any key press.

### Component: Void Transaction Modal
- `F12` triggers. Confirmation with mandatory reason.
- Voids entire transaction and returns items to stock.

### Component: Discount Modal
- `F4` triggers. Options: Per-item %, Per-item fixed, Transaction-level %.
- Senior Citizen / PWD discount presets (Philippine law).

---

## §5. Business Rules (Extracted)

- Sale completion triggers `SaleCompleted` event → Inventory deduction + Accounting revenue.
- Credit sales require customer selection and credit limit check.
- Void transaction publishes `TransactionVoided` event → Inventory return.
- Active cashier shift required — cannot transact without open shift.
- All cash tendered must be ≥ Grand Total (no negative change).

---

## §6. UI Generation Scope

### Page Layout (Primary State: Active Cart with Items)

```
FULL CONTENT AREA (no sidebar visible — POS takes full width):
┌────────────────────────────────────┬───────────────────────────────┐
│ [🔍 Scan or search item...]       │  PAYMENT                      │
│                                    │                               │
│ CART                               │  Grand Total                  │
│ #│ Item              │Qty│Price│Tot│  ₱2,835.00                   │
│ 1│ NPK 14-14-14      │ 2 │₱850 │₱1,700│                          │
│ 2│ Tomato Seeds       │ 5 │₱45  │₱225  │  Amount Tendered          │
│ 3│ Knapsack Sprayer   │ 1 │₱1550│₱1,550│  [₱3,000.00           ]  │
│ 4│ Work Gloves        │ 3 │₱120 │₱360  │                          │
│                                    │  [₱50] [₱100] [₱500] [₱1K]  │
│                                    │  [Exact]                      │
│──────────────────────────────────  │                               │
│ Items: 4  │  Subtotal: ₱3,835.00  │  CHANGE                      │
│ Discount: -₱0.00                   │  ₱165.00                     │
│ VAT (12%): ₱0.00 (VAT-inclusive)   │  (1×₱100, 1×₱50, 1×₱10,    │
│ GRAND TOTAL: ₱3,835.00            │   1×₱5)                      │
│                                    │                               │
│                                    │  [F8 Subtotal] [F10 Complete]│
├────────────────────────────────────┴───────────────────────────────┤
│ SALE-2026-0893 │ Cashier: Ana Reyes │ Shift: AM │ 10:42 AM       │
└───────────────────────────────────────────────────────────────────┘
```

**IMPORTANT**: The POS Transaction screen should **collapse the sidebar** to maximize screen real estate. The sidebar is replaced by a thin module indicator or is hidden. All navigation happens via keyboard shortcuts in POS mode.

---

## §7. Layout Expectations

- **Left Panel (60%):** Item lookup bar (top, 48px), Cart table (middle, fills), Cart summary (bottom, ~80px).
- **Right Panel (40%):** Grand Total (top, 80px, prominent), Payment input (middle), Change display (bottom).
- **Status Bar**: Full width, bottom, 32px.
- **No sidebar**: POS mode hides sidebar to maximize transaction space.

---

## §8. Component Expectations

### Sample Cart (4 items)
| # | Item | Qty | Price | Total |
|---|------|-----|-------|-------|
| 1 | NPK Fertilizer 14-14-14 (50kg) | 2 | ₱850.00 | ₱1,700.00 |
| 2 | Tomato Seeds (Diamante F1) | 5 | ₱45.00 | ₱225.00 |
| 3 | Knapsack Sprayer 16L | 1 | ₱1,550.00 | ₱1,550.00 |
| 4 | Work Gloves (Leather) | 3 | ₱120.00 | ₱360.00 |

### Cart Summary
- Items: 4 | Subtotal: ₱3,835.00 | Discount: ₱0.00 | **Grand Total: ₱3,835.00**

### Payment
- Grand Total: ₱3,835.00 (large, bold, 28px)
- Amount Tendered: ₱4,000.00
- Change: ₱165.00 (green, bold, 24px)

### Transaction Status
- SALE-2026-0893 | Ana Reyes | AM Shift | 10:42 AM | 4 items

---

## §9. Interaction Expectations

- **Item lookup**: Always focused. Type → autocomplete → Enter adds item.
- **Qty adjustment**: Click qty cell or Tab to it. Type new value or +/- keys.
- **F8**: Opens payment section / focuses "Amount Tendered" field.
- **F10**: Completes transaction (only when tendered ≥ total).
- **F12**: Void entire transaction (confirmation modal).
- **F4**: Open discount modal for selected cart item.
- **Escape**: Clear search / cancel current modal.

---

## §10. Do Not Assume

- Do NOT add loyalty points or rewards.
- Do NOT add online payment methods (GCash, etc.) — cash and credit only.
- Do NOT add item image thumbnails in the cart (space critical).
- Do NOT add a secondary monitor/customer display.
- Do NOT show the sidebar — POS mode runs full-width.
- Do NOT add receipt printing configuration — that's in settings.

---

## §11. Required Output Quality Standard

- This must look like a **real POS terminal** — not a web form.
- Grand Total must be the single most visually dominant element on screen.
- Keyboard shortcut hints must be visible (F-key labels on buttons).
- Cart must feel like rapid-fire data entry, not a shopping cart.
- "POS/Sales" module context shown in status bar, not in a sidebar tab.
- Agricultural product names. ₱ values.

---

## §12. UI Consistency Rules

- Typography: Inter. Grand Total: 28px bold. Change: 24px bold.
- Cart: alternating rows, 32px row height (compact for POS).
- Buttons: Quick amount buttons use outlined style. Complete = primary green.
- Background: slightly darker than standard (#F0F0EA) for POS focus mode.

---

## §13. Fallback Behavior If Context Is Missing

- If denomination breakdown cannot calculate, show only total change amount.
- If customer lookup is not available, default to "Walk-in Customer".

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
- Do NOT design the full receipt — only the on-screen preview reference.
