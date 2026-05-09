# Product Planning

> Start with what users need to do, not what the site should look like.

## Define the Goal

Before design or code, clarify what the site is supposed to do.

| Site type | Goal |
|-----------|------|
| Marketing site | Get visitors to understand the product and sign up |
| Portfolio | Show credibility and examples of work |
| SaaS app | Let users sign up, log in, and complete workflows |
| E-commerce | Help users browse, compare, buy, and manage orders |
| Blog / content site | Publish searchable, readable articles |

This step determines everything else.

## Platform Decision

Decide early whether the site is primarily desktop or mobile. This affects layout, navigation patterns, input design, and what features are feasible.

| Platform priority | When to choose it |
|---|---|
| Desktop-first | Complex workflows, data-heavy dashboards, admin tools, productivity apps used at a desk |
| Mobile-first | Consumer-facing apps, high street businesses, content browsing, anything users access on the go |
| Fully responsive (equal) | Marketing sites, portfolios, e-commerce, blogs — visited from anywhere |

Most sites should be responsive, but knowing which platform to prioritise prevents design and implementation conflicts later.

**Key questions:**

- Where will most users access this site?
- Are there touch-only interactions (swipe, tap-and-hold) that only make sense on mobile?
- Does the layout require a wide viewport to work (e.g. multi-column dashboards)?
- Are there features that should be hidden, simplified, or deferred on smaller screens?

Document the answer. It becomes a constraint for wireframes, visual design, and responsive CSS breakpoints.

## Questions to Answer First

```text
What should users be able to do?
What should users understand quickly?
What is the primary action on each page?
What is the success condition?
What does the site or app not need to do yet?
```

## Product Task Example

```markdown
# Product Tasks

Users need to:

- Understand what the product does
- Sign up or log in
- Complete the main workflow
- Review results and status
- Configure settings
- Recover from errors
```

## Common Planning Mistakes

- Starting with visual design before defining user tasks
- Building features nobody asked for
- Not writing down what the site should NOT do
- Designing for the ideal case only (ignoring empty/error states)

## Common Tools

- **Any text editor or Notion** — write the product brief in plain text first; clarity matters more than format
- **FigJam** — sketch user flows and early page lists as a visual diagram before writing them down
- **Linear or GitHub Issues** — log scope decisions and flag out-of-scope items during planning
- **ChatGPT or Claude** — challenge assumptions, generate user stories, or stress-test the brief

See [Tools Overview](../tools/index.md) for a full reference.

## Output

A short product brief that can be handed to a designer or developer.
Use the [Product Brief template](../starters/product-brief.md).

## Research and References

Before designing, gather:

- Competitor websites
- Design references
- Target audience notes
- Product requirements
- Brand examples
- Content examples

For a SaaS dashboard, you might study Linear, Stripe, PostHog, Vercel, Plain, and Intercom.

This is not for copying. It is for understanding patterns your users already recognise.
