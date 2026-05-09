# Testing

Testing verifies the site or app works correctly across devices, browsers, and edge cases.

## Testing Types

| Type | What it covers |
|---|---|
| Manual QA | Visual layout, real user flows, edge cases |
| Unit tests | Individual functions and utilities |
| Component tests | UI components in isolation |
| Integration tests | Multiple parts working together |
| End-to-end tests | Full user flows in a real browser |
| Accessibility checks | Keyboard nav, screen reader, contrast |
| Performance checks | Load times, Core Web Vitals |

## Manual QA Questions

```text
Does it work?
Does it work on mobile?
Does it work in major browsers?
Are errors handled gracefully?
Are loading states visible and helpful?
Can it be used with keyboard navigation only?
Are forms validated with useful error messages?
Are permissions enforced correctly?
```

## Tools

- **Playwright** — end-to-end browser testing; runs real user flows in a real browser
- **Vitest or Jest** — unit and component testing for JavaScript and TypeScript
- **axe DevTools** — browser extension for automated accessibility checks against WCAG
- **Chrome DevTools** — inspect layout, simulate mobile viewports, and audit network requests manually
- **Lighthouse** — built into Chrome DevTools; audits performance, accessibility, and SEO in one pass

See [Dev Environment Tools](../tools/dev-environment.md) for testing and linting tool details.

## Checklist

| Check | Status | Notes |
|-------|--------|-------|
| Main user flow tested end-to-end | To do | |
| Mobile layout verified at 375px | To do | |
| Keyboard navigation works throughout | To do | |
| Empty states display correctly | To do | |
| Error states display correctly | To do | |
| Form validation gives clear feedback | To do | |
| Auth-protected routes reject unauthenticated users | To do | |
| Automated tests pass in CI | To do | |
