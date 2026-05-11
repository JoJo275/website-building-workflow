# Example Design System

The conventions in [Semantic HTML](html.md) and [CSS Architecture](css.md) describe the rules. This page shows what those rules look like when applied to a real project — with names, component lists, and decisions made.

Use it as a template. Swap the prefix, the palette, and the component list for your own. The patterns are the part worth copying. For a worked color palette and visual style decisions that go alongside this structure, see [Visual Style](../design/visual-style.md).

---

## Picking a prefix

Every component class in a custom design system needs a short, unique prefix to avoid colliding with third-party classes or utility frameworks.

Good prefixes are:

- 2–3 characters from the product name (`sn-` for SignalNest, `tf-` for TaskFlow, `ds-` for your design system)
- Lowercase, followed by a single dash
- Consistent — never mix `ui-` and `c-` in the same project

Once chosen, the prefix is applied to every component class:

```text
[prefix]-button
[prefix]-card
[prefix]-input
[prefix]-modal
[prefix]-toast
```

State classes do not get a prefix — they describe state, not components:

```text
is-open
is-loading
is-active
is-disabled
has-error
has-warning
```

---

## Example component vocabulary

This is a worked example for a project management app. Define yours before building anything — it becomes the build list.

| Class | What it is |
|---|---|
| `[prefix]-button` | Base button. Modifiers: `-primary`, `-secondary`, `-ghost`, `-danger` |
| `[prefix]-card` | Surface block. Modifiers for tone (muted, elevated) and interactivity |
| `[prefix]-page-shell` | Full-page chrome — `<header>`, `<main>`, `<footer>` composition |
| `[prefix]-dashboard-grid` | Two-pane layout: sidebar + main content area |
| `[prefix]-status-pill` | Rounded status indicator with icon, text, and colour |
| `[prefix]-modal` | `<dialog>`-based modal styling |
| `[prefix]-form-field` | Label + input + help text + error message composition |
| `[prefix]-empty-state` | "Nothing here yet" block — includes icon, heading, and call to action |
| `[prefix]-toast` | Transient status message, bottom-right of screen |
| `[prefix]-skip-link` | Visually hidden skip-to-main link, visible on focus |

Rules for this list:

- **Modifiers use single dashes.** `[prefix]-button-primary`, not `[prefix]-button--primary`. The prefix already namespaces the class.
- **Sub-parts follow the same pattern.** `[prefix]-card-header`, `[prefix]-card-body`, `[prefix]-card-footer`. They read like what they are.
- **No layout inside components.** `[prefix]-card` styles the element it's on. The grid that arranges cards is composed at the call site.
- **If a name needs four segments**, the component is too broad — split it.

---

## Example file structure for a project

Adapted from a Python/Tailwind project. The split principle applies regardless of framework.

```text
src/
└── static/
    └── css/
        ├── input.css        # entry: @import statements only
        ├── tokens.css       # :root { --color-*, --space-*, --radius-*, … }
        ├── base.css         # html, body, :focus-visible, reduced-motion
        ├── layout.css       # [prefix]-page-shell, [prefix]-dashboard-grid
        ├── components.css   # all [prefix]-* component rules
        ├── effects.css      # transitions, hover polish, animations
        └── app.css          # generated output — DO NOT EDIT, NOT COMMITTED
```

Each file has a charter comment at the top. A contribution that does not fit the charter goes in a different file.

Example `input.css`:

```css
/* Charter: thin orchestrator — only @tailwind and @import. No other rules. */

@tailwind base;
@import "./tokens.css";
@import "./base.css";

@tailwind components;
@import "./layout.css";
@import "./components.css";

@tailwind utilities;
@import "./effects.css";
```

---

## Example design tokens

A working `:root` block for a project management tool. Adjust values to match your design language.

```css
/* tokens.css — Charter: only :root { --… } and [data-theme="…"] blocks */

:root {
  /* Typography */
  --font-sans: 'Inter', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', 'Fira Code', monospace;

  --text-xs:   0.75rem;
  --text-sm:   0.875rem;
  --text-base: 1rem;
  --text-lg:   1.125rem;
  --text-xl:   1.25rem;
  --text-2xl:  1.5rem;
  --text-3xl:  1.875rem;
  --text-4xl:  2.25rem;

  --leading-tight:  1.2;
  --leading-snug:   1.375;
  --leading-normal: 1.6;

  /* Colour — cool neutral base, single blue accent */
  --color-accent:       #2563eb;
  --color-accent-hover: #1d4ed8;
  --color-focus:        #2563eb;

  --color-success: #16a34a;
  --color-warning: #d97706;
  --color-error:   #dc2626;
  --color-info:    #0284c7;

  --color-bg:           #ffffff;
  --color-surface:      #f8fafc;
  --color-surface-2:    #f1f5f9;
  --color-border:       #e2e8f0;
  --color-border-focus: #93c5fd;

  --color-text:         #0f172a;
  --color-text-muted:   #64748b;
  --color-text-disabled:#94a3b8;

  /* Spacing — 4px base */
  --space-1:  0.25rem;   /*  4px */
  --space-2:  0.5rem;    /*  8px */
  --space-3:  0.75rem;   /* 12px */
  --space-4:  1rem;      /* 16px */
  --space-6:  1.5rem;    /* 24px */
  --space-8:  2rem;      /* 32px */
  --space-12: 3rem;      /* 48px */
  --space-16: 4rem;      /* 64px */

  /* Shape — low radius signals precision */
  --radius-sm:   2px;
  --radius-md:   4px;
  --radius-lg:   8px;
  --radius-full: 9999px;

  /* Shadow */
  --shadow-sm: 0 1px 2px rgb(0 0 0 / 0.05);
  --shadow-md: 0 4px 6px rgb(0 0 0 / 0.07), 0 2px 4px rgb(0 0 0 / 0.05);
  --shadow-lg: 0 10px 15px rgb(0 0 0 / 0.1), 0 4px 6px rgb(0 0 0 / 0.05);

  /* Motion */
  --duration-fast:   100ms;
  --duration-normal: 200ms;
  --ease-out: cubic-bezier(0.16, 1, 0.3, 1);

  /* Z-index layers */
  --z-sticky:  10;
  --z-overlay: 50;

  /* Breakpoints */
  --bp-sm:  640px;
  --bp-md:  768px;
  --bp-lg:  1024px;
  --bp-xl:  1280px;
}

[data-theme="dark"] {
  --color-bg:         #0f172a;
  --color-surface:    #1e293b;
  --color-surface-2:  #334155;
  --color-border:     #334155;
  --color-text:       #f1f5f9;
  --color-text-muted: #94a3b8;
}
```

---

## Example component: button

A complete button component with all five states. Use this as the template for every interactive component.

```css
/* components.css */

.ui-button {
  display: inline-flex;
  align-items: center;
  gap: var(--space-2);
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-md);
  font-size: var(--text-sm);
  font-weight: 500;
  cursor: pointer;
  transition: background var(--duration-fast) var(--ease-out),
              color     var(--duration-fast) var(--ease-out);
}

/* Modifiers */
.ui-button-primary {
  background: var(--color-accent);
  color: #fff;
  border: none;
}

.ui-button-ghost {
  background: transparent;
  color: var(--color-text);
  border: 1px solid var(--color-border);
}

.ui-button-danger {
  background: var(--color-error);
  color: #fff;
  border: none;
}

/* States — declare all five for every modifier */
.ui-button-primary:hover  { background: var(--color-accent-hover); }
.ui-button-ghost:hover    { background: var(--color-surface-2); }

.ui-button:focus-visible {
  outline: 2px solid var(--color-focus);
  outline-offset: 2px;
}

.ui-button:disabled,
.ui-button.is-disabled {
  opacity: 0.5;
  cursor: not-allowed;
  pointer-events: none;
}

.ui-button.is-loading {
  position: relative;
  color: transparent; /* hide label while spinner shows */
}

.ui-button.is-loading::after {
  content: '';
  position: absolute;
  inset: 0;
  margin: auto;
  width: 1em;
  height: 1em;
  border: 2px solid currentColor;
  border-top-color: transparent;
  border-radius: 50%;
  animation: spin 0.6s linear infinite;
}

@keyframes spin { to { transform: rotate(360deg); } }
```

---

## Example component: form field

Shows composition — label, input, help text, and error message as a unit.

```css
.ui-form-field {
  display: flex;
  flex-direction: column;
  gap: var(--space-1);
}

.ui-form-field label {
  font-size: var(--text-sm);
  font-weight: 500;
  color: var(--color-text);
}

.ui-form-field input,
.ui-form-field textarea,
.ui-form-field select {
  padding: var(--space-2) var(--space-3);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  font-size: var(--text-base);
  color: var(--color-text);
  background: var(--color-bg);
}

.ui-form-field input:focus-visible {
  outline: 2px solid var(--color-focus);
  outline-offset: 0;
  border-color: var(--color-border-focus);
}

.ui-form-field .field-help {
  font-size: var(--text-sm);
  color: var(--color-text-muted);
}

.ui-form-field .field-error {
  font-size: var(--text-sm);
  color: var(--color-error);
}

.ui-form-field.has-error input {
  border-color: var(--color-error);
}
```

Usage in HTML:

```html
<div class="ui-form-field has-error">
  <label for="email">Email address</label>
  <input
    id="email"
    type="email"
    aria-describedby="email-error"
    value="not-an-email"
  >
  <p id="email-error" class="field-error">Enter a valid email address.</p>
</div>
```

---

## Theme switching

A single `data-theme` attribute on `<html>` switches the entire token set. No class swap, no CSS rebuild.

```js
// Toggle dark mode
const root = document.documentElement;

function toggleTheme() {
  const isDark = root.getAttribute('data-theme') === 'dark';
  root.setAttribute('data-theme', isDark ? 'light' : 'dark');
  localStorage.setItem('theme', isDark ? 'light' : 'dark');
}

// Restore preference on load — run before first paint to avoid flash
(function () {
  const saved = localStorage.getItem('theme');
  const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
  if (saved === 'dark' || (!saved && prefersDark)) {
    document.documentElement.setAttribute('data-theme', 'dark');
  }
})();
```

---

## When to add a new CSS file

The five-file split is the right size for most projects. Add a sixth only when all of these are true:

- The content is genuinely page-scoped or output-scoped (not reusable).
- Adding it to `effects.css` would push that file past a single screen.
- It does not compose well with the existing component vocabulary even with a modifier.

Examples that might justify a sixth file:

- `print.css` — print-specific overrides for a document view
- `pages/marketing-hero.css` — one-off landing page layout with a custom hero

Give the new file a charter comment. Nothing else imports from it.

---

## When to stop using utility strings entirely

Moving from Pattern A (utilities for layout) to Pattern B (custom CSS owns everything) is a one-way door. Only make the jump when all of these are true:

- The component vocabulary has been stable for two consecutive releases.
- The utility strings in templates feel like friction, not convenience — at least two contributors agree.
- A visual regression test suite covers every component at every breakpoint.

Until then, stay on Pattern A.
