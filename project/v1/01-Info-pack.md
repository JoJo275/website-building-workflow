# Info Pack: Website Building Workflow

A typical website is built through these stages:

1. Goal
2. Research
3. Information architecture
4. Wireframes
5. Visual design
6. Prototype
7. Frontend implementation
8. Backend/CMS implementation
9. Content
10. QA/testing
11. Deployment
12. Analytics/iteration

But the exact workflow depends on the type of website.

## 1. Define the goal

Before design or code, clarify what the site is supposed to do.

Examples:

**Marketing site:**
Get visitors to understand the product and sign up.

**Portfolio:**
Show credibility and examples of work.

**SaaS app:**
Let users sign up, log in, and complete workflows.

**E-commerce:**
Help users browse, compare, buy, and manage orders.

**Blog/content site:**
Publish searchable, readable articles.

This step determines everything else.

A bad starting point is:

> “What should it look like?”

A better starting point is:

> “What should users be able to do, and what should they understand?”
## 2. Research and references

People usually gather:

- competitor websites
- design references
- target audience notes
- product requirements
- brand examples
- content examples

For example, if building a SaaS dashboard, you might study Linear, Stripe, PostHog, Vercel, Plain, Intercom, and similar products.

This is not for copying. It is for understanding patterns users already recognize.

## 3. Information architecture

This means deciding what pages/sections exist and how they connect.

Example:

```text
Home
Pricing
Features
Docs
Login
Sign up

App
  Dashboard
  Inbox
  Analytics
  Settings
```

This is where you create:

- sitemap
- route map
- navigation structure
- page hierarchy
- user flows

For a web app, this is especially important because users are not just reading. They are doing tasks.

## 4. Wireframes

Wireframes are low-detail layouts.

They answer:

- Where does the nav go?
- Where is the main action?
- What information appears first?
- How many sections are on the page?
- What is hidden vs visible?

Wireframes should usually be grayscale and boring.

Example:

```text
[Sidebar] [Header]
          [Metric cards]
          [Main content table]
          [Right detail panel]
```

This avoids wasting time polishing a layout that is structurally wrong.

## 5. Visual design

After the wireframe works, designers add:

- typography
- colors
- spacing
- icons
- images
- shadows
- borders
- states
- responsive layouts
- brand style

This is where Figma is commonly used.

For a real product, you usually also define a small design system:

- Colors
- Font sizes
- Spacing scale
- Border radius
- Buttons
- Inputs
- Cards
- Badges
- Modals
- Tables
- Nav items

This matters because otherwise every screen becomes slightly inconsistent.

## 6. Prototype

A prototype shows how screens connect.

Example:

```text
Click "Sign up"        → signup page
Click "View feedback"  → feedback detail panel opens
Click "Filter"         → dropdown opens
Click "Mark resolved"  → status changes
```

This can be done in Figma before writing code.

The prototype does not need real backend logic. It is mainly to test whether the flow makes sense.

## 7. Frontend implementation

Frontend is what users see and interact with.

Common frontend technologies:

- HTML
- CSS
- JavaScript
- TypeScript
- React
- Vue
- Svelte
- Next.js
- Tailwind

Frontend work includes:

- page layout
- components
- buttons/forms
- routing
- responsive behavior
- client-side state
- API calls
- loading/error/empty states
- accessibility
- animations/interactions

Example frontend components:

- Navbar
- Sidebar
- Button
- Input
- Card
- Table
- Modal
- Dropdown
- FeedbackCard
- DashboardMetric

For your kind of app, this is where React components would be built.

## 8. Backend implementation

Backend handles server-side logic.

Common backend responsibilities:

- user accounts
- authentication
- database access
- API endpoints
- permissions
- file uploads
- email sending
- payments
- admin tools
- background jobs

Common backend technologies:

- FastAPI
- Django
- Flask
- Express
- Rails
- Laravel
- Spring
- ASP.NET

For your app, FastAPI would expose routes like:

```text
GET  /feedback
POST /feedback
PATCH /feedback/{id}
GET  /analytics/summary
POST /auth/login
POST /auth/signup
```

The frontend calls these routes and displays the results.

## 9. Database

Dynamic websites usually need a database.

Examples:

- Users
- Feedback items
- Tags
- Organizations
- Comments
- Settings
- Billing records

Common databases:

- PostgreSQL
- MySQL
- SQLite
- MongoDB
- Redis

For a serious SaaS app, PostgreSQL is usually the safer default than SQLite.

## 10. Content

This is often underestimated.

Content includes:

- homepage copy
- button labels
- empty-state messages
- error messages
- onboarding text
- documentation
- pricing descriptions
- emails
- legal pages
- tooltips

A polished website is not just layout. The words matter a lot.

Bad:

> Submit

Better, depending on context:

- Send feedback
- Create project
- Invite teammate
- Mark as resolved

## 11. QA/testing

Before launch, you check:

- Does it work?
- Does it work on mobile?
- Does it work in Chrome/Firefox/Safari?
- Are errors handled?
- Are loading states handled?
- Is it accessible with keyboard?
- Are forms validated?
- Is it fast enough?
- Does auth work correctly?
- Are permissions correct?

Common testing types:

- Manual QA
- Unit tests
- Component tests
- Integration tests
- End-to-end tests
- Accessibility checks
- Performance checks
- Security checks

For a solo dev, you do not need enterprise-level QA at first, but you do need a checklist.

## 12. Deployment

Deployment means putting the site/app online.

**Static site** — frontend only, no server needed. Host on GitHub Pages, Netlify, Vercel, or Cloudflare Pages.

Good for:

- portfolio
- landing page
- docs
- blog
- simple marketing site

**Dynamic web app** — frontend + backend + database. Needs server/runtime/database hosting.

Good for:

- SaaS apps
- dashboards
- accounts
- payments
- user-generated data
- admin panels

Your feedback triage app is dynamic.

## 13. Monitoring and analytics

After launch, people add:

- error tracking
- uptime checks
- analytics
- performance monitoring
- user feedback tools
- logs

Examples of questions this answers:

- Are users signing up?
- Where do they drop off?
- Which pages are slow?
- What errors are happening?
- Are API requests failing?

## The common professional workflow

1. Product brief
2. User flows
3. Sitemap
4. Wireframes
5. Visual design
6. Prototype
7. Design review
8. Frontend build
9. Backend build
10. Content pass
11. QA pass
12. Launch
13. Measure and iterate

## The solo-developer version

1. Write what the site/app should do.
2. Make a route map.
3. Wireframe the major screens in Figma.
4. Turn the best wireframe into a polished Figma design.
5. Write a short markdown spec for each screen.
6. Use `/plan` before asking Copilot/Opus to code.
7. Implement one screen/component at a time.
8. Compare code output against Figma.
9. Fix spacing/states/responsiveness.
10. Deploy.

## Website types and workflows

| Type | Main workflow |
|------|---------------|
| Landing page | Copy → wireframe → visual design → static frontend → deploy |
| Portfolio | Content/examples → design → static frontend → deploy |
| Blog/docs | Information architecture → CMS/static generator → content → deploy |
| SaaS app | Product flows → UI design → frontend/backend/database → auth → deploy |
| E-commerce | Product catalog → checkout flow → payments → inventory/order system |
| Dashboard app | Data model → user tasks → UI components → API integration → state handling |

Your app is closest to: **SaaS dashboard app**

So you need more planning than a normal marketing site.

## Important distinction

A website has three different "truths":

**Design truth:** What should it look like? Usually Figma.

**Behavior truth:** What should happen when users interact? Usually markdown specs, user stories, or tickets.

**Code truth:** How is it actually implemented? Usually repo files, components, tests, API routes.

A lot of your friction with Copilot probably comes from giving it only the design truth.

A mockup says:

> This is what it should look like.

But Copilot also needs:

- What components exist?
- What data powers this?
- What states are required?
- What routes should this live under?
- What files should change?
- What should not change?

## Best mental model

Do not think of website creation as:

> Make design → convert to code

Think of it as:

```text
Define user tasks
→ design screens that support those tasks
→ define components/states/data
→ implement in code
→ test against the intended behavior
```

## Practical next step

For your app, create this order:

- `docs/ui/01-product-tasks.md`
- `docs/ui/02-route-map.md`
- `docs/ui/03-component-inventory.md`
- `docs/ui/04-dashboard-screen.md`
- `docs/ui/05-feedback-inbox-screen.md`
- `docs/ui/06-interaction-states.md`

Then build the matching Figma screens.

That gives Copilot a much better target than a screenshot alone.
