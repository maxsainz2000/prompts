## §1. Role & Instruction

You are a UI screen designer for a Windows desktop merchandising application.
Your task is to generate the **login/authentication screen** for the VISTA application. This is the first screen users see when launching the application.

---

## §2. System Objective

Provide a clean, professional authentication interface that clearly identifies the application, collects credentials, and communicates the system's purpose — suitable for non-IT staff in a retail store environment.

---

## §3. Application Context (Embedded)

### System Identity
- **Application**: VISTA — Villon's Integrated Supply and Trade Application
- **Entity**: Villon Farm Supply (agricultural retail, MSME)
- **Platform**: Windows desktop (WPF) — design for 1366×768 minimum
- **Design Language**: Professional, functional, not decorative.

### Color Palette
- **Primary**: `#4A6741` (sage green)
- **Background**: `#FAFAF5` (warm off-white)
- **Accent**: `#2C3E2C` (dark forest green)
- **Text**: `#1A1A18` (near-black)

---

## §4. Referenced Documentation (Embedded Extracts)

### Security Requirements (from `modules/spec.md` §8)

- §8.1: Current user's name and role displayed after login.
- §8.3: Login screen must clearly communicate the system name, enforce strong authentication, and clear sensitive data from memory on logout (OWASP DA3).

### OWASP Constraints (from `context-villon-vista-2026-03-28.md`)

| ID | Threat | Mitigation |
|----|--------|-----------|
| DA2 | Broken Authentication | Enforce secure login |
| DA3 | Sensitive Data Exposure | Clear memory post-logout |
| DA4 | Improper Cryptography | No MD5/SHA1 for passwords |
| DA5 | Improper Authorization | Least privilege per role — show role after login |

---

## §5. Business Rules (Extracted)

- Users must authenticate before accessing any module.
- The login screen must display the application name clearly.
- Password fields must use masked input (●●●●●●).
- No "Remember Password" option in v1 (security policy).

---

## §6. UI Generation Scope

### Page Layout

```
FULL SCREEN (no sidebar, no top bar, no footer):

LEFT HALF (~50%):
├── Application logo / branding area
├── "VISTA" application name (large)
├── "Villon's Integrated Supply and Trade Application" (subtitle)
├── "Villon Farm Supply" (entity name)
└── Agricultural illustration or pattern (decorative)

RIGHT HALF (~50%):
├── "Sign In" heading
├── Username field
├── Password field (masked)
├── "Sign In" button (full width, primary color)
├── Version info: "v1.0.0"
└── "Offline Mode Available" indicator
```

### Component Composition

1. **Branding Panel** (left) — logo, app name, entity name
2. **Login Form** (right) — username, password, submit button
3. **Version Footer** — app version, offline notice

---

## §7. Layout Expectations

- **Split layout**: 50/50 horizontal split. Left = branding. Right = form.
- **Left panel**: Dark forest green (`#2C3E2C`) background with light text. Can include a subtle leaf/agriculture pattern or gradient.
- **Right panel**: White (`#FFFFFF`) background with the login form centered.
- **Form width**: ~360px, centered within the right panel.
- **Total viewport**: Full 1366×768, no window chrome visible.

---

## §8. Component Expectations

### Left Branding Panel
- Large "VISTA" text (28–32px, bold, white)
- Subtitle: "Villon's Integrated Supply and Trade Application" (14px, light green)
- Entity: "Villon Farm Supply" (16px, white, with a small leaf or wheat icon)
- Optional: Subtle agricultural pattern background (wheat, leaves, farm silhouette)

### Right Login Form
- Heading: "Sign In" (24px, dark text)
- Subheading: "Enter your credentials to continue" (14px, muted text)
- **Username field**: Label "Username", placeholder "Enter your username", icon 👤
- **Password field**: Label "Password", placeholder "Enter your password", icon 🔒, eye toggle for show/hide
- **Sign In button**: Full width, `#4A6741` background, white text, "Sign In"
- **Below button**: "v1.0.0" in small muted text
- **Offline notice**: Small gray text "🟢 System ready — offline mode available"

---

## §9. Interaction Expectations

- `Enter` key submits the login form.
- `Tab` moves focus from username → password → sign in button.
- Password field has show/hide toggle (eye icon).
- Invalid credentials show inline error: "Invalid username or password. Please try again."

---

## §10. Do Not Assume

- Do NOT add "Forgot Password" functionality — not in scope for v1.
- Do NOT add "Remember Me" checkbox — security policy prohibits this.
- Do NOT add social login or SSO buttons.
- Do NOT add user registration link — users are created by the Admin.
- Do NOT add any navigation elements (sidebar, top bar, footer).

---

## §11. Required Output Quality Standard

- The login screen must feel professional and trustworthy.
- "VISTA" and "Villon Farm Supply" must be prominently visible.
- Sample state: both fields empty, ready for input.
- The agricultural/earth-tone branding must be immediately apparent.

---

## §12. UI Consistency Rules

- Typography: Inter (fallback: Segoe UI).
- Primary button: `#4A6741` background, white text, 4px border radius.
- Input fields: `#FFFFFF` background, `#D4D4C8` border, 4px border radius, 36px height.
- Left panel: `#2C3E2C` background.

---

## §13. Fallback Behavior If Context Is Missing

- If an agricultural illustration is not available, use a solid gradient from `#2C3E2C` to `#4A6741`.
- If a logo icon is not available, use text-only "VISTA" as the logo.

---

## §14. Restrictions / Non-Goals

- Do NOT generate any post-login screens.
- Do NOT include role selection at login — roles are assigned server-side.
- Do NOT generate mobile login layouts.
