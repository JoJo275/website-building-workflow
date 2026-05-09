# Component Spec: UserAvatar

## Purpose

Displays a circular avatar for a user. Shows the user's profile image if available, otherwise falls back to their initials on a coloured background. Used in the header, comment threads, and member lists.

## Props / Inputs

| Prop | Type | Required | Notes |
|---|---|---|---|
| `name` | `string` | Yes | Used to generate initials and the accessible label |
| `imageUrl` | `string` | No | If omitted, the initials fallback is shown |
| `size` | `"sm" \| "md" \| "lg"` | No | Defaults to `"md"` (40px) |
| `onClick` | `() => void` | No | If provided, the avatar is rendered as a button |

## Variants

- **Default** — profile image displayed
- **Initials fallback** — no `imageUrl`, shows first and last initial
- **Small** — 24px, used in comment threads
- **Large** — 64px, used on profile pages
- **Interactive** — rendered as a `<button>` when `onClick` is provided
- **Loading** — skeleton placeholder while user data is fetching

## Behaviour

- If `imageUrl` is provided and loads successfully, the image fills the circle.
- If `imageUrl` fails to load, the component falls back to the initials variant silently.
- Initials are derived from the first character of the first and last word in `name`.
- Background colour for initials is deterministically derived from the name string so it is stable across renders.
- When `onClick` is provided, hovering shows a subtle ring and the cursor becomes a pointer.

## Accessibility

- When rendered as a button, `aria-label` is set to `"View profile for {name}"`.
- When decorative, `aria-hidden="true"` is applied and the image `alt` is empty.
- Focus ring must be visible in keyboard navigation.

## Acceptance Criteria

| Criterion | Status | Notes |
|-----------|--------|-------|
| Profile image renders correctly when a valid `imageUrl` is supplied | To do | |
| Initials fallback renders when no `imageUrl` is provided | To do | |
| Broken image URLs fall back to initials without a visible error | To do | |
| All three size variants render at the correct dimensions | To do | |
| Interactive variant is keyboard focusable and has a visible focus ring | To do | |
| Component passes axe accessibility checks | To do | |
