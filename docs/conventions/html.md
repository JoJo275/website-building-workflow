# Semantic HTML

The most important frontend decision is also the cheapest: use the right HTML element for what something *is*, before reaching for a class or a framework.

## Why it matters

| Benefit | What it means in practice |
|---|---|
| Accessibility for free | Screen readers, voice control, and keyboard users navigate by landmarks (`<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>`) and headings. A page built from `<div>`s is invisible to that class of users. |
| No JavaScript needed for built-in behaviour | `<button>` is keyboard-activatable and has the right role. `<dialog>` traps focus. `<details>`/`<summary>` is a free disclosure widget. `<form>` validates without a line of JS. |
| Better SEO and link previews | `<article>`, `<time datetime="…">`, and `<address>` carry meaning that crawlers use. |
| Smaller, cheaper HTML | The right tag needs fewer classes. `<nav>` replaces `<div role="navigation" aria-label="…" class="flex …">`. |

## Element reference

| Use case | Correct element |
|---|---|
| Page top with logo and primary navigation | `<header>` containing `<h1>` and `<nav>` |
| Main page content | `<main id="main">` — one per page; skip-link target |
| Self-contained chunk with a heading | `<section aria-labelledby="…">` |
| Re-publishable item (a blog post, a card row) | `<article>` |
| List of items | `<ul>` / `<ol>` with `<li>` — never `<div>` rows |
| Tabular data | `<table>` with `<thead>` / `<tbody>` / `<th scope="…">` |
| Action that *does* something | `<button type="button">` (or `type="submit"` inside a form) |
| Action that *navigates* | `<a href="…">` |
| Form input with a label | `<label for="…">` paired with `<input id="…">` — always together |
| Group of related form fields | `<fieldset>` + `<legend>` |
| Modal dialog | `<dialog>` — use `.showModal()`, not `.show()` |
| Disclosure or accordion | `<details>` + `<summary>` |
| Timestamp | `<time datetime="2026-04-30T12:00:00Z">` |
| Live update region | `<div role="status" aria-live="polite">` |
| Generic block wrapper with no semantics | `<div>` — only when no better tag applies |

## The `<div>` decision

`<div>` is a generic block container with no semantic meaning. Before reaching for it, run this check:

1. **Is this a landmark?** → `<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>`
2. **Is this a self-contained section?** → `<section>` (with a heading) or `<article>`
3. **Is this a list of similar things?** → `<ul>`, `<ol>`, or `<dl>`
4. **Is this navigation?** → `<nav>` + `<ul>` of `<a>`
5. **Is this a control?** → `<button>`, `<a>`, or `<input>`
6. **None of the above?** → `<div>` is correct. Move on.

If you find yourself adding `role="button"` or `role="navigation"` to a `<div>`, stop — there is a real element for that. [ARIA](../glossary.md#aria) roles exist for cases where the right element genuinely does not exist, which is rare.

## Tags carry meaning, classes carry style

Apply this division consistently:

| Thing | Purpose |
|---|---|
| **Tag** | What the element *is* |
| **Class** | How the element *looks* |
| **`id`** | Unique anchor for labels, skip-links, and fragment URLs — never used for styling |
| **`data-state`** | JS-driven state hooks for open/closed, loading, etc. |
| **`data-theme`** | Theme switching — pairs with CSS custom property overrides |

Avoid inventing ad-hoc `data-*` attributes for styling. Keep them to `data-state` and `data-theme`.

When meaning lives in the tag, the entire site can be restyled by swapping a stylesheet without touching HTML. When meaning lives in the class (`<div class="header">`), the page is locked to that stylesheet.

## Forms

- Every input has a `<label for>` paired by `id`.
- Group related fields in `<fieldset><legend>…</legend>`.
- Error messages live in a sibling element linked with `aria-describedby="field-id-error"` on the input.
- Use native validation attributes (`required`, `minlength`, `pattern`) before adding JavaScript.
- Style with `:invalid` / `:user-invalid` — the latter only flags fields after the user has interacted with them, which is usually what you want.

## Accessibility floor

| Requirement | Why |
|---|---|
| Heading levels are sequential — `<h1>` once per page, then `<h2>`s, no skipping | Screen readers use headings to navigate; gaps break the outline |
| Colour contrast ≥ 4.5:1 for body text, 3:1 for large text and UI borders | [WCAG](../glossary.md#wcag) AA minimum |
| Every image has `alt=""` (decorative) or descriptive alt text | Screen readers read alt text aloud |
| [Skip-link](../glossary.md#skip-link) to `#main` as the first focusable element | Keyboard users need a way past the nav on every page |
| All interactive elements reachable and operable by keyboard alone | Mouse-only UIs exclude a significant percentage of users |
| Status indicators use icon + text + colour — never colour alone | Required for colour-blind and monochrome-print paths |

## What to avoid

| Pattern | Problem |
|---|---|
| `<a href="#">` used as a button | Pollutes browser history, breaks middle-click — use `<button type="button">` |
| `onclick="…"` attributes in HTML | Logic scattered across markup — use `addEventListener` in JS |
| `role="button"` on a `<div>` | `<button>` already exists and handles keyboard, focus, and ARIA correctly |
| Positive `tabindex` values | Breaks the natural tab order — never use `tabindex` above 0 |
| Icon-only controls with no accessible label | Add `aria-label` or a visually-hidden `<span>` |
