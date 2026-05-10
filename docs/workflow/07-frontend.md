# Frontend

Frontend covers everything that runs in the browser: structure, style, interactivity, and API integration.

## What Frontend Includes

- HTML structure
- CSS and styling
- JavaScript and TypeScript
- Framework components (React, Vue, Svelte, etc.)
- Routing
- API calls
- Loading states
- Error states
- Responsive layouts
- Accessibility

## Common Components

```text
Navbar
Sidebar
Button
Input
Card
Table
Modal
Dropdown
StatusBadge
DetailPanel
DashboardMetric
```

## CSS

CSS controls every visual property of the page. Knowing the core concepts and patterns prevents the most common frontend problems.

### Custom properties (design tokens in code)

The design tokens defined in [Visual Design](06-visual-design.md) are implemented as CSS custom properties. Define them once on `:root` and reference them everywhere.

```css
:root {
  /* Typography */
  --font-sans: Inter, system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', monospace;

  --text-xs:   0.75rem;   /*  12px */
  --text-sm:   0.875rem;  /*  14px */
  --text-base: 1rem;      /*  16px */
  --text-lg:   1.125rem;  /*  18px */
  --text-xl:   1.25rem;   /*  20px */
  --text-2xl:  1.5rem;    /*  24px */
  --text-3xl:  1.875rem;  /*  30px */
  --text-4xl:  2.25rem;   /*  36px */

  --leading-tight:  1.2;
  --leading-normal: 1.5;
  --leading-loose:  1.75;

  --measure: 65ch;  /* max line width for readable body text */

  /* Spacing */
  --space-1:  0.25rem;  /*  4px */
  --space-2:  0.5rem;   /*  8px */
  --space-3:  0.75rem;  /* 12px */
  --space-4:  1rem;     /* 16px */
  --space-6:  1.5rem;   /* 24px */
  --space-8:  2rem;     /* 32px */
  --space-12: 3rem;     /* 48px */
  --space-16: 4rem;     /* 64px */

  /* Colour */
  --color-accent:    #2563eb;
  --color-accent-hover: #1d4ed8;
  --color-success:   #16a34a;
  --color-warning:   #d97706;
  --color-error:     #dc2626;

  --color-bg:        #ffffff;
  --color-surface:   #f8fafc;
  --color-border:    #e2e8f0;

  --color-text:      #0f172a;
  --color-text-muted:#64748b;

  /* Shape */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
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

Never hardcode a colour, size, or spacing value inside a component rule. Reference a token instead.

### Box model

Every element is a box. Understanding this prevents most layout bugs.

```css
/* Make padding and border part of the element's width — not additive */
*, *::before, *::after {
  box-sizing: border-box;
}
```

Without `box-sizing: border-box`, a `200px` wide element with `16px` padding becomes `232px` wide — which breaks layouts.

### Layout

Use **Flexbox** for one-dimensional alignment (rows or columns). Use **Grid** for two-dimensional layouts (rows and columns together).

```css
/* Flexbox — horizontal nav */
.nav {
  display: flex;
  align-items: center;
  gap: var(--space-4);
}

/* Grid — page layout with sidebar */
.layout {
  display: grid;
  grid-template-columns: 240px 1fr;
  gap: var(--space-6);
}

/* Grid — responsive card grid without media queries */
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: var(--space-6);
}
```

### Responsive design

Use mobile-first media queries. Start with the smallest layout and add breakpoints as the viewport grows.

```css
/* Mobile-first: this applies at all sizes */
.sidebar {
  display: none;
}

/* Show sidebar above tablet width */
@media (min-width: 768px) {
  .sidebar {
    display: block;
  }
}
```

Common breakpoints:

| Name | Min width | Typical use |
|---|---|---|
| sm | 480px | Large mobile |
| md | 768px | Tablet portrait |
| lg | 1024px | Tablet landscape / small desktop |
| xl | 1280px | Desktop |
| 2xl | 1536px | Wide desktop |

Use `rem` or `ch` for font sizes and line widths. Use `%`, `fr`, or `clamp()` for layout widths. Avoid fixed `px` widths for anything that needs to flex.

### Typography

```css
body {
  font-family: var(--font-sans);
  font-size: var(--text-base);
  line-height: var(--leading-normal);
  color: var(--color-text);
}

/* Constrain prose width for readability */
.prose {
  max-width: var(--measure);
}

h1 { font-size: var(--text-4xl); line-height: var(--leading-tight); font-weight: 700; }
h2 { font-size: var(--text-3xl); line-height: var(--leading-tight); font-weight: 700; }
h3 { font-size: var(--text-2xl); line-height: var(--leading-tight); font-weight: 600; }
```

### States and transitions

Every interactive element needs visible feedback for hover, focus, active, and disabled.

```css
.button {
  background: var(--color-accent);
  color: #fff;
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-sm);
  border: none;
  cursor: pointer;
  transition: background var(--duration-fast) var(--ease-out);
}

.button:hover  { background: var(--color-accent-hover); }
.button:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 2px;
}
.button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

### Reduced motion

Respect users who have configured their OS to reduce animation.

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    transition-duration: 0.01ms !important;
    animation-duration: 0.01ms !important;
  }
}
```

### CSS reset

Apply a minimal reset before any other styles to remove browser inconsistencies.

```css
*, *::before, *::after { box-sizing: border-box; }

* {
  margin: 0;
  padding: 0;
}

img, video, svg { display: block; max-width: 100%; }

input, button, textarea, select { font: inherit; }
```

## Implementation Order

1. Static layout (HTML + CSS only)
2. Component structure
3. Routing
4. API integration
5. Loading and error states
6. Responsive adjustments
7. Accessibility pass

## Content and Copy

Copy is often underestimated in frontend work. The words on every element matter.

Content includes:

- Homepage copy
- Page headings and subheadings
- Button labels
- Empty-state messages
- Error messages
- Onboarding text
- Documentation
- Pricing descriptions
- Emails
- Legal pages
- Tooltip descriptions
- Form labels and help text

Bad button label:

> Submit

Better, depending on context:

- Send feedback
- Create project
- Invite teammate
- Mark as resolved

Write copy before or alongside implementation, not as an afterthought.

## Common Tools

- **React + Next.js** — the most common choice for component-based apps with routing and server rendering
- **Astro** — good for content-heavy or mostly-static sites with minimal JavaScript
- **Tailwind CSS** — utility-first styling; keeps styles co-located with components
- **TypeScript** — adds type safety; catches mistakes at edit time rather than runtime
- **Storybook** — develop and review UI components in isolation, outside the full app; covers hard-to-reach states without needing the full app running

## Storybook Workflow

Storybook is one of the better workflows for component-heavy apps. Build each component and all its variants in Storybook before wiring it into a real screen.

For a feedback card component, stories might look like:

```text
FeedbackCard / default
FeedbackCard / urgent
FeedbackCard / resolved
FeedbackCard / with many tags
FeedbackCard / long message
FeedbackCard / mobile
FeedbackCard / loading skeleton
```

This pairs well with Copilot — ask it to implement one story at a time. Each story is a small, verifiable unit of work with a clear acceptance condition (does it match the design?). Once all stories pass, wiring the component into the dashboard is straightforward.

Define stories in the component spec before implementation. See [Component Spec](../starters/component-spec.md).

See [Frontend Tools](../tools/frontend.md) for a full breakdown of frameworks, CSS tools, and build systems.

## Checklist

| Check | Status | Notes |
|-------|--------|-------|
| Layout matches the design at all breakpoints | To do | |
| Components handle loading, empty, and error states | To do | |
| All interactive elements are keyboard accessible | To do | |
| No hardcoded values that belong in config or API responses | To do | |
| Lint and typecheck pass | To do | |
