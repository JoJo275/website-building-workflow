# Website-Building Workflow Repo Guide

This file gathers the recommended structure and content for a repo that publishes an MkDocs site documenting a practical website-building workflow. The goal is to create a reusable personal playbook for planning, designing, building, testing, deploying, and iterating on websites and web apps.

---

## 1. Recommended Purpose of the Repo

The repo should act as a public or semi-public knowledge base for how websites are made.

It can be used as:

- A personal website-building playbook
- A reusable workflow reference for future projects
- A portfolio artifact showing how you think through product/design/engineering work
- A documentation hub for templates, checklists, and AI-assisted coding workflows

The repo should not just be random notes. It should contain reusable systems, templates, checklists, and examples.

---

## 2. Recommended GitHub Pages Setup

### Best setup

Use a separate project repo for the MkDocs guide:

```text
website-building-workflow
```

Publish it as a GitHub Pages project site:

```text
https://YOUR_USERNAME.github.io/website-building-workflow/
```

Keep the root GitHub Pages site separate:

```text
YOUR_USERNAME.github.io
```

Use that root site later as a personal homepage or portfolio hub that links to projects, docs, and apps.

### Recommended site layout

```text
YOUR_USERNAME.github.io/                  → personal homepage / portfolio hub
YOUR_USERNAME.github.io/website-workflow/ → website-building workflow guide
YOUR_USERNAME.github.io/project-docs/      → optional project-specific docs
```

### Why not use the root `.github.io` repo for this?

The root GitHub Pages site is tied to the special repo named:

```text
YOUR_USERNAME.github.io
```

That site is better saved for your main public identity. If you use it for one documentation project, you may later need to replace or restructure it when you want a portfolio homepage.

For this workflow guide, a project site is cleaner and less risky.

---

## 3. Recommended Repo Structure

```text
website-building-workflow/
  README.md
  mkdocs.yml

  docs/
    index.md

    workflow/
      01-overview.md
      02-website-types.md
      03-product-planning.md
      04-information-architecture.md
      05-wireframes.md
      06-visual-design.md
      07-frontend.md
      08-backend.md
      09-database.md
      10-testing.md
      11-deployment.md
      12-ai-workflows.md

    checklists/
      launch-checklist.md
      ui-qa-checklist.md
      accessibility-checklist.md
      responsive-checklist.md
      copilot-implementation-checklist.md

    templates/
      product-brief.md
      route-map.md
      screen-spec.md
      component-spec.md
      ai-task-brief.md
      pr-review.md
      debugging-template.md
      feature-spec.md

    assets/
      images/
      diagrams/

  design-source/
    README.md
    exports/
    diagrams/
    references/

  .github/
    workflows/
      deploy.yml
```

---

## 4. What Goes in `docs/`

Use `docs/` for files that should become part of the MkDocs website.

Examples:

```text
docs/index.md
docs/workflow/01-overview.md
docs/checklists/launch-checklist.md
docs/templates/screen-spec.md
docs/assets/images/example-wireframe.png
```

The `docs/` folder should contain polished documentation, not messy drafts or large raw design files.

Good things to include in `docs/`:

- Published Markdown pages
- Checklists
- Templates
- Small screenshots
- Diagrams used in the docs
- Visual examples that support the guide

Avoid putting these directly in `docs/`:

- Large `.fig` files
- Photoshop files
- Krita files
- Random exports
- Raw experiment files
- Huge image archives

---

## 5. What Goes in `design-source/`

Use `design-source/` for raw or supporting design materials that are not necessarily meant to appear directly on the published site.

Example:

```text
design-source/
  README.md
  exports/
    homepage-wireframe-v1.png
    dashboard-layout-v2.png
  diagrams/
    website-flow.drawio
    sitemap.drawio
  references/
    competitor-notes.md
    visual-reference-links.md
```

This keeps the published MkDocs content clean while still allowing the repo to track supporting design material.

If files are large, consider not committing them directly, or use Git LFS if they truly need to be versioned.

---

## 6. Should You Use `docs/v1/`?

Usually, no.

Avoid this for now:

```text
docs/v1/
```

That structure implies formal versioned documentation, such as:

```text
docs/v1/
docs/v2/
docs/v3/
```

That is useful for:

- API docs
- Library docs
- Framework docs
- Public product docs with old versions preserved
- Course/curriculum versions

For this workflow guide, it is probably unnecessary at the beginning.

Use this instead:

```text
docs/workflow/
docs/checklists/
docs/templates/
docs/assets/
```

If you later want formal versions, you can add versioning after the site matures.

---

## 7. Recommended Content Sections

### 7.1 Home Page

File:

```text
docs/index.md
```

Purpose:

- Explain what the guide is
- State who it is for
- Link to the main workflow
- Link to templates and checklists

Suggested content:

```markdown
# Website-Building Workflow

A practical guide for planning, designing, building, testing, deploying, and iterating on websites and web apps.

## Main sections

- Workflow overview
- Website types
- Product planning
- Information architecture
- Wireframes
- Visual design
- Frontend
- Backend
- Database
- Testing
- Deployment
- AI workflows
- Templates
- Checklists
```

---

### 7.2 Workflow Overview

File:

```text
docs/workflow/01-overview.md
```

This should explain the general pipeline:

```text
Goal
→ Research
→ Information architecture
→ Wireframes
→ Visual design
→ Prototype
→ Frontend implementation
→ Backend/CMS implementation
→ Content
→ QA/testing
→ Deployment
→ Analytics/iteration
```

Also include the simplified solo-developer version:

```text
1. Write what the site/app should do.
2. Make a route map.
3. Wireframe the major screens.
4. Turn the best wireframe into a polished design.
5. Write a short screen spec.
6. Use AI planning before coding.
7. Implement one screen/component at a time.
8. Compare output against the design.
9. Fix spacing, states, responsiveness, and accessibility.
10. Deploy.
```

---

### 7.3 Website Types

File:

```text
docs/workflow/02-website-types.md
```

Cover common website/app types:

| Type | Main Workflow |
|---|---|
| Landing page | Copy → wireframe → visual design → static frontend → deploy |
| Portfolio | Content/examples → design → static frontend → deploy |
| Blog/docs | Information architecture → CMS/static generator → content → deploy |
| SaaS app | Product flows → UI design → frontend/backend/database → auth → deploy |
| E-commerce | Catalog → checkout → payments → inventory/orders |
| Dashboard app | Data model → user tasks → components → API integration → states |

Include notes on static vs dynamic sites.

---

### 7.4 Product Planning

File:

```text
docs/workflow/03-product-planning.md
```

Explain that planning should start with user tasks, not visual style.

Recommended questions:

```text
What should users be able to do?
What should users understand quickly?
What is the primary action on each page?
What is the success condition?
What does the site/app not need to do yet?
```

Include a product-task example:

```markdown
# Product Tasks

Users need to:

- Understand what the product does
- Sign up or log in
- Complete the main workflow
- Review results/status
- Configure settings
- Recover from errors
```

---

### 7.5 Information Architecture

File:

```text
docs/workflow/04-information-architecture.md
```

Cover:

- Sitemap
- Route map
- Navigation structure
- User flows
- Page hierarchy

Example route map:

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

---

### 7.6 Wireframes

File:

```text
docs/workflow/05-wireframes.md
```

Explain that wireframes are low-detail layout plans.

They answer:

```text
Where does navigation go?
Where is the main action?
What information appears first?
What can be hidden?
What must always be visible?
```

Recommendation:

Start in grayscale. Avoid colors, gradients, shadows, and detailed branding until the structure works.

---

### 7.7 Visual Design

File:

```text
docs/workflow/06-visual-design.md
```

Cover:

- Typography
- Color
- Spacing
- Icons
- Images
- Shadows
- Borders
- Responsive design
- Hover/focus states
- Empty/loading/error states

Include design system basics:

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

Recommended principle:

```text
Figma defines appearance.
Markdown specs define behavior.
Code implements both.
```

---

### 7.8 Frontend

File:

```text
docs/workflow/07-frontend.md
```

Cover what frontend work includes:

- HTML structure
- CSS/styling
- JavaScript/TypeScript
- React/Vue/Svelte/etc.
- Routing
- Components
- API calls
- Loading states
- Error states
- Responsive layouts
- Accessibility

Example components:

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

---

### 7.9 Backend

File:

```text
docs/workflow/08-backend.md
```

Cover backend responsibilities:

- Authentication
- Users/accounts
- API routes
- Database access
- Permissions
- Email
- Payments
- Background jobs
- Admin tools

Example API routes:

```text
GET /items
POST /items
PATCH /items/{id}
DELETE /items/{id}
POST /auth/login
POST /auth/signup
```

---

### 7.10 Database

File:

```text
docs/workflow/09-database.md
```

Cover:

- Tables/collections
- Relationships
- Migrations
- Seeds/test data
- Backups
- Development vs production databases

Example data model thinking:

```text
Users
Organizations
Projects
Items
Tags
Comments
Settings
Audit logs
```

---

### 7.11 Testing

File:

```text
docs/workflow/10-testing.md
```

Cover:

- Manual QA
- Unit tests
- Component tests
- Integration tests
- End-to-end tests
- Accessibility checks
- Performance checks
- Security checks

Recommended questions:

```text
Does it work?
Does it work on mobile?
Does it work in major browsers?
Are errors handled?
Are loading states handled?
Can it be used with keyboard navigation?
Are forms validated?
Are permissions correct?
```

---

### 7.12 Deployment

File:

```text
docs/workflow/11-deployment.md
```

Cover:

- Static hosting
- Dynamic hosting
- Frontend deployment
- Backend deployment
- Database hosting
- Environment variables
- Domains
- SSL
- Monitoring
- Logs

Static site examples:

```text
GitHub Pages
Netlify
Vercel
Cloudflare Pages
```

Dynamic app examples:

```text
Railway
Render
Fly.io
Vercel serverless
AWS/GCP/Azure
```

---

### 7.13 AI Workflows

File:

```text
docs/workflow/12-ai-workflows.md
```

Cover the better AI-assisted coding workflow:

```text
Idea
→ brief/spec
→ context package
→ plan
→ small implementation
→ test/verify
→ review/refactor
→ commit
```

Contrast weak and strong workflows.

Weak workflow:

```text
Idea
→ vague Copilot prompt
→ many files change
→ eyeball the result
→ keep prompting until it seems okay
```

Better workflow:

```text
Idea
→ task brief
→ constraints
→ acceptance criteria
→ plan
→ small diff
→ tests
→ review
→ commit
```

Recommended AI uses:

| Situation | Best AI Workflow |
|---|---|
| You are confused | Ask/explain mode |
| You need a feature | Spec → plan → edit |
| You need a tiny change | Inline edit |
| You have a bug | Debug hypotheses first |
| You want safer output | Tests first |
| You repeat a task often | Prompt file |
| You want consistent behavior | Repo custom instructions |
| You need implementation | Agent mode with strict acceptance criteria |

---

## 8. Recommended Checklists

### 8.1 Launch Checklist

File:

```text
docs/checklists/launch-checklist.md
```

Include:

```markdown
# Launch Checklist

## Content
- [ ] Homepage copy reviewed
- [ ] Button labels clear
- [ ] Empty states written
- [ ] Error messages written
- [ ] Legal/privacy pages included if needed

## UI
- [ ] Desktop layout checked
- [ ] Tablet layout checked
- [ ] Mobile layout checked
- [ ] Hover states checked
- [ ] Focus states checked
- [ ] Loading states checked
- [ ] Empty states checked
- [ ] Error states checked

## Functionality
- [ ] Main user flow works
- [ ] Forms validate input
- [ ] Auth works, if applicable
- [ ] API calls work
- [ ] Database writes work
- [ ] Permissions checked

## Technical
- [ ] Tests pass
- [ ] Lint passes
- [ ] Typecheck passes
- [ ] Environment variables configured
- [ ] Production database configured
- [ ] Domain configured
- [ ] SSL works

## Post-launch
- [ ] Analytics installed
- [ ] Error monitoring configured
- [ ] Logs accessible
- [ ] Backup plan exists, if needed
```

---

### 8.2 UI QA Checklist

File:

```text
docs/checklists/ui-qa-checklist.md
```

Include:

```markdown
# UI QA Checklist

- [ ] Spacing matches design
- [ ] Font sizes are consistent
- [ ] Line heights are readable
- [ ] Colors use design tokens
- [ ] Border radii are consistent
- [ ] Cards align correctly
- [ ] Navigation state is clear
- [ ] Buttons have hover/focus/disabled states
- [ ] Inputs have error/success states
- [ ] Tables/lists handle long content
- [ ] Layout works on mobile
- [ ] Layout works with empty data
- [ ] Layout works with lots of data
```

---

### 8.3 Accessibility Checklist

File:

```text
docs/checklists/accessibility-checklist.md
```

Include:

```markdown
# Accessibility Checklist

- [ ] Page has semantic landmarks
- [ ] Headings are ordered logically
- [ ] Interactive elements are keyboard accessible
- [ ] Focus states are visible
- [ ] Buttons use button elements
- [ ] Links use anchor elements
- [ ] Form labels are present
- [ ] Error messages are associated with inputs
- [ ] Color contrast is acceptable
- [ ] Images have useful alt text or are marked decorative
- [ ] Modals trap focus when open
- [ ] Page works at 200% zoom
```

---

### 8.4 Copilot Implementation Checklist

File:

```text
docs/checklists/copilot-implementation-checklist.md
```

Include:

```markdown
# Copilot Implementation Checklist

Before asking AI to edit code:

- [ ] Task goal is clear
- [ ] Relevant files are listed
- [ ] Constraints are listed
- [ ] Acceptance criteria are written
- [ ] Design reference is linked, if applicable
- [ ] Existing APIs/data models are known
- [ ] Non-goals are listed

During implementation:

- [ ] Ask for a plan first
- [ ] Keep changes small
- [ ] Avoid unrelated refactors
- [ ] Ask AI to list files before editing
- [ ] Run tests/lint/typecheck

After implementation:

- [ ] Review the diff manually
- [ ] Ask AI for a critical code review
- [ ] Confirm acceptance criteria
- [ ] Commit with a clear message
```

---

## 9. Recommended Templates

### 9.1 Product Brief Template

File:

```text
docs/templates/product-brief.md
```

```markdown
# Product Brief

## Goal
What problem does this site/app solve?

## Audience
Who is it for?

## Primary User Tasks
- Task 1
- Task 2
- Task 3

## Success Criteria
How do we know this is successful?

## Non-goals
What are we intentionally not building yet?

## Risks / Unknowns
- Risk 1
- Risk 2
```

---

### 9.2 Route Map Template

File:

```text
docs/templates/route-map.md
```

```markdown
# Route Map

## Public Routes

```text
/
/pricing
/features
/login
/signup
```

## App Routes

```text
/app
/app/dashboard
/app/items
/app/items/:id
/app/settings
```

## Notes
- Which routes require auth?
- Which routes are public?
- Which routes are admin-only?
```

---

### 9.3 Screen Spec Template

File:

```text
docs/templates/screen-spec.md
```

```markdown
# Screen Spec: [Screen Name]

## Purpose
What is this screen for?

## Primary Actions
- Action 1
- Action 2
- Action 3

## Layout
- Header
- Sidebar
- Main content
- Secondary panel

## Components
- ComponentA
- ComponentB
- ComponentC

## Data Needed
- field_one
- field_two
- field_three

## States
- Loading
- Empty
- Loaded
- Error
- Mobile

## Figma / Design Reference
Add link here.

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Implementation Constraints
- Constraint 1
- Constraint 2
- Constraint 3
```

---

### 9.4 Component Spec Template

File:

```text
docs/templates/component-spec.md
```

```markdown
# Component Spec: [Component Name]

## Purpose
What does this component do?

## Props / Inputs
| Prop | Type | Required | Notes |
|---|---|---:|---|
| example | string | Yes | Description |

## Variants
- Default
- Loading
- Empty
- Error
- Disabled
- Mobile

## Behavior
What happens on click, hover, submit, etc.?

## Accessibility
- Keyboard behavior
- ARIA notes, if needed
- Focus behavior

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2
```

---

### 9.5 AI Task Brief Template

File:

```text
docs/templates/ai-task-brief.md
```

```markdown
# AI Task Brief

## Task
Describe exactly what should be changed.

## Context
Relevant files:
- file/path/example.tsx
- file/path/example.py

Current behavior:
- Explain current behavior.

Desired behavior:
- Explain desired behavior.

## Constraints
- Do not change unrelated files.
- Reuse existing components where possible.
- Do not introduce dependencies without approval.
- Preserve existing public behavior unless explicitly changed.

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Validation
Run:

```bash
npm test
npm run lint
pytest
```
```

---

### 9.6 PR Review Template

File:

```text
docs/templates/pr-review.md
```

```markdown
# PR Review Checklist

Review the diff for:

- [ ] Correctness bugs
- [ ] Edge cases
- [ ] Security issues
- [ ] Unnecessary complexity
- [ ] Missing tests
- [ ] Unclear naming
- [ ] Broken existing behavior
- [ ] Accessibility problems
- [ ] Performance regressions

For each issue, include:

1. File/location
2. Problem
3. Why it matters
4. Suggested fix
```

---

## 10. Recommended `mkdocs.yml`

```yaml
site_name: Website Building Workflow
site_description: A practical workflow for planning, designing, building, testing, and deploying websites.
site_url: https://YOUR_USERNAME.github.io/website-building-workflow/

repo_url: https://github.com/YOUR_USERNAME/website-building-workflow
repo_name: YOUR_USERNAME/website-building-workflow

theme:
  name: material
  features:
    - navigation.sections
    - navigation.indexes
    - navigation.top
    - search.suggest
    - search.highlight
    - content.code.copy

nav:
  - Home: index.md
  - Workflow:
      - Overview: workflow/01-overview.md
      - Website Types: workflow/02-website-types.md
      - Product Planning: workflow/03-product-planning.md
      - Information Architecture: workflow/04-information-architecture.md
      - Wireframes: workflow/05-wireframes.md
      - Visual Design: workflow/06-visual-design.md
      - Frontend: workflow/07-frontend.md
      - Backend: workflow/08-backend.md
      - Database: workflow/09-database.md
      - Testing: workflow/10-testing.md
      - Deployment: workflow/11-deployment.md
      - AI Workflows: workflow/12-ai-workflows.md
  - Checklists:
      - Launch Checklist: checklists/launch-checklist.md
      - UI QA Checklist: checklists/ui-qa-checklist.md
      - Accessibility Checklist: checklists/accessibility-checklist.md
      - Responsive Checklist: checklists/responsive-checklist.md
      - Copilot Implementation Checklist: checklists/copilot-implementation-checklist.md
  - Templates:
      - Product Brief: templates/product-brief.md
      - Route Map: templates/route-map.md
      - Screen Spec: templates/screen-spec.md
      - Component Spec: templates/component-spec.md
      - AI Task Brief: templates/ai-task-brief.md
      - PR Review: templates/pr-review.md
      - Debugging Template: templates/debugging-template.md
      - Feature Spec: templates/feature-spec.md
```

---

## 11. Recommended GitHub Actions Deployment

Use GitHub Actions rather than manual deployment once the repo is stable.

Suggested workflow:

```text
Push to main
→ GitHub Actions installs dependencies
→ MkDocs builds the site
→ GitHub Pages publishes the output
```

Example file:

```text
.github/workflows/deploy.yml
```

```yaml
name: Deploy MkDocs Site

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.12'

      - name: Install dependencies
        run: |
          pip install mkdocs mkdocs-material

      - name: Build site
        run: mkdocs build --strict

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: site

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

---

## 12. Recommended AI Workflow for Maintaining This Repo

Use AI to help write and maintain the docs, but do not let it create a sprawling mess.

Recommended workflow:

```text
Idea
→ short outline
→ Markdown page draft
→ review for clarity and usefulness
→ add checklist/template if reusable
→ commit
```

For coding or repo changes:

```text
Task brief
→ plan
→ small change
→ build locally
→ review diff
→ commit
```

Good AI prompt:

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

Bad AI prompt:

```text
Make my docs better.
```

---

## 13. Recommended First Build Order

Do not try to fill the entire site at once.

Build in this order:

```text
1. README.md
2. mkdocs.yml
3. docs/index.md
4. docs/workflow/01-overview.md
5. docs/workflow/02-website-types.md
6. docs/workflow/12-ai-workflows.md
7. docs/templates/ai-task-brief.md
8. docs/templates/screen-spec.md
9. docs/checklists/launch-checklist.md
10. GitHub Actions deployment
```

Then expand the rest gradually.

---

## 14. Recommended Philosophy

The repo should not become a graveyard of notes.

It should answer:

```text
What do I do next when building a website?
What should I think about before designing?
What should I give AI before asking it to code?
How do I check if the result is good?
What templates can I reuse?
What checklists prevent mistakes?
```

Keep the site practical, not academic.

A good page should usually include:

- Short explanation
- Practical workflow
- Example
- Checklist or template
- Common mistakes

---

## 15. Final Recommended Setup

Use this structure:

```text
website-building-workflow/
  README.md
  mkdocs.yml
  docs/
    index.md
    workflow/
    checklists/
    templates/
    assets/
  design-source/
  .github/workflows/deploy.yml
```

Use this publishing strategy:

```text
Project site:
https://YOUR_USERNAME.github.io/website-building-workflow/
```

Keep this for later:

```text
Root site:
https://YOUR_USERNAME.github.io/
```

Use `docs/` for published MkDocs content.
Use `design-source/` for raw design/supporting files.
Avoid `docs/v1/` unless formal documentation versioning becomes necessary.
