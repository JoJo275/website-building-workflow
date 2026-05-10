# Testing

Testing verifies the site or app works correctly across devices, browsers, and edge cases.

Before launch, check:

- Does it work?
- Does it work on mobile?
- Does it work in Chrome, Firefox, and Safari?
- Are errors handled?
- Are loading states handled?
- Is it accessible with keyboard only?
- Are forms validated?
- Is it fast enough?
- Does auth work correctly?
- Are permissions correct?

For a solo developer, you do not need enterprise-level QA at first, but you do need a checklist.

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

## Common Tools

- **Playwright** — end-to-end browser testing; runs real user flows in a real browser
- **Vitest or Jest** — unit and component testing for JavaScript and TypeScript
- **axe DevTools** — browser extension for automated accessibility checks against WCAG
- **Chrome DevTools** — inspect layout, simulate mobile viewports, and audit network requests manually
- **Lighthouse** — built into Chrome DevTools; audits performance, accessibility, and SEO in one pass

See [Dev Environment Tools](../tools/dev-environment.md) for testing and linting tool details.

## End-to-End Test Flows

Plan core user flows early, even if you write the tests later. Playwright can run these flows in a real browser, locally or in CI.

Example flows for a SaaS app:

```text
User signs up
User logs in
User opens inbox
User filters feedback
User opens feedback detail
User changes status
User adds tag
User logs out
```

You do not need Playwright on day one, but structure the app so core flows can be tested end-to-end later.

## Accessibility and Performance

Run Lighthouse and axe as a final quality pass before launch.

- **Lighthouse** — audits performance, accessibility, SEO, and best practices; runs from Chrome DevTools, command line, or CI
- **axe DevTools** — accessibility checks in browser, IDE, and CI workflows

A polished site is fast, accessible, and usable — not just visually correct.

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
