# AI Task Brief

## Task

Add a dark mode toggle button to the site header that persists the user's preference using `localStorage`.

## Context

Relevant files:

- `src/components/Header.tsx`
- `src/styles/tokens.css`
- `src/hooks/useTheme.ts`

Current behaviour:

The site always renders in light mode. There is no mechanism for the user to switch themes.

Desired behaviour:

A toggle button in the top-right of the header switches between light and dark mode. The selected preference is saved to `localStorage` and restored on page load. Dark mode is applied by adding a `.dark` class to the `<html>` element.

## Constraints

- Do not change unrelated files.
- Reuse existing components where possible.
- Do not introduce new dependencies without approval.
- Preserve existing public behaviour unless explicitly changed.
- Do not modify any existing CSS colour values — only add dark-mode overrides via the `.dark` class.

## Acceptance Criteria

| Criterion | Status | Notes |
|-----------|--------|-------|
| Toggle button is visible in the header on all screen sizes | To do | |
| Clicking the toggle switches the theme immediately without a page reload | To do | |
| Preference persists across page reloads via `localStorage` | To do | |
| Dark mode applies the correct colour tokens defined in `tokens.css` | To do | |
| No flash of incorrect theme on initial load | To do | |

## Validation

```bash
npm test
npm run lint
npm run typecheck
```
