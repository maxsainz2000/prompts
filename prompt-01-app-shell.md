## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **application shell** — the persistent navigation structure that surrounds the content area on every page of the VISTA application. This shell includes the top bar, left sidebar, content area placeholder, and bottom status bar.

This is a foundational screen. Every subsequent page screen will render its content within this shell's content area.

---

## §2. System Objective

Create the global navigation structure that provides module switching, page navigation, user identity display, and system status visibility — enabling users to orient themselves within the application at all times.

---

## §3. Application Context (Embedded)

### System Identity
- **Application**: VISTA — Villon's Integrated Supply and Trade Application
- **Entity**: Villon Farm Supply (agricultural retail, MSME)
- **Platform**: Windows desktop (WPF) — design for 1366×768 minimum
- **Design Language**: Professional, functional, data-dense. Not decorative.

### Color Palette (Earth-Tone Agricultural)
- **Primary**: `#4A6741` (sage green)
- **Sidebar Background**: `#2C3E2C` (dark forest green)
- **Sidebar Text**: `#E8EDE8` (light)
- **Content Background**: `#FAFAF5` (warm off-white)
- **Footer Background**: `#2C3E2C` (same as sidebar)
- **Footer Text**: `#E8EDE8`
- **Active Page Highlight**: `#4A6741` with white text

---

## §4. Referenced Documentation (Embedded Extracts)

### Navigation Architecture (from `modules/spec.md` §7)

#### §7.1 Application Wireframe

```
┌──────────────────────────────────────────────────────────────────┐
│  🏪 VISTA    [Purchasing] [Inventory] [POS] [Accounting]    👤 User (Role)  │
├──────────┬───────────────────────────────────────────────────────┤
│ Sidebar  │                                                      │
│          │                                                      │
│ • Page 1 │              Content Area                            │
│ • Page 2 │                                                      │
│ • Page 3 │              (Page content renders here)             │
│ • Page 4 │                                                      │
│ • Page 5 │                                                      │
│ • Page 6 │                                                      │
│ • Page 7 │                                                      │
│          │                                                      │
├──────────┴───────────────────────────────────────────────────────┤
│  🟢 Online (synced) │ Last sync: 2 min ago      │ v1.0.0       │
└──────────────────────────────────────────────────────────────────┘
```

#### §7.2 Sidebar Pages Per Module

| Purchasing | Inventory | POS / Sales | Accounting |
|-----------|-----------|-------------|------------|
| Dashboard | Dashboard | Dashboard | Dashboard |
| Suppliers | Item Master | Transaction | Chart of Accounts |
| Purchase Requests | Categories | Transaction History | Journal Entries |
| Purchase Orders | Stock on Hand | Returns | General Ledger |
| Receiving | Stock Adjustments | Customers | AP Ledger |
| Payables | Stock Movements | Pricing | AR Ledger |
| Reports | Physical Count | Cashier Mgmt | Financial Statements |
| | Reports | Reports | Financial Reports |
| | | | Period Close |
| | | | Reports |
| | | | Audit Trail |

### Sync Status Visibility (from `modules/spec.md` §6.2)

| Indicator | Meaning |
|-----------|---------|
| 🟢 **Online** | Connected and synced to MariaDB |
| 🟡 **Syncing** | Sync in progress |
| 🔴 **Offline** | Operating on local SQLite only |

### Security — Role Display (from `modules/spec.md` §8.1)

The current user's name and role are displayed in the top-right corner of every page.

---

## §5. Business Rules (Extracted)

- Navigation sidebar changes its page list based on the active module.
- Only one module can be active at a time.
- The current user's name and role must always be visible (OWASP DA5 compliance).
- Sync status must always be visible in the footer bar.

---

## §6. UI Generation Scope

### Page Layout

```
TOP BAR (full width, ~48px height):
├── Left: App Logo + "VISTA" text
├── Center: Module tabs [Purchasing] [Inventory] [POS/Sales] [Accounting]
└── Right: User avatar + "Maria Santos" + "Manager" role badge

LEFT SIDEBAR (~200px width, full height minus top/bottom bars):
├── Module name header (e.g., "PURCHASING")
├── Active page highlighted (sage green background, white text)
└── Inactive pages (light text on dark background)

CONTENT AREA (remaining width and height):
└── Placeholder text: "Select a page from the sidebar"

BOTTOM STATUS BAR (full width, ~32px height):
├── Left: 🟢 "Online (synced)"
├── Center: "Last sync: 2 minutes ago"
└── Right: "VISTA v1.0.0"
```

### Component Composition

1. **Top Bar** — module switcher + user identity
2. **Left Sidebar** — page navigation for active module
3. **Content Area** — empty placeholder
4. **Bottom Status Bar** — sync indicator + version

---

## §7. Layout Expectations

- **Top Bar**: Fixed height 48px. Dark forest green (`#2C3E2C`) background. White/light text.
- **Sidebar**: Fixed width 200px. Same dark forest green background. Page items are 36px tall with 12px left padding.
- **Content Area**: `#FAFAF5` background. Centered placeholder text.
- **Status Bar**: Fixed height 32px. Same dark forest green background. 12px font size.
- **Module Tabs**: Pill-shaped or underline-indicated. Active module uses `#4A6741` background or underline.
- **Total viewport**: Assume 1366×768 desktop resolution.

---

## §8. Component Expectations

### Top Bar
- VISTA logo (leaf/plant icon or simple text logo) left-aligned
- 4 module tabs center-aligned with labels: "Purchasing", "Inventory", "POS/Sales", "Accounting"
- Show "Purchasing" as the active module (highlighted)
- User: "Maria Santos" with role badge "Manager" right-aligned

### Left Sidebar
- Module header: "PURCHASING" in uppercase, smaller font
- 7 page links listed vertically: Dashboard, Suppliers, Purchase Requests, Purchase Orders, Receiving, Payables, Reports
- "Dashboard" shown as active (highlighted with sage green background)
- Each page item has a subtle icon to the left

### Content Area
- Large centered text: "Welcome to VISTA"
- Subtitle: "Select a page from the sidebar to begin"

### Status Bar
- Left: Green dot 🟢 + "Online (synced)"
- Center: "Last sync: 2 minutes ago"
- Right: "VISTA v1.0.0"

---

## §9. Interaction Expectations

- Module tabs switch the sidebar page list when clicked.
- Sidebar page links navigate to the selected page.
- Active page has visual highlight (background color change).
- `Ctrl+1/2/3/4` keyboard shortcuts for module switching.

---

## §10. Do Not Assume

- Do NOT invent additional navigation elements not described above.
- Do NOT add a search bar to the top bar (that is page-level, not shell-level).
- Do NOT add notification bells, settings gear, or other icons not specified.
- Do NOT create a hamburger menu — the sidebar is always visible on desktop.
- Do NOT assume the content area should display any page content — it is a placeholder.

---

## §11. Required Output Quality Standard

- The shell must look like a production-ready desktop application frame.
- The Purchasing module should appear active with its 7 sidebar pages.
- User name "Maria Santos" and role "Manager" must be visible.
- Sync status "Online" with green indicator must be visible.
- All text must be legible at 13–14px body size.

---

## §12. UI Consistency Rules

- Typography: Inter (fallback: Segoe UI).
- Sidebar background: `#2C3E2C` (dark forest green).
- Active sidebar item: `#4A6741` background with white text.
- Content background: `#FAFAF5` (warm off-white).
- Status bar: `#2C3E2C` background, `#E8EDE8` text.
- All borders: `#D4D4C8`.

---

## §13. Fallback Behavior If Context Is Missing

- If module icons are not available, use text-only module tabs.
- If sidebar page icons are not available, use text-only page links.
- If a specific color cannot be rendered, use the closest available shade.

---

## §14. Restrictions / Non-Goals

- Do NOT generate any page content inside the content area.
- Do NOT generate mobile or tablet layouts.
- Do NOT add any module-specific business logic.
- Do NOT create interactive forms or data tables within this shell.
