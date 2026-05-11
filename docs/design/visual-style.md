# Visual Style

A reference for visual design decisions: overall aesthetic, color tokens, typography scale, and layout patterns. Pair with [Design Tokens](design-tokens.md) for the implementation.

The color palettes, typography values, and layout examples on this page are drawn from a real dashboard product. Use them as a starting point — the structure matters more than the specific values.

---

## Aesthetic traits

Define these before touching CSS. They constrain every component decision that follows.

| Trait | Example direction |
|---|---|
| Overall look | Modern SaaS dashboard — clean, not minimal to the point of confusion |
| Density | Medium-dense but readable — more information than a marketing site, less than a spreadsheet |
| Corners | Rounded but not bubbly (`rounded-xl` to `rounded-2xl`) |
| Shadows | Soft, minimal (`shadow-sm`) — depth without drama |
| Borders | Subtle (`border border-slate-200`) — enough to separate surfaces |
| Background | Off-white in light mode, deep slate in dark mode |
| Accent | One signal color — used for primary actions and active states |
| Motion | Small, functional transitions only — nothing decorative at rest |

The mood goal: **calm, sharp, organized.** Not playful, not corporate-boring.

---

## Color tokens — light mode

CSS custom properties defined in `tokens.css`. Tailwind utility classes map to them via `tailwind.config.cjs`. The values below are an example palette for a calm dashboard product — adjust to suit your brand.

| Token | Value | Use |
|---|---|---|
| `--color-bg` | `slate-50` | App background |
| `--color-surface` | `white` | Cards, tables, panels |
| `--color-surface-alt` | `slate-100` | Secondary panels, hover rows |
| `--color-text` | `slate-900` | Primary text |
| `--color-text-muted` | `slate-500` | Metadata, timestamps |
| `--color-primary` | `teal-600` | Active states, primary buttons |
| `--color-primary-hover` | `teal-700` | Primary hover |
| `--color-warning` | `amber-500` | Needs review, warnings |
| `--color-danger` | `rose-600` | Delete, error, spam |
| `--color-border` | `slate-200` | Card and table dividers |
| `--color-focus` | `teal-500` | `:focus-visible` ring |

---

## Color tokens — dark mode

Dark mode is an explicit `:root[data-theme="dark"]` override in `tokens.css` — not automatic.

| Token | Dark value |
|---|---|
| `--color-bg` | `slate-950` |
| `--color-surface` | `slate-900` |
| `--color-surface-alt` | `slate-800` |
| `--color-text` | `slate-100` |
| `--color-text-muted` | `slate-400` |
| `--color-primary` | `teal-400` |
| `--color-primary-hover` | `teal-300` |
| `--color-warning` | `amber-400` |
| `--color-danger` | `rose-400` |
| `--color-border` | `slate-700` |
| `--color-focus` | `teal-400` |

---

## Typography

### System font stack

Using the system font stack avoids web font loading costs, FOIT, and licensing complexity — the design looks native on every platform.

```text
font-family:
  -apple-system, BlinkMacSystemFont,
  "Segoe UI", Roboto, "Helvetica Neue",
  Arial, sans-serif,
  "Apple Color Emoji", "Segoe UI Emoji";

font-family-mono:
  ui-monospace, SFMono-Regular, Menlo, Consolas,
  "Liberation Mono", monospace;
```

A bespoke web font is a polish pass for a later version — it does not block launch.

### Type scale

| Use | Tailwind classes |
|---|---|
| Page titles | `text-2xl font-semibold` |
| Section headers | `text-lg font-medium` |
| Body | `text-sm text-slate-700` |
| Metadata | `text-xs text-slate-500` |
| Status pills | `text-xs font-medium uppercase tracking-wide` |

---

## Visual non-negotiables

Define these before building. They are the constraints that must not be broken silently — revisiting any of them requires a documented decision. The example below comes from a dashboard product; adapt the specifics to your project.

!!! example "Example: visual non-negotiables for a dashboard product"

    1. **Status indicators carry icon + text + color** — never color alone. The accessible and print paths must remain readable without color.
    2. **One `<h1>` per page**, sequential heading levels, skip-link to `#main`.
    3. **Inline SVG for charts** — no charting library runtime in a lean v1.
    4. **Icons as static SVGs** — no JS icon library at runtime.
    5. **Reduced-motion respected** via `@media (prefers-reduced-motion: reduce)`.
    6. **No `!important`** outside the reduced-motion block in the effects layer.

---

## SaaS dashboard layout

A standard layout for internal product tools and SaaS dashboards.

```text
┌────────────────────────────────────────────────┐
│  Header (workspace switcher + user menu)       │
├────────────┬───────────────────────────────────┤
│            │                                   │
│  Sidebar   │  Main content area                │
│            │                                   │
└────────────┴───────────────────────────────────┘
```

### Sidebar

Collapsible left sidebar. The items depend entirely on your product — the example below is from a triage and workflow tool.

!!! example "Example: sidebar items for a feedback triage product"

    | Order | Item | Purpose |
    |---|---|---|
    | 1 | Dashboard | Overview cards and summary metrics |
    | 2 | Inbox | New and unresolved items requiring action |
    | 3 | All items | Full filtered and searchable list |
    | 4 | People | Submitters, customers, or contacts |
    | 5 | Roadmap | Items marked as planned or in-progress |
    | 6 | Changelog | Items marked as shipped |
    | 7 | Insights | Aggregations — top tags, trends |
    | 8 | Settings | Workspace, members, configuration |

### Header

Common header contents for a multi-tenant SaaS:

- Workspace or account switcher — only visible when the user belongs to more than one workspace.
- User menu — profile, sign out.
- Theme switcher — light / dark, once dark mode ships.

---

## Public routes (unauthenticated)

Standard set for a SaaS with sign-up, email verification, and a public-facing surface. Authenticated users hitting `/` redirect to their workspace or dashboard.

!!! example "Example: public routes for a multi-tenant SaaS"

    | Route | Purpose |
    |---|---|
    | `/` | Marketing landing page |
    | `/login` | Sign-in form |
    | `/signup` | Account + workspace creation |
    | `/forgot-password` | Password reset request |
    | `/reset-password?token=…` | Password reset confirmation |
    | `/verify-email?token=…` | Email verification confirmation |
    | `/invitations/<token>` | Workspace invitation acceptance |
    | `/<slug>/submit` | Public submission form for a workspace |
    | `/<slug>/roadmap/public` | Read-only published roadmap |
    | `/<slug>/changelog/public` | Read-only published changelog |

---

## Logo and favicon

For a v1 launch, a wordmark (the app name in the system font, semibold) and a simple favicon are sufficient. A designed mark is a later polish pass — it does not block alpha or beta.
