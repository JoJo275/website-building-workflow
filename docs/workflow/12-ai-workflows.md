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
