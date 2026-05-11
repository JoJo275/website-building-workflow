# Frontend Tools

Frameworks, libraries, styling tools, and build systems for building what users see in the browser.

## Frameworks

### React

A JavaScript library for building component-based UIs. The most widely used frontend library.

- Component-based architecture
- Large ecosystem and community
- Flexible — pairs with any meta-framework or build tool

<https://react.dev>

### Next.js

A React [meta-framework](../glossary.md#meta-framework) with file-based routing, [server-side rendering](../glossary.md#ssr), static generation, and API routes.

**Good for:** Full-stack apps, marketing sites, dashboards, anything that needs SEO or server rendering.

<https://nextjs.org>

### Vue

A progressive JavaScript framework with a gentler learning curve than React.

- Single-file components (HTML, CSS, JS in one file)
- Good for simpler apps or teams coming from HTML/CSS backgrounds

<https://vuejs.org>

### Svelte / SvelteKit

A compiler-based framework that produces smaller bundles. SvelteKit is the full-stack [meta-framework](../glossary.md#meta-framework).

- Very little boilerplate
- Reactivity built into the language
- SvelteKit is the equivalent of Next.js for Svelte

<https://svelte.dev> / <https://kit.svelte.dev>

### Astro

A static site framework optimised for content-heavy sites with minimal JavaScript.

- Ships zero JS by default
- Supports components from React, Vue, Svelte, etc.
- Excellent for docs, blogs, and marketing sites

<https://astro.build>

## CSS and Styling

### Tailwind CSS

A [utility-first](../glossary.md#utility-first-css) CSS framework. Instead of writing custom CSS, you apply small utility classes directly in HTML.

```html
<button class="bg-indigo-600 text-white px-4 py-2 rounded hover:bg-indigo-700">
  Submit
</button>
```

- Consistent spacing, colour, and sizing scales
- No naming conventions required
- Excellent with component-based frameworks

<https://tailwindcss.com>

### [CSS Modules](../glossary.md#css-modules)

Scoped CSS files where class names are automatically made unique per component. No global style conflicts.

- Built into Next.js, Vite, and most build tools
- Plain CSS syntax
- Good for projects that prefer standard CSS

### Styled Components / Emotion

CSS-in-JS libraries for writing CSS inside JavaScript files, co-located with components.

- Dynamic styles based on props
- Scoped by default
- Works well with React

<https://styled-components.com>

## UI Component Libraries

### shadcn/ui

A collection of accessible, unstyled components built on Radix UI and styled with Tailwind. Components are copied into your project rather than installed as a dependency.

- Full control over styling
- Built on accessible primitives
- Works with Next.js and Vite

<https://ui.shadcn.com>

### Radix UI

Unstyled, accessible component primitives (modals, dropdowns, tooltips, etc.).

- Handles all accessibility and keyboard behaviour
- Bring your own styles
- The foundation used by shadcn/ui

<https://radix-ui.com>

### Mantine

A full-featured React component library with its own styling system.

- Large set of components out of the box
- Built-in theming
- Good for dashboards and internal tools

<https://mantine.dev>

### Material UI (MUI)

Google Material Design implemented for React.

- Very large component set
- Strong in enterprise and dashboard applications
- Heavier and more opinionated than Radix/shadcn

<https://mui.com>

## Build Tools

### Vite

The modern standard for frontend build tooling. Extremely fast hot module replacement in development.

- Works with React, Vue, Svelte, and vanilla JS
- Faster than Webpack for most projects
- Simple config

<https://vitejs.dev>

### TypeScript

A typed superset of JavaScript. Catches errors at build time and improves editor tooling.

- Required for most serious frontend projects
- Works with all major frameworks
- Adds interfaces, types, and generics to JavaScript

<https://typescriptlang.org>

## Choosing a Stack

| Goal | Recommended stack |
|---|---|
| Full-stack web app | Next.js + Tailwind + shadcn/ui |
| Static/content site | Astro + Tailwind |
| Simple SPA | React + Vite + Tailwind |
| Vue preference | Nuxt + Tailwind |
| Dashboard (internal) | Next.js or Vite + Mantine or MUI |
