# CSS Architecture

How to organise CSS so that it scales without becoming a maintenance burden.

## Why split CSS into files

A single CSS file is fine for small sites (three to five pages). As the surface grows — more pages, a real design identity, reusable components — a single file becomes a problem:

- Every change touches the same file, causing frequent merge conflicts.
- It is impossible to tell at a glance whether a diff is a token change, a layout change, or a component change.
- Decoration (`hover` lifts, animations) lives next to resets, which makes "what is load-order sensitive?" invisible.

The solution is a small, deliberate file split with one file per concern.

## File structure

```text
static/css/
├── input.css        # entry point — only @import statements and @tailwind directives
├── tokens.css       # design tokens: colours, spacing, radius, shadow, motion
├── base.css         # element resets, root styles, focus ring, reduced-motion
├── layout.css       # page shells, grids, stacks, gutters
├── components.css   # the component class vocabulary
├── effects.css      # transitions, animations, gradients, decorative polish
└── app.css          # generated output — DO NOT EDIT
```

`input.css` is a thin orchestrator:

```css
@tailwind base;
@import "./tokens.css";
@import "./base.css";

@tailwind components;
@import "./layout.css";
@import "./components.css";

@tailwind utilities;
@import "./effects.css";
```

**Load order is significant.** Tokens must be defined before base styles reference them. Components must be defined before effects polish them. Do not reorder without thinking through the cascade implications.

### Why each file exists

| File | Charter | What belongs here |
|---|---|---|
| `tokens.css` | Design contract | Only `:root { --… }` and `[data-theme="…"]` blocks. No selectors, no `@apply`, no `@media`. |
| `base.css` | Element floor | Element-level rules (`html`, `body`, `*`, `:focus-visible`). No class selectors. |
| `layout.css` | Page structure | Page shells, grids, stacks, gutters. Structural primitives, not visual polish. |
| `components.css` | Component vocabulary | Only named component classes (`.[prefix]-card`, `.[prefix]-button`, etc.). |
| `effects.css` | Decoration | Transitions, animations, hover/focus polish, gradients. Everything here can be deleted in a print stylesheet. |

Each file has a charter. A PR that adds a `:root { --… }` block to `components.css` is rejected — the charter is the file's contract.

## Design tokens

Design tokens are named values that make every visual decision in the product consistent and changeable from one place.

Define them as CSS custom properties on `:root`:

```css
:root {
  /* Typography */
  --font-sans: Inter, system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
  --text-sm:   0.875rem;
  --text-base: 1rem;
  --text-lg:   1.125rem;
  --text-xl:   1.25rem;
  --text-2xl:  1.5rem;
  --text-3xl:  1.875rem;
  --leading-tight:  1.2;
  --leading-normal: 1.6;

  /* Colour */
  --color-accent:       #2563eb;
  --color-accent-hover: #1d4ed8;
  --color-success:      #16a34a;
  --color-warning:      #d97706;
  --color-error:        #dc2626;
  --color-bg:           #ffffff;
  --color-surface:      #f8fafc;
  --color-border:       #e2e8f0;
  --color-text:         #0f172a;
  --color-text-muted:   #64748b;
  --color-focus:        #2563eb;

  /* Spacing (4px base) */
  --space-1:  0.25rem;
  --space-2:  0.5rem;
  --space-4:  1rem;
  --space-6:  1.5rem;
  --space-8:  2rem;
  --space-12: 3rem;
  --space-16: 4rem;

  /* Shape */
  --radius-sm:   4px;
  --radius-md:   8px;
  --radius-lg:   12px;
  --radius-full: 9999px;

  /* Shadow */
  --shadow-sm: 0 1px 2px rgb(0 0 0 / 0.05);
  --shadow-md: 0 4px 6px rgb(0 0 0 / 0.07), 0 2px 4px rgb(0 0 0 / 0.05);
  --shadow-lg: 0 10px 15px rgb(0 0 0 / 0.1), 0 4px 6px rgb(0 0 0 / 0.05);

  /* Motion */
  --duration-fast:   100ms;
  --duration-normal: 200ms;
  --ease-out: cubic-bezier(0.16, 1, 0.3, 1);
}
```

Dark mode overrides use `[data-theme="dark"]` on `<html>` — same token names, different values. A theme switch requires no class swap and no CSS rebuild, just one attribute change.

A new design token must update every file that references it — the token definition, the Tailwind config (if using Tailwind), and any documentation. If any of those lag, the design system has drifted.

## Naming conventions

### The two-layer model

| Layer | Where | When to use |
|---|---|---|
| Design tokens | CSS custom properties in `tokens.css` | One source of truth for colour, radius, shadow |
| Utility classes | Directly in HTML (`class="bg-white border …"`) | First reach for every visual decision |
| Component classes | `@layer components` in CSS, via `@apply` | Only after the same utility string appears in three or more templates |

### Component class naming

Choose a short project prefix (e.g. `ui-`, `c-`, or your product initials). Then use block-element shape with single dashes:

```text
[prefix]-card
[prefix]-card-header
[prefix]-card-footer
[prefix]-button
[prefix]-button-primary
[prefix]-button-ghost
[prefix]-input
[prefix]-form-field
[prefix]-modal
[prefix]-toast
[prefix]-empty-state
```

### State class naming

State classes use a verb-prefix so they read naturally:

```text
is-open
is-loading
is-active
is-disabled
has-error
has-warning
```

State classes are promoted immediately — `is-loading` must mean the same thing on a button, a card, and a form row. Unlike component classes (rule of three), there is no threshold for state classes.

### Forbidden naming patterns

| Pattern | Problem |
|---|---|
| Tag-shaped names — `header`, `nav`, `button` | Use the actual HTML element instead |
| Colour-baked names — `red-button`, `blue-card` | Use semantic names (`button-danger`) so reskinning does not lie |
| Layout-baked names on components — `card-left`, `card-grid` | Layout is composed at the call site, not baked into the component |

## The rule of three

Do not create a component class prematurely. The rule:

> First implementation: inline utility classes. When the same utility string appears verbatim in **three or more** templates, promote it to a named component class.

Why three, not two:

- Two repeats might be coincidence; three is a pattern.
- Pre-promoted classes make the component vocabulary lie — they suggest a component that does not exist yet.
- Late promotion is cheap (one `@apply` line, search-and-replace). Early promotion is expensive (every change touches a class file and every consumer).

When promoting:

1. Pick a name following the conventions above.
2. Add the `@apply` rule under `@layer components`.
3. Replace the utility string in every consumer.
4. Build and visually diff.
5. Add a row to the component inventory documentation.

## Layout primitives

Layout primitives are composed at the call site with utilities, not baked into component classes. This keeps layout visible to anyone reading a template.

| Pattern | Example composition |
|---|---|
| Page shell | `min-h-screen bg-[--color-bg] text-[--color-text]` |
| Two-pane (sidebar + main) | `grid grid-cols-[16rem_1fr] min-h-screen` |
| Content gutter | `mx-auto max-w-6xl px-4 md:px-6 lg:px-8 py-8` |
| Card grid | `grid gap-4 md:grid-cols-2 lg:grid-cols-3` |
| Stack | `flex flex-col gap-4` |
| Inline cluster | `inline-flex items-center gap-2` |
| Table wrapper | `overflow-x-auto rounded-lg border border-[--color-border]` |
| Form row | `flex flex-col gap-1` |

## Component states

Every interactive component must handle all five states, even if some are visually identical to the default:

| State | CSS selector | What it signals |
|---|---|---|
| Default | Base class | Resting appearance |
| Hover | `:hover` | Pointer is over and the action is available |
| Focus | `:focus-visible` | Keyboard focus — tied to `var(--color-focus)` |
| Disabled | `:disabled`, `[aria-disabled="true"]`, `.is-disabled` | Action is unavailable |
| Error / loading | `.has-error`, `.is-loading` | Validation failure or async work in flight |

Example for a button component:

```css
.[prefix]-button { /* default */ }
.[prefix]-button:hover { /* hover */ }
.[prefix]-button:focus-visible { outline: 2px solid var(--color-focus); outline-offset: 2px; }
.[prefix]-button:disabled,
.[prefix]-button.is-disabled { opacity: 0.5; cursor: not-allowed; }
.[prefix]-button.has-error { border-color: var(--color-error); }
.[prefix]-button.is-loading { /* spinner via ::after */ }
```

Key distinctions:

- **Disabled and loading are not the same.** Loading signals "I clicked, it's working" (`aria-busy="true"`). Disabled signals "you cannot click this" (`disabled` or `aria-disabled`).
- **Empty states get the same treatment as components.** A list with zero items renders a message that tells the user what to do next, not just "nothing here."
- **Loading states appear immediately**, not after a delay. A delay hides the state from users on slow connections — the people who need it most.
- **Error messages echo what the server said**, not a generic "something went wrong."

## Specificity budget

Keep CSS specificity low and predictable:

| Specificity | Example | Allowed |
|---|---|---|
| `0,1,0` | Single class | Yes — default |
| `0,2,0` | Class + state class (`.button.is-loading`) | Yes |
| `0,2,1` | Class + pseudo (`:hover`, `:focus-visible`) | Yes |
| Anything higher | `.card .button a:hover` | No — use a modifier class instead |

Rules:

- **No `#id` selectors.** IDs are for anchors, skip-links, and `<label for>` — never for styling.
- **No tag-only overrides** below the base/reset layer.
- **No `!important`** in production CSS, with one exception: the `prefers-reduced-motion` block, which must override utility-class transitions.
- **No inline `style="…"`** — use a class. The only legitimate inline styles are JS-set dynamic values (a progress bar width, a chart value).

## Sizing units

| What | Unit | Reason |
|---|---|---|
| Font sizes and vertical rhythm | `rem` | Scales with the user's browser default font size |
| Maximum prose line width | `ch` | `65ch` is roughly 65 characters — the readable sweet spot |
| Hairlines and shadow offsets | `px` | Fine-grained values that do not need to scale |
| Fluid widths inside grids and flex containers | `%`, `fr` | Respond to their container |
| Arbitrary pixel values like `13px` or `22px` | — | Avoid — they break visual rhythm |

## Responsive strategy

- **Mobile-first.** Default styles target the smallest viewport. Add breakpoints with `min-width` as the viewport grows.
- **Three breakpoints.** `sm` (640px), `md` (768px), `lg` (1024px). Avoid bespoke values.
- Layout primitives own their responsive behaviour — a page shell component collapses the sidebar correctly; pages do not re-implement it.
- Tables stay as tables; on narrow viewports, secondary columns hide (`hidden md:table-cell`) rather than narrowing into cards.

Define breakpoints as named values in `tokens.css` so they are used consistently:

```css
/* tokens.css */
@custom-media --sm  (min-width: 640px);
@custom-media --md  (min-width: 768px);
@custom-media --lg  (min-width: 1024px);
@custom-media --xl  (min-width: 1280px);
```

Then reference them in component and layout files:

```css
.sidebar {
  display: none;
}

@media (--md) {
  .sidebar {
    display: block;
  }
}
```

## Motion

- Small, functional transitions only. No decorative animation.
- Wrap all transitions in `prefers-reduced-motion: reduce`:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    transition-duration: 0.01ms !important;
    animation-duration:  0.01ms !important;
  }
}
```

- Default transition durations: `100ms` for hover micro-interactions, `200ms` for panel opens and larger reveals.

## Focus and keyboard

- Every focusable element shows a `:focus-visible` ring tied to `var(--color-focus)`. Never `outline: none` without a visible replacement.
- Include a skip-link to `#main` as the first focusable element on every page.
- Tab order must match visual order. Never use a positive `tabindex`.
- Modal dialogs use `<dialog>.showModal()` so focus trapping is handled by the browser.

## Z-index discipline

Define a small named set and stick to it:

| Layer | Value | Use case |
|---|---|---|
| Base | (none) | Normal document flow |
| Sticky | `z-10` | Sticky table headers, top navigation bar |
| Overlay | `z-50` | Dialogs, toasts, popovers |

Anything requiring a fourth layer needs explicit review.

## Working alongside a utility framework

A custom component layer and a utility framework (like Tailwind) can coexist. There are two patterns — pick one and commit:

**Pattern A — utilities for layout, custom classes for components.**
Pages compose structure with utility strings at the call site. Individual UI elements use component classes.

```html
<!-- layout at the call site with utilities -->
<div class="grid grid-cols-[16rem_1fr] min-h-screen">

  <!-- components use named classes -->
  <aside class="sidebar">
    <nav class="nav-primary">…</nav>
  </aside>

  <main id="main" class="content-area">
    <button class="ui-button ui-button-primary">Save</button>
  </main>

</div>
```

**Pattern B — custom CSS owns everything.**
Component classes handle both structure and layout. No utility strings appear in templates. Higher upfront cost, lower per-page cost long term.

Mixing both patterns inconsistently is worse than either alone.

## Avoiding style duplication

Before adding a new component class, search the existing vocabulary:

- If the same visual outcome already exists → use that class.
- If it is *almost* right → add a modifier (e.g. `ui-card-compact`) rather than a sibling class.
- If it is genuinely new → apply the rule of three before promoting.

A CI lint check can catch duplication automatically by flagging repeated `@apply` lines or identical declaration blocks across component files.

## Maintaining visual consistency

A living style guide page that renders every component, modifier, and state is the strongest consistency tool available.

- A new component is not complete until it appears in the style guide with all states shown.
- Visual regression screenshots against the style guide, run on any CSS PR, catch accidental regressions before they reach production.
- Without a style guide, inconsistencies accumulate silently and only become visible when a user notices them.

## Known risks of a custom component system

Record these honestly before committing to a bespoke vocabulary:

| Risk | Mitigation |
|---|---|
| **Larger maintenance surface** — every component is owned end-to-end, including all states | Style guide requirement: every state must be shown before a component ships |
| **Dead-class drift** — utility frameworks self-prune unused classes; custom classes do not | Regular audits or a PurgeCSS step in the build |
| **Onboarding cost** — contributors must learn the bespoke vocabulary before they can ship | Keep the vocabulary small and the style guide easy to browse |
| **Cross-file drift** — tokens, config, and documentation must stay in lockstep | Require all four to update in the same PR; CI fails if they diverge |
| **Specificity creep** — nested selectors appear under deadline pressure, then the budget breaks | Enforce the specificity budget in code review; once broken it requires a deliberate refactor |

The mitigation for every one of these is the combination of: a style guide page, file charters, and visual regression tests. Without those three, a custom system is harder to maintain than it is worth.

## What to avoid

| Idea | Why |
|---|---|
| BEM `__` / `--` double-separators | A prefix plus single dashes covers the same ground more legibly |
| CSS-in-JS | Runtime cost on every render; couples styling to a JS framework |
| `@apply` outside the component layer | Makes tracing where a class is defined unnecessarily hard |
| Icon fonts | Break for screen readers, miss in print — use inline SVG with `<title>` or `aria-label` |
| More than one CSS framework | Two frameworks' resets conflict; one is enough |
| `!important` in component rules | A cascade problem indicates a structural problem — fix the selector |
| Dead utility classes | Utility frameworks self-prune; custom classes do not — audit regularly |
