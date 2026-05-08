# Visual Design

Applies colour, typography, and style to a working wireframe.

## Design System Basics

```text
Colors
Font sizes
Spacing scale
Border radius
Buttons
Inputs
Cards
Badges
Modals
Tables
Navigation
```

## Core Properties to Define

| Property | Notes |
|---|---|
| Typography | Font family, sizes, weights, line heights |
| Colour | Brand palette, semantic colours (error, warning, success) |
| Spacing | Consistent scale (e.g. 4px, 8px, 16px, 24px, 32px) |
| Icons | Single icon library |
| Borders | Consistent radius and width |
| Shadows | Minimal set |

## States to Design

Every interactive component needs all states designed before handoff:

- Default
- Hover
- Focus
- Active
- Disabled
- Loading
- Empty
- Error

## Recommended Principle

```text
Figma defines appearance.
Markdown specs define behaviour.
Code implements both.
```

## Responsive Design

Design for mobile first. Define breakpoints and verify layouts at:

- 375px (small mobile)
- 768px (tablet)
- 1280px (desktop)

## Prototype

After the visual design is stable, create a prototype to test screen connections before writing code.

A prototype shows what happens when users interact:

```text
Click "Sign up"        → signup page
Click "View feedback"  → feedback detail panel opens
Click "Filter"         → dropdown opens
Click "Mark resolved"  → status changes
```

The prototype does not need real backend logic. It tests whether the flow makes sense.

Prototypes are typically built in Figma using interactive connections between frames.

## Output

Figma file in `design-source/`. Exported assets in `design-source/exports/`.
