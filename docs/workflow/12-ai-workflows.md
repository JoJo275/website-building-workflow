# AI Workflows

Using AI tools effectively for planning, coding, and reviewing.

## The Better Workflow

```text
Idea
→ task brief
→ constraints
→ acceptance criteria
→ plan
→ small implementation
→ test and verify
→ review and refactor
→ commit
```

## Weak vs Strong Prompts

**Weak:**

```text
Idea
→ vague Copilot prompt
→ many files change
→ eyeball the result
→ keep prompting until it seems okay
```

**Strong:**

```text
Idea
→ task brief with context
→ constraints listed
→ acceptance criteria written
→ plan reviewed before code is written
→ small diff
→ tests run
→ diff reviewed manually
→ commit
```

## When to Use Each Mode

| Situation | Best AI Workflow |
|---|---|
| You are confused | Ask and explain mode |
| You need a feature | Spec → plan → edit |
| You need a tiny change | Inline edit |
| You have a bug | State hypotheses first |
| You want safer output | Write tests first |
| You repeat a task often | Prompt file |
| You want consistent behaviour | Repo custom instructions |
| You need full implementation | Agent mode with strict acceptance criteria |

## Good Prompt Example

```text
Update docs/workflow/07-frontend.md.

Goal:
Explain frontend implementation for beginners building real websites.

Constraints:
- Keep it practical.
- Include components, routing, styling, API calls, states, and accessibility.
- Do not make it framework-specific only.
- Add a short checklist at the end.
```

## Recommended Uses for This Repo

- Drafting new workflow pages from a short outline
- Expanding checklist items with examples
- Reviewing a page for gaps and inconsistencies
- Generating template stubs to fill in manually

## The Three Truths

A website has three separate sources of truth. Keeping them aligned is the main challenge.

**Design truth** — what it should look like. Usually Figma.

**Behaviour truth** — what should happen when users interact. Usually markdown specs, user stories, or tickets.

**Code truth** — how it is actually implemented. Usually repo files, components, tests, and API routes.

Most friction with AI coding tools comes from providing only the design truth. A mockup tells the AI what something looks like, but not:

- What components exist
- What data powers the UI
- What states are required
- What routes this lives under
- What files should change
- What should not change

Provide all three truths before asking for code.

## Mental Model

Do not think of website creation as:

> Make design → convert to code

Think of it as:

```text
Define user tasks
→ design screens that support those tasks
→ define components, states, and data
→ implement in code
→ test against the intended behaviour
```

## Common Tools

- **GitHub Copilot** — inline completions and agent mode inside VS Code; good for focused, single-file edits
- **Cursor** — VS Code fork with deeper AI integration; supports multi-file context and codebase-wide edits
- **Claude or ChatGPT** — useful for planning, reviewing specs, and generating first drafts outside the editor
- **`.github/copilot-instructions.md`** — define project-specific conventions the AI follows automatically
- **Prompt files (`.prompt.md`)** — store repeatable task prompts in the repo for consistent AI-assisted work

See [Dev Environment Tools](../tools/dev-environment.md) for editor and AI tool details.

## Using /plan Before Implementation

Use `/plan` in Copilot agent mode before writing code for any non-trivial change.

Format the plan request with full context:

```text
/plan Implement the FeedbackCard component based on docs/ui/components/feedback-card.md and the Figma reference.

Before editing:
- list files you will change
- identify existing components to reuse
- identify any missing props or types
- do not modify backend files
```

Review the plan before accepting it. If the files listed look wrong or too broad, refine the prompt before proceeding.

`/plan` is for the immediate coding task only. Use markdown files for stable decisions and project structure.

## Visual QA After Implementation

After Copilot implements a UI, compare it against the design reference before committing.

Check:

- Sidebar width
- Card spacing
- Font sizes
- Line height
- Border radius
- Colour tokens
- Empty states
- Mobile layout
- Hover and focus states
- Loading states

AI-generated UI often gets the general layout right but misses exact values. This is where most visual drift happens.

## End-to-End Tests

Use Playwright for testing real app flows. Playwright supports Chromium, Firefox, and WebKit, and can run locally or in CI.

Plan core flows early, even if you write the tests later:

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

You do not need Playwright on day one, but structure the app so it can be tested end-to-end later.

## Accessibility and Performance

Run Lighthouse and axe as a final quality pass before launch.

- **Lighthouse** — audits performance, accessibility, SEO, and best practices; runs from Chrome DevTools, command line, or CI
- **axe DevTools** — accessibility checks in browser, IDE, and CI workflows

For a portfolio or SaaS app, a polished result means fast, accessible, and usable — not just visually correct.
