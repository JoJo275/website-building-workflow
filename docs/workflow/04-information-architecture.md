# Information Architecture

Defines how content and pages are organised before any visual design begins.

## What to Define

- Sitemap — every page that exists
- Route map — the URL structure
- Navigation structure — what appears in menus
- User flows — paths through the site
- Page hierarchy — which pages are parent/child

## Example Route Map

```text
/
  landing
  pricing
  features
  docs
  login
  signup

/app
  dashboard
  inbox
  item/:id
  analytics
  settings
```

## Good IA Principles

### Group related pages together

Pages that serve the same user goal should live under the same parent in the sitemap and the same section of the nav. If a user is comparing pricing and reading feature details, both pages belong under the marketing section — not scattered across unrelated areas. Grouping reduces the number of decisions a user has to make to find what they need.

### Match the URL structure to the navigation

The URL a user sees in the address bar should reflect where they are in the site hierarchy. If the nav shows **App → Settings → Billing**, the URL should be `/app/settings/billing`, not `/billing` or `/user/account/payment`. Mismatched URLs confuse users who share links, use the back button, or try to navigate by editing the URL directly.

### Avoid deep nesting beyond three levels

A hierarchy deeper than three levels (`/level-1/level-2/level-3`) becomes hard to navigate and hard to reason about. If you find yourself going four or five levels deep, it is usually a sign that the content can be reorganised into a flatter structure or split into a separate section. Deep nesting also makes breadcrumbs and mobile navigation harder to implement cleanly.

### Name pages by what the user does, not internal jargon

Page names should reflect the user's task or goal, not the organisation's internal terminology. `/dashboard` is clearer than `/control-panel`. `/account` is clearer than `/user-profile-management`. `/sign-up` is clearer than `/registration`. If a page name only makes sense to someone who already works on the product, it needs to be renamed.

## Output

A route map document.
Use the [Route Map template](../starters/route-map.md).
