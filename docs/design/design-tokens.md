# Design Tokens

Design tokens are the single source of truth for visual values — colors, spacing, radii, shadows, and motion. Every component reads from them; nothing hard-codes a hex or a duration.

Code examples on this page use `sn-` as the class prefix (from a worked example project). Substitute your own project's prefix throughout — see [Example Design System](../conventions/example-system.md) for guidance on picking one.

---

## The CSS file stack

Tokens drive a layered CSS build. Each file has one job and a strict import order. The architecture is described generally in [CSS Architecture](../conventions/css.md) — this page applies it as a practical recipe.

```text
tokens.css    →  base.css  →  layout.css  →  components.css  →  effects.css
```

| File | Charter | What goes here |
|---|---|---|
| `tokens.css` | Tokens | `:root { --color-*, --radius-*, --shadow-*, --motion-* }` |
| `base.css` | Base | `html`, `body`, `:focus-visible`, reduced-motion defaults |
| `layout.css` | Layout | Page-level structural primitives — grids, gutters, stacks |
| `components.css` | Components | `.[prefix]-<name>` component rules; `@apply` is legal here |
| `effects.css` | Effects | Opt-in `.[prefix]-fx-*` decorative classes — hover glows, transitions |

The order is fixed:

- `tokens` must be first so every downstream file can read `var(--color-*)`.
- `effects` must be last so a flourish can override a component without specificity tricks.

The compiled output (`app.css`) is generated — never hand-edit it.

---

## Token categories

```css
:root {
    /* Color */
    --color-bg:           #f8fafc;  /* app background */
    --color-surface:      #ffffff;  /* cards, panels */
    --color-text:         #0f172a;  /* primary text */
    --color-primary:      #0d9488;  /* teal-600 */
    --color-danger:       #e11d48;  /* rose-600 */

    /* Shape */
    --radius-sm:  0.375rem;
    --radius-md:  0.75rem;
    --radius-lg:  1rem;

    /* Shadow */
    --shadow-sm:  0 1px 2px 0 rgb(0 0 0 / 0.05);
    --shadow-md:  0 4px 6px -1px rgb(0 0 0 / 0.07);

    /* Motion */
    --motion-fast:    120ms;
    --motion-base:    200ms;
    --easing-standard: cubic-bezier(0.4, 0, 0.2, 1);
}
```

---

## Editing a token

### Change an existing color

1. Open `tokens.css`.
2. Find the `--color-*` token. Comments cite the Tailwind shade so you can pick a neighbour without guessing hex.
3. Update the value in the `:root` block (light) **and** the `:root[data-theme="dark"]` block — dark mode is an explicit override, not automatic.

```diff
 :root {
-    --color-primary: #0d9488; /* teal-600 */
+    --color-primary: #4f46e5; /* indigo-600 */
 }
 :root[data-theme="dark"] {
-    --color-primary: #2dd4bf; /* teal-400 */
+    --color-primary: #818cf8; /* indigo-400 */
 }
```

Every component that references `var(--color-primary)` updates immediately. No component files need to change.

### Add a brand-new color

1. Add the token to `tokens.css` (both light and dark themes).
2. If you need a Tailwind utility class (`bg-accent`, `text-accent`), add it to `tailwind.config.cjs` and wire it to the CSS variable so the token stays the source of truth:

```js
// tailwind.config.cjs
colors: {
  accent: 'rgb(var(--color-accent-rgb) / <alpha-value>)',
}
```

This indirection keeps the theme switcher working — flipping `data-theme` only flips CSS variables. Baking a hex into the Tailwind config breaks dark mode silently.

---

## Theme presets

A theme preset is one `:root[data-theme="<name>"]` block that overrides tokens without touching component files.

```css
:root[data-theme="dark"] {
    --color-bg:      #020617;  /* slate-950 */
    --color-surface: #0f172a;  /* slate-900 */
    --color-primary: #2dd4bf;  /* teal-400 */
}
```

Rules for presets:

- Override only the tokens whose defaults don't fit. Leave the rest inherited.
- A preset must not require a new selector or component override to look right. If it does, the component itself is wrong — fix it to consume tokens.
- Wire the switcher by writing the preset name to `document.documentElement.dataset.theme` and persisting to `localStorage`. Adding a preset is data-only — no JS change needed.

---

## Editing components

Every component lives once in `components.css` under a `.[prefix]-<name>` class.

!!! example

    ```diff
     .sn-card {
    -    @apply bg-surface border border-line rounded-2xl shadow-sm p-4;
    +    @apply bg-surface border border-line rounded-3xl shadow-md p-5;
     }
    ```

Rules:

- `@apply` is legal **only** in `components.css` and `layout.css`.
- Keep the selector flat. Specificity ceiling is **0,2,1** — one class plus one state pseudo-class (`:hover`, `:focus-visible`, `[aria-expanded="true"]`).
- State variants use modifier classes (`.sn-card--ghost`) or state classes (`.is-loading`). Never inline styles.
- Never use `!important` outside the `@media (prefers-reduced-motion)` block in `effects.css`.

---

## Component promotion rule

A pattern earns a `.sn-<name>` class once it appears in **three or more templates**. Until then, leave it as ad-hoc utilities on the markup. Premature components rot fast.

1. Confirm the third use site exists.
2. Add the class to `components.css`.
3. Replace the utility cluster in all three templates with the new class.
4. Add the component to the styleguide page so it has a canonical reference render.

---

## Decorative effects

Flourishes — background gradients, hover glows, entrance animations — go in `effects.css` as opt-in `.[prefix]-fx-*` classes.

!!! example

    ```css
    @media (prefers-reduced-motion: no-preference) {
        .sn-fx-hover-lift {
            transition: transform var(--motion-fast) var(--easing-standard);
        }
        .sn-fx-hover-lift:hover {
            transform: translateY(-2px);
        }
    }
    ```

Requirements:

- Safe to remove without breaking layout or readability.
- Any motion wrapped in `@media (prefers-reduced-motion: no-preference)`.
- Below the specificity ceiling (one class).

Add the class to the markup where you want the flourish. Never apply it via descendant selectors.

---

## Layout and spacing

Class names in the table below are from a worked example — substitute your own prefix.

| Need | Edit |
|---|---|
| Page gutter width | `layout.css` — `.[prefix]-content-gutter` `max-w-*` |
| Vertical rhythm between sections | `layout.css` — `.[prefix]-stack` `gap` |
| Sidebar width | `layout.css` — `.[prefix]-dashboard-grid` columns |
| Form field spacing | `components.css` — `.[prefix]-form-row` `gap` |
| Card inner padding | `components.css` — `.[prefix]-card` `p-*` |

Layout primitives are structural only — no decoration, no color. If you find yourself adding `bg-*` to `layout.css`, the rule belongs in `components.css`.

---

## Motion

All transitions reference `--motion-*` and `--easing-standard` from `tokens.css`. Tune motion globally by editing the tokens; tune one component by referencing a different token, never by hard-coding a duration.

!!! example

    ```css
    .sn-toast {
        transition: opacity var(--motion-fast) var(--easing-standard);
    }
    ```

Reduced-motion is enforced at the `effects.css` level. Do not reinvent the pattern inside individual components.

---

## Common mistakes

These apply to any token-driven CSS architecture — class names follow the `[prefix]-` convention from the worked example.

| Symptom | Likely cause |
|---|---|
| `!important` review comment | Decoration leaking into a component or layout file |
| Specificity above 0,2,1 | Compound selectors (`.[prefix]-card .[prefix]-button`) — restructure the class |
| Dark mode broken after adding a color | Forgot to override the token in `data-theme="dark"` |
| Theme switcher does nothing | Component hard-codes a hex instead of `var(--color-*)` |
| New component duplicates an existing one | Promotion rule not followed — use the existing `.[prefix]-<name>` |
| `@apply` in `tokens.css` or `base.css` | Those charters forbid `@apply` — move the rule to `components.css` |

---

## Where to edit what

Class names follow the `[prefix]-` convention — substitute your own prefix.

| I want to change… | Edit |
|---|---|
| Brand color, surface color, text color | `tokens.css` — a `--color-*` custom property |
| Corner radius, shadow strength | `tokens.css` — `--radius-*`, `--shadow-*` |
| Animation duration or easing | `tokens.css` — `--motion-*`, `--easing-*` |
| Look of an existing component | `components.css` — the `.[prefix]-<name>` rule |
| Add a new component | `components.css` — see promotion rule above |
| Page-level structure (grids, gutters) | `layout.css` — `.[prefix]-<layout-primitive>` |
| Decorative flourish (gradient, hover glow) | `effects.css` — opt-in `.[prefix]-fx-*` class |
| Base typography, focus ring defaults | `base.css` |
| Add a new theme preset | `tokens.css` — new `:root[data-theme="…"]` block |
