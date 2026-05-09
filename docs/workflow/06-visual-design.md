# Visual Design

Applies colour, typography, and style to a working wireframe.

## Design Language

Before opening Figma, define what the site should feel like. This is the design brief — a short, written description of the intended experience. It gives every visual decision a reference point.

### What to define

#### Tone and personality

Choose three to five adjectives that describe how the site should feel.

```text
Examples:
Clean, trustworthy, and calm        → fintech, healthcare, productivity tools
Bold, energetic, and playful        → consumer apps, games, youth brands
Minimal, precise, and technical     → developer tools, APIs, CLIs
Warm, approachable, and friendly    → community platforms, onboarding-heavy apps
Premium, refined, and confident     → agencies, luxury brands, editorial sites
```

#### What the site must accommodate

Who uses it, where, and how. This defines constraints before any pixels are drawn.

```text
- Who: developers, non-technical managers, or general consumers?
- Where: desktop-first or mobile-first? Low-bandwidth environments?
- How: quick one-time tasks, or long sessions with complex workflows?
- Accessibility: does it need to meet WCAG AA? Screen reader support?
- Internationalisation: right-to-left scripts, variable text lengths?
```

#### Visual direction

How the personality translates into tangible design decisions.

| Feeling | Likely translation |
|---|---|
| Clean and minimal | Lots of whitespace, small type scale, muted palette, no decorative shadows |
| Bold and energetic | Strong typographic hierarchy, saturated accent colour, tighter spacing |
| Warm and approachable | Rounded corners, soft shadows, friendly sans-serif, slightly warm neutrals |
| Technical and precise | Monospace accents, dense information layout, low-contrast neutrals, sharp edges |
| Premium and refined | Generous spacing, serif or high-quality sans, restrained palette, subtle motion |

#### Core constraints

Decisions that rule things in or out early.

```text
Shape language: rounded (large radius) or sharp (0–2px radius)?
Density: spacious (lots of breathing room) or compact (more content per screen)?
Colour temperature: warm, cool, or neutral base?
Type scale: one typeface or two? Serif or sans-serif for body?
Motion: static or animated transitions? Subtle or expressive?
Iconography: filled, outlined, or duotone?
```

### Example design language brief

```text
Product: TaskFlow — project management for small software teams

Tone: Clean, efficient, and calm. Professional without being corporate.
      Should feel like a well-made tool, not a flashy consumer app.

Users: Developers and small team leads on desktop, mostly in long sessions.
       Occasional mobile access for quick status checks.

Shape language: Low border radius (4px). Sharp edges signal precision.
Density: Moderate. More content-dense than a consumer app, but not cramped.
Colour: Cool neutral base. Single blue accent. Red only for destructive actions.
Type: One sans-serif (Inter). No serif. Strong weight contrast for hierarchy.
Motion: Minimal. Transitions under 150ms. No decorative animation.
Icons: Outlined. Lucide icon set.

This should feel like Linear or Vercel — not Trello or Notion.
```

Define this before the design system. Every token, spacing decision, and component style should be traceable back to it.

## Design Tokens

Design tokens are the named values that make up your design system. Define them before building any components. Every visual decision in the product — spacing, colour, shape, motion — should come from this list, not be invented per component.

These tokens are later expressed as CSS custom properties (see [Frontend → CSS](07-frontend.md)).

### Typography

| Token | What to decide | Example |
|---|---|---|
| Font family | One or two typefaces maximum. Define a fallback stack. | `Inter, system-ui, sans-serif` |
| Font scale | A limited set of sizes. Use a ratio (e.g. 1.25) or a named scale. | `12 / 14 / 16 / 18 / 20 / 24 / 30 / 36 / 48px` |
| Font weights | Two or three weights. More than three is rarely needed. | `400 (regular), 500 (medium), 700 (bold)` |
| Line height | Tighter for headings, looser for body. | Headings: `1.2`, Body: `1.6` |
| Letter spacing | Usually 0 for body; slight tracking for uppercase labels. | Labels: `0.05em` |
| Measure (line width) | Maximum character width per line for readable body text. | `65ch` — beyond ~75 chars, reading becomes tiring |
| Text colour hierarchy | Primary, secondary, muted, disabled. | `#111 / #555 / #888 / #bbb` |

### Colour

| Token group | What to define |
|---|---|
| Brand / accent | The primary action colour. Used for buttons, links, and focus rings. Keep to one. |
| Neutrals | A grey scale from near-white to near-black. Typically 8–10 steps. Used for backgrounds, borders, and text. |
| Semantic colours | Fixed-purpose colours: `success` (green), `warning` (amber), `error` (red), `info` (blue). |
| Surface colours | Background layers: page background, card surface, elevated panel. Usually the lightest 2–3 neutrals. |
| Border colour | Usually a mid-range neutral. Often one value covers most cases. |
| Focus ring | A high-contrast colour for keyboard focus indicators. Often the accent colour or a contrasting blue. |

Test all colour combinations for WCAG AA contrast (4.5:1 for body text, 3:1 for large text and UI elements).

### Spacing

Use a consistent multiplier-based scale. A 4px base is the most common.

```text
xs   —  4px
sm   —  8px
md   — 16px
lg   — 24px
xl   — 32px
2xl  — 48px
3xl  — 64px
4xl  — 96px
```

Apply these values to: margin, padding, gap, and layout gutters. Never use arbitrary values like `13px` or `22px` — they break visual rhythm.

### Shape

| Token | What to decide | Example |
|---|---|---|
| Border radius | One or two values. Sharp = 0–2px. Rounded = 6–12px. Pill = 9999px. | `4px` for inputs, `8px` for cards |
| Border width | Usually 1px. Sometimes 2px for focus rings. | `1px` |
| Border colour | Single neutral token used across all dividers and outlines. | `--color-border: #e2e8f0` |

### Shadows and Elevation

Define a small named set. More than four levels is usually unnecessary.

```text
none   — no shadow (flat surfaces)
sm     — subtle lift (cards, dropdowns on light backgrounds)
md     — moderate lift (modals, popovers)
lg     — strong lift (dialogs, full overlays)
```

Shadows should follow your design language. Minimal/technical sites often use flat colour borders instead of shadows.

### Effects and Motion

| Token | What to decide | Example |
|---|---|---|
| Transition duration | Fast for micro-interactions, slower for larger reveals. | `100ms` hover, `200ms` panel open |
| Transition easing | Ease-out feels natural for elements entering the screen. | `ease-out`, `cubic-bezier(0.16, 1, 0.3, 1)` |
| Opacity (disabled) | Standard value for disabled elements. | `0.5` |
| Blur (backdrop) | For frosted-glass overlays or modal backdrops. | `blur(8px)` |

Respect `prefers-reduced-motion`. Wrap transitions in a media query if they are decorative.

### Component Inventory

Once tokens are defined, list every UI component the design needs. This becomes the build list.

```text
Buttons (primary, secondary, ghost, destructive)
Inputs (text, password, select, textarea, checkbox, radio)
Badges and status labels
Cards
Modal and drawer
Dropdown menu
Tooltip
Navbar
Sidebar
Pagination
Alert / toast
Table
Skeleton loader
Empty state
Avatar
```

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

After the visual design is stable, build a prototype to test how screens connect before writing any code.

### What a prototype is

A prototype is a clickable simulation of the product. It links Figma frames together so that clicking a button navigates to the next screen, opens a panel, or changes a state — without any real backend logic.

It is not a design. It is not code. It is a test of whether the flow makes sense.

### What a prototype is not

- It does not need real data
- It does not need working forms or API calls
- It does not need animations or pixel-perfect polish
- It does not need to cover every screen — only the critical paths

### What to prototype

Focus on the paths that matter most:

- The primary sign-up or onboarding flow
- The core user workflow (the thing the product exists to do)
- Any flow that involves multiple steps or conditional branching
- Screens with complex interactions (drawers, multi-step forms, modals)

### How to build one in Figma

1. Create a frame for each key screen in the flow
2. Use Figma's **Prototype** panel to add connections between frames
3. Set the trigger (On Click, On Hover, etc.) and the destination frame
4. Add transitions if useful — but keep them simple
5. Share the prototype link with teammates or test users

```text
Frame: Landing page
  → Click "Sign up"         → Frame: Signup form

Frame: Signup form
  → Click "Create account"  → Frame: Onboarding step 1

Frame: Dashboard
  → Click "View feedback"   → Frame: Feedback detail panel (overlay)
  → Click "Filter"          → Frame: Filter dropdown (overlay)
  → Click "Mark resolved"   → Frame: Dashboard (resolved state)
```

### What to test

Run through the prototype yourself first, then with at least one other person who has not seen the design. Ask:

- Can you find the primary action without being told where it is?
- Does the flow feel like the right number of steps?
- Is anything confusing, missing, or in the wrong order?
- Do you know where you are at each point in the flow?

Answers to these questions are free to act on now. They are expensive to act on after the frontend is built.

### Fidelity levels

| Fidelity | When to use |
|---|---|
| Low — linked wireframe frames | Early validation before visual design; fast to build and easy to change |
| Medium — linked visual design frames | Standard pre-build prototype; tests both flow and visual design together |
| High — micro-interactions, real-looking data | Only when the interaction detail matters (complex animations, gesture-based UI) |

Most projects need medium fidelity. High fidelity prototypes take significantly longer and rarely change the structural decisions.

### Handing off to development

Once the prototype is reviewed and the flow is signed off:

- Annotate frames with behaviour notes (what happens on hover, what the loading state looks like, what the error state says)
- Export the prototype link alongside the Figma design file
- Write a screen spec for complex screens using the [Screen Spec template](../starters/screen-spec.md)

The prototype answers *where does this go*. The screen spec answers *what does it do*.

## Tools

- **Figma** — primary tool for visual design, component libraries, and design system documentation
- **Coolors or Realtime Colors** — generate and test colour palettes quickly against real UI
- **Google Fonts or Fontpair** — browse and pair typefaces before committing to a font stack
- **Heroicons, Phosphor, or Lucide** — icon libraries with consistent styles; pick one and stick to it
- **Unsplash or Pexels** — placeholder images for mockups before real photography is available

See [Design Tools](../tools/design.md) for full details.

## Output

Figma file in `design-source/`. Exported assets in `design-source/exports/`.
