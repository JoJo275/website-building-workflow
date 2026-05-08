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

## Checklist

- [ ] Main user flow tested end-to-end
- [ ] Mobile layout verified at 375px
- [ ] Keyboard navigation works throughout
- [ ] Empty states display correctly
- [ ] Error states display correctly
- [ ] Form validation gives clear feedback
- [ ] Auth-protected routes reject unauthenticated users
- [ ] Automated tests pass in CI
