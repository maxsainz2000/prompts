## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **Categories** page — a split-layout page with a category tree on the left and category form on the right.

---

## §2. System Objective

Enable the Manager to organize the product catalog into hierarchical categories (e.g., Fertilizers > Organic, Seeds > Vegetables > Tomato) for filtering, reporting, and product organization.

---

## §3. Application Context (Embedded)

### Navigation Context
- **Active Module**: Inventory | **Active Page**: Categories
- **Sidebar**: Dashboard, Item Master, **Categories**, Stock on Hand, Stock Adjustments, Stock Movements, Physical Count, Reports
- **User**: Maria Santos / Manager | **Sync**: 🟢 Online
- Primary: `#4A6741` | Sidebar: `#2C3E2C` | Background: `#FAFAF5`

---

## §4. Referenced Documentation (Embedded Extracts)

### Component: Category Tree
- Hierarchical tree view (expandable/collapsible nodes).
- Each node shows: Category name, item count, expand/collapse arrow.
- Root-level categories: Fertilizers, Seeds, Pesticides, Farm Tools, Equipment, Safety, Feeds.
- Sub-categories: e.g. Seeds > Vegetables, Seeds > Fruits, Seeds > Rice.
- Click a node to select it (edit form populates).
- Right-click context menu: Add Sub-category, Rename, Deactivate.

### Component: Category Form
**Fields:**

| Field | Required |
|-------|----------|
| Category Name | Yes |
| Parent Category | No (dropdown — null = root category) |
| Description | No |
| Status | Active/Inactive |

- Position: Right panel (~50%).
- "Save" and "Cancel" buttons at bottom.

### Component: Category Search
- Search box above the tree. Filters tree to matching nodes.

---

## §5. Business Rules (Extracted)

- Categories are hierarchical (unlimited depth, but recommended max 3 levels).
- A category cannot be deleted if it has assigned items (show count).
- Categories are soft-deleted (deactivated).
- Every item must have at least one category.

---

## §6. UI Generation Scope

### Page Layout (Primary State: Split View)

```
CONTENT AREA:
┌──────────────────────────────┬──────────────────────────────────┐
│ Categories              [+]  │  Edit Category                   │
│ [🔍 Search categories...]   │                                   │
├──────────────────────────────┤  Name: [Fertilizers           ]  │
│ ▼ 📁 Fertilizers (45)       │  Parent: [— Root —            ]  │
│   ├── Organic (12)           │  Description: [Soil nutrition   │
│   ├── Chemical (28)          │    products for crops]           │
│   └── Specialty (5)          │  Status: ● Active               │
│ ▶ 📁 Seeds (78)             │                                   │
│ ▶ 📁 Pesticides (34)        │  Items in this category: 45     │
│ ▼ 📁 Farm Tools (25)        │                                   │
│   ├── Cutting Tools (8)      │                                   │
│   ├── Digging Tools (10)     │  [Cancel]              [Save]   │
│   └── Hand Tools (7)         │                                   │
│ ▶ 📁 Equipment (15)         │                                   │
│ ▶ 📁 Safety (20)            │                                   │
│ ▶ 📁 Feeds (18)             │                                   │
└──────────────────────────────┴──────────────────────────────────┘
```

---

## §7. Layout Expectations

- **Split**: 50/50 horizontal. Tree left, form right.
- **Tree**: Indented nodes, toggle arrows, item counts in muted text.
- **Form**: 2-column fields where applicable, centered in right panel.

---

## §8. Component Expectations

### Category Tree (sample)
- Fertilizers (45): Organic (12), Chemical (28), Specialty (5)
- Seeds (78): Vegetables (35), Fruits (18), Rice (15), Flowers (10)
- Pesticides (34): Insecticide (18), Herbicide (10), Fungicide (6)
- Farm Tools (25): Cutting Tools (8), Digging Tools (10), Hand Tools (7)
- Equipment (15)
- Safety (20)
- Feeds (18)

### Category Form (sample — "Fertilizers" selected)
- Name: Fertilizers
- Parent: — Root —
- Description: Soil nutrition products for crops and plants
- Status: Active
- Items in category: 45

---

## §9. Interaction Expectations

- Tree node click: selects and populates the form.
- Tree expand/collapse: arrow click toggles children visibility.
- "+ " button (top-right of tree): creates new root category.
- Right-click menu on node: Add Sub-category, Rename, Deactivate.

---

## §10. Do Not Assume

- Do NOT add drag-and-drop reordering of categories.
- Do NOT add category images or icons beyond folder emoji.
- Do NOT add category-level pricing rules.

---

## §11. Required Output Quality Standard

- Production-ready. Agricultural categories. Item counts realistic.
- "Categories" active in sidebar.

---

## §12. UI Consistency Rules

- Typography: Inter. Tree indentation: 20px per level. Active node: `#4A6741` background.

---

## §13. Fallback Behavior If Context Is Missing

- If tree cannot render hierarchically, use an indented list.

---

## §14. Restrictions / Non-Goals

- Do NOT generate backend code. Do NOT generate mobile layouts.
