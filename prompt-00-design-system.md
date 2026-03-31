## §1. Role & Instruction

You are a visual design system architect for a Windows desktop merchandising application.
Your task is to define the foundational design tokens — colors, typography, shapes, and appearance — for the VISTA application used by Villon Farm Supply, an agricultural retail MSME in the Philippines.

---

## §2. System Objective

Establish a professional, functional, earth-tone design system that reflects the agricultural retail context of Villon Farm Supply while maintaining high readability and data-density appropriate for a WPF desktop application.

---

## §3. Brand Context

### Organization Identity
- **Application Name**: VISTA — Villon's Integrated Supply and Trade Application
- **Business**: Villon Farm Supply — local agricultural retail store
- **Sector**: Agriculture / Farm Supplies (seeds, fertilizers, tools, pesticides)
- **Location**: Philippines
- **User Profile**: Non-IT staff (store clerks, cashiers, manager) — requires simple, clear interfaces

### Design Philosophy
- **Simplicity over complexity** — explicit design principle
- Professional, functional appearance — NOT decorative or flashy
- Data-dense layouts optimized for desktop (1366×768 minimum)
- High contrast for readability in retail store lighting conditions

---

## §4. Color Palette — Agricultural Earth-Tone Identity

### Primary Colors

| Token | Hex | Usage |
|-------|-----|-------|
| **Primary** | `#4A6741` | Deep sage green — buttons, active nav, primary actions. Evokes agriculture/growth. |
| **Primary Light** | `#6B8F5E` | Lighter sage — hover states, secondary elements |
| **Primary Dark** | `#354B30` | Dark sage — pressed states, active sidebar items |

### Neutral Colors

| Token | Hex | Usage |
|-------|-----|-------|
| **Background** | `#FAFAF5` | Warm off-white — main content background |
| **Surface** | `#FFFFFF` | Cards, panels, modals |
| **Sidebar** | `#2C3E2C` | Dark forest green — sidebar background |
| **Sidebar Text** | `#E8EDE8` | Light text on sidebar |
| **Border** | `#D4D4C8` | Warm gray — borders, dividers |
| **Text Primary** | `#1A1A18` | Near-black — body text |
| **Text Secondary** | `#6B6B63` | Muted — labels, captions |

### Status Colors (Documented Standard)

| Status | Background | Text | Usage |
|--------|-----------|------|-------|
| Draft | `#E0E0E0` | `#616161` | Gray — unpublished records |
| Pending | `#FFF3E0` | `#E65100` | Amber — awaiting approval |
| Approved | `#E8F5E9` | `#2E7D32` | Green — confirmed/active |
| Rejected | `#FFEBEE` | `#C62828` | Red — denied |
| Void | `#F5F5F5` | `#212121` | Black — cancelled/voided |
| Partially Received | `#E3F2FD` | `#1565C0` | Blue — in progress |
| Fully Received | `#E0F2F1` | `#00695C` | Teal — complete |

### Alert Colors

| Alert | Background | Icon Color |
|-------|-----------|------------|
| Info | `#E3F2FD` | `#1565C0` |
| Success | `#E8F5E9` | `#2E7D32` |
| Warning | `#FFF3E0` | `#E65100` |
| Error | `#FFEBEE` | `#C62828` |

### Data Visualization Colors

| Usage | Color |
|-------|-------|
| Revenue / Positive | `#4A6741` (primary green) |
| Expense / Negative | `#C62828` (alert red) |
| Neutral / Baseline | `#78909C` (blue-gray) |
| Accent 1 | `#5D8AA8` (steel blue) |
| Accent 2 | `#D4A574` (warm tan) |
| Accent 3 | `#8B6F47` (earth brown) |

---

## §5. Typography

| Element | Font | Weight | Size |
|---------|------|--------|------|
| **Headings** | Inter (fallback: Segoe UI) | 600 (Semi-Bold) | 18–24px |
| **Subheadings** | Inter | 500 (Medium) | 14–16px |
| **Body** | Inter | 400 (Regular) | 13–14px |
| **Table Data** | Inter | 400 (Regular) | 13px |
| **Labels** | Inter | 500 (Medium) | 12px |
| **Captions** | Inter | 400 (Regular) | 11px |
| **Monospaced (amounts)** | JetBrains Mono (fallback: Consolas) | 400 | 13px |

---

## §6. Shape & Spacing

| Token | Value |
|-------|-------|
| **Corner Radius (Small)** | 4px — buttons, inputs, badges |
| **Corner Radius (Medium)** | 8px — cards, panels |
| **Corner Radius (Large)** | 12px — modals, drawers |
| **Base Spacing Unit** | 4px |
| **Table Row Height** | 36px (compact density) |
| **Form Field Height** | 36px |
| **Sidebar Width** | 200px |
| **Footer Height** | 32px |

---

## §10. Do Not Assume

- Do NOT use bright, saturated primary colors. The palette is intentionally muted/earthy.
- Do NOT use rounded/pill-shaped buttons. Corner radius is small (4px).
- Do NOT apply dark mode as default. Light mode with warm off-white background is the standard.
- Do NOT use decorative fonts. All fonts must be optimized for data readability.

---

## §11. Required Output Quality Standard

- The design system must produce screens that look like a professional desktop ERP/POS application.
- Colors must maintain WCAG AA contrast ratios.
- The palette must feel appropriate for an agricultural business — not tech startup, not medical, not gaming.
- Typography must support dense data tables with many columns.

---

## §12. UI Consistency Rules

- All status badges use the exact hex values defined in §4 Status Colors.
- All sidebar backgrounds use `#2C3E2C` (dark forest green).
- All buttons use `#4A6741` (primary sage green) with white text.
- All table headers use `#F5F5EE` background with `#1A1A18` text.
- All form field borders use `#D4D4C8`.

---

## §13. Fallback Behavior If Context Is Missing

- If the Stitch tool does not support a specific color token, use the closest available preset.
- If custom fonts are not available, fall back to the system default (Inter → Segoe UI).
- If corner radius options are limited, choose the smallest available option.

---

## §14. Restrictions / Non-Goals

- Do NOT create any screens in this prompt — design tokens only.
- Do NOT define component-level styles (those are in the individual prompts).
- Do NOT create mobile or tablet-specific tokens.
