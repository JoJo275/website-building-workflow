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

- Page headings and subheadings
- Button labels
- Empty-state messages
- Error messages
- Onboarding text
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

## Checklist

- [ ] Layout matches the design at all breakpoints
- [ ] Components handle loading, empty, and error states
- [ ] All interactive elements are keyboard accessible
- [ ] No hardcoded values that belong in config or API responses
- [ ] Lint and typecheck pass
