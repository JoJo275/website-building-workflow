# Wireframes

Wireframes are low-detail layout plans. They answer structural questions before visual design begins.

## What Wireframes Answer

```text
Where does navigation go?
Where is the main action?
What information appears first?
What can be hidden or collapsed?
What must always be visible?
```

## Rules

- Start in grayscale
- Avoid colours, gradients, shadows, and detailed branding until the structure works
- Use placeholder text and boxes for images
- Focus on layout and hierarchy, not style

## What to Wireframe

- Every unique page layout
- Key empty states
- Key error states
- Mobile layout variants for complex screens

## Examples

### Landing page

```text
+------------------------------------------+
|  Logo               Nav links    [CTA]   |
+------------------------------------------+
|                                          |
|          [ Headline - one sentence ]     |
|          [ Subheadline - sentence ]      |
|          [ Primary CTA button ]          |
|                                          |
+------------------------------------------+
|  [Icon]        [Icon]        [Icon]      |
|  Feature 1     Feature 2     Feature 3   |
|  Short desc    Short desc    Short desc  |
+------------------------------------------+
|         [ Testimonial / social proof ]   |
|                  [ Final CTA ]           |
+------------------------------------------+
|  Footer links                    Legal   |
+------------------------------------------+
```

### Dashboard

```text
+----------+-------------------------------+
|          |  Page title          User v   |
|  Nav     +-------------------------------+
|          |  [Stat]   [Stat]   [Stat]     |
|  Home    +------------------+------------+
|  Inbox   |                  |            |
|  Projects|   Main content   |  Sidebar   |
|  Settings|   (chart/table)  |  (detail)  |
|          |                  |            |
+----------+------------------+------------+
```

### Form or detail page

```text
+------------------------------------------+
|  Logo               Nav links    [User]  |
+------------------------------------------+
|  Breadcrumb > Path > Current page        |
|  Page title                              |
+----------------------+-------------------+
|                      |                   |
|  [ Field label ]     |  Summary / info   |
|  [ ____________ ]    |  box              |
|                      |                   |
|  [ Field label ]     |  [ Action btn ]   |
|  [ ____________ ]    |                   |
|                      |                   |
|  [ Submit ]          |                   |
|                      |                   |
+----------------------+-------------------+
```

## Common Tools

- **Paper and pen** — fastest for early exploration; work out the layout before opening any software
- **Figma** — recommended for digital wireframes; easy to share, annotate, and hand off to a developer
- **Excalidraw** — browser-based with no sign-up required; good for quick sketches and rough flows
- **FigJam** — better for mapping user flows and page relationships than pixel-precise wireframes

See [Design Tools](../tools/design.md) for full details.

## Output

Wireframe images exported to `design-source/exports/`.
Reference them in screen specs using the [Screen Spec template](../starters/screen-spec.md).
