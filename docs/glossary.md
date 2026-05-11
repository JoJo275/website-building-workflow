# Glossary

Definitions for terms used throughout these docs. Each entry is written for someone who has heard the word but isn't sure exactly what it means.

---

## A

### Acceptance criteria

A written list of conditions a feature must meet before it is considered done. Good acceptance criteria are specific, testable, and agreed on before implementation starts — not discovered during code review. Used heavily in [AI Workflows](workflow/12-ai-workflows.md).

### Accessibility

The practice of building websites and apps that can be used by people with disabilities — including visual, motor, cognitive, and hearing differences. In web development this means keyboard navigation, screen reader support, sufficient colour contrast, and correct use of HTML semantics. Abbreviated as **a11y** (a, 11 letters, y). See [Accessibility Checklist](checklists/accessibility-checklist.md) and [Semantic HTML](conventions/html.md).

### API

**Application Programming Interface.** A defined contract for how one piece of software talks to another. In web development, usually means an HTTP API: a server that accepts requests at specific URLs and returns data (typically JSON). Your frontend calls your backend via an API; your backend calls payment or email services via their APIs. See [Backend](workflow/08-backend.md).

### ARIA

**Accessible Rich Internet Applications.** A set of HTML attributes (`role`, `aria-label`, `aria-expanded`, etc.) that add semantic meaning to elements when native HTML elements are not sufficient. Use sparingly — the correct HTML element is almost always better than adding ARIA to a `<div>`. See [Semantic HTML](conventions/html.md).

### Authentication

Verifying **who** a user is — login, password, magic link, OAuth. Separate from [authorisation](#authorisation). Common patterns: session cookies, JWTs, third-party services like Clerk or Auth0. See [Backend](workflow/08-backend.md) and [Third-Party Services](tools/third-party.md).

### Authorisation

Determining **what** an authenticated user is allowed to do. A user can be authenticated (logged in) but not authorised to access an admin route. Usually implemented as role checks or attribute-based policies. See [Backend](workflow/08-backend.md).

---

## B

### Background job

Work that should not happen inside a web request because it is slow, unreliable, or should run on a schedule. Examples: sending emails after signup, processing uploaded images, generating reports. Typically queued and run by a worker process. See [Backend](workflow/08-backend.md).

### bcrypt

A password hashing function designed to be intentionally slow, making brute-force attacks expensive. Always hash passwords before storing them; never store plain text. Also compare argon2, which is newer. See [Backend](workflow/08-backend.md).

### Box model

The CSS model that describes how every HTML element occupies space: content area + padding + border + margin. With `box-sizing: border-box` (recommended), padding and border are included in the declared width, making layout predictable. Without it, adding padding to a `200px` element makes it wider than `200px`. See [CSS Architecture](conventions/css.md).

### Breakpoint

A viewport width at which a CSS layout changes. Defined with `@media (min-width: …)`. Typically named sm / md / lg / xl. Mobile-first means the base styles target the smallest screen and breakpoints add complexity as the viewport grows. See [CSS Architecture](conventions/css.md).

### Bundler

A build tool that takes many JavaScript (or TypeScript) source files, resolves their imports, and outputs one or a few optimised files for the browser. Common bundlers: Vite, esbuild, webpack, Rollup. Most modern frameworks include a bundler so you rarely configure one directly. See [Frontend Tools](tools/frontend.md).

---

## C

### Cascade

The algorithm CSS uses to decide which rule wins when multiple rules target the same element. Priority order: `!important` → inline styles → specificity → source order. Understanding the cascade prevents the most common "why isn't my style applying?" bugs. See [CSS Architecture](conventions/css.md).

### CDN

**Content Delivery Network.** A network of servers distributed around the world that caches and delivers static assets (HTML, CSS, JS, images) from a server physically close to the visitor. Reduces latency, improves load times, and absorbs traffic spikes. Static hosting platforms (Vercel, Netlify, Cloudflare Pages) are essentially CDNs with a deploy pipeline attached. See [Website Types](workflow/02-website-types.md) and [Deployment](workflow/11-deployment.md).

### CI/CD

**Continuous Integration / Continuous Deployment.** An automated pipeline that runs on every code push: tests pass, code is linted, the build succeeds, and the result is deployed. Catches mistakes before they reach production and eliminates manual deploy steps. GitHub Actions is the standard tool for GitHub-hosted repos. See [Deployment](workflow/11-deployment.md) and [Dev Environment Tools](tools/dev-environment.md).

### CMS

**Content Management System.** Software that lets non-developers create, edit, and publish content without touching code. Examples: WordPress, Contentful, Sanity, Ghost. For developer-built sites, a "headless CMS" delivers content via an API which the frontend renders. A static-site generator like Astro can treat markdown files as a lightweight CMS.

### Component

A reusable, self-contained piece of UI — a button, a card, a modal, a form field. Components encapsulate their HTML, CSS, and sometimes logic. The core building block of frontend frameworks like React, Vue, and Svelte. See [Frontend](workflow/07-frontend.md) and [Component Spec](starters/component-spec.md).

### Connection pooling

Reusing a fixed set of open database connections instead of opening and closing a new connection for every request. Opening a database connection is expensive; pooling amortises that cost. ORMs and database clients usually handle this automatically. See [Database](workflow/09-database.md).

### Core Web Vitals

Google's set of user-experience metrics that measure real-world loading performance and interactivity: **LCP** (Largest Contentful Paint — how fast the main content loads), **INP** (Interaction to Next Paint — responsiveness), and **CLS** (Cumulative Layout Shift — visual stability). Audited by Lighthouse and Chrome DevTools. See [Testing](workflow/10-testing.md).

### CSS custom property

A variable defined in CSS with a `--` prefix: `--color-primary: #0d9488`. Referenced with `var(--color-primary)`. The CSS implementation of [design tokens](#design-token). Defined on `:root` so they are available globally; overridden in scoped selectors for themes and components. See [CSS Architecture](conventions/css.md) and [Design Tokens](design/design-tokens.md).

### CSS Grid

A two-dimensional CSS layout system for placing elements in rows and columns simultaneously. Best for page-level layout and anything that needs rows and columns to align. Complementary to [Flexbox](#flexbox), which handles one dimension at a time. See [CSS Architecture](conventions/css.md).

### CSS Modules

A CSS file format where class names are automatically scoped to the component that imports them, preventing naming collisions. Built into Next.js, Vite, and most modern build tools. See [Frontend Tools](tools/frontend.md).

### CSS-in-JS

An approach where CSS is written inside JavaScript files, co-located with components. Examples: Styled Components, Emotion. Allows dynamic styles based on props. Has runtime overhead and is less common in newer projects, which tend to prefer Tailwind or CSS Modules. See [Frontend Tools](tools/frontend.md).

---

## D

### Design brief

A short written description of what a product should feel like — tone, personality, target user, and visual direction — written before touching any design tool. Gives every subsequent visual decision a reference point. See [Visual Design](workflow/06-visual-design.md) and [Visual Style](design/visual-style.md).

### Design system

A shared set of components, patterns, and guidelines that ensures visual and behavioural consistency across a product. Includes design tokens, a component library, and usage guidelines. See [CSS Architecture](conventions/css.md) and [Example Design System](conventions/example-system.md).

### Design token

A named value for a visual decision — a colour, a spacing size, a border radius, a motion duration. Tokens are defined once and referenced everywhere, so changing a value in one place updates the whole product. Implemented as [CSS custom properties](#css-custom-property). See [Design Tokens](design/design-tokens.md) and [Visual Design](workflow/06-visual-design.md).

### Diff

A view of exactly what changed in a file between two versions — lines added (green) and lines removed (red). In version control, you review a diff before merging a pull request. In AI workflows, keeping diffs small and focused makes review faster and mistakes easier to spot. See [AI Workflows](workflow/12-ai-workflows.md).

### DNS

**Domain Name System.** The internet's phonebook — translates human-readable domain names (`example.com`) into IP addresses that servers understand. When you buy a domain and point it at a host, you're creating DNS records (A records, CNAMEs). Propagation can take minutes to hours after changes. See [Deployment](workflow/11-deployment.md).

### Document database

A database that stores data as flexible, JSON-like documents rather than rows in tables. Examples: MongoDB, Firestore. Good for unstructured or highly variable data where a rigid schema is a poor fit. Contrasts with a [relational database](#relational-database). See [Database](workflow/09-database.md).

### DOM

**Document Object Model.** The browser's in-memory tree representation of an HTML page. JavaScript reads and modifies the DOM to make pages interactive — adding classes, changing text, showing and hiding elements. Frameworks like React manage DOM updates for you via a virtual DOM.

### Dynamic site

A site that generates pages on the server or client per request, rather than serving pre-built files. Necessary when pages depend on user-specific data, authentication state, or real-time information. Requires a running server or serverless functions. Contrasts with a [static site](#static-site). See [Website Types](workflow/02-website-types.md).

---

## E

### Empty state

The UI shown when a list or page has no content yet — typically an icon, a heading, a short explanation, and a primary action. Empty states set expectations and guide users to their first action. A missing empty state makes the app feel broken. See [Copy & Voice](design/copy-voice.md).

### End-to-end test

A test that drives a real browser through a complete user flow — sign up, log in, perform an action, log out — verifying the whole stack works together. Slow to run but catches integration bugs that unit tests miss. Playwright is the standard tool. See [Testing](workflow/10-testing.md).

### Environment variable

A named value stored outside the codebase and injected at runtime — database connection strings, API keys, secrets. Never hardcode secrets in source files. Different values are used in development, test, and production environments. Also called env vars. See [Backend](workflow/08-backend.md) and [Deployment](workflow/11-deployment.md).

### Error state

The UI shown when an operation fails — a form submission error, a failed API call, a network timeout. Every user-facing action needs a defined error state. Pair with [loading state](#loading-state) and [empty state](#empty-state). See [Frontend](workflow/07-frontend.md).

### Error tracking

A service that captures, logs, and surfaces runtime errors from production — with full stack traces and request context. Sentry is the standard tool. Essential for knowing what breaks after deployment without waiting for user reports. See [Deployment](workflow/11-deployment.md).

---

## F

### Feature spec

A written description of a feature before it is built — what problem it solves, user flows, edge cases, and acceptance criteria. Reduces guesswork during implementation and makes AI-assisted coding far more effective. See [Feature Spec](starters/feature-spec.md) and [AI Task Brief](starters/ai-task-brief.md).

### Flexbox

A one-dimensional CSS layout model for aligning items in a row or column. Best for navigation bars, button groups, centering content, and distributing space between items in a single direction. Complementary to [CSS Grid](#css-grid), which handles two dimensions. See [CSS Architecture](conventions/css.md).

### Focus ring

The visible outline that appears on an interactive element (button, link, input) when it receives keyboard focus. Required for accessibility — keyboard users rely on it to know where they are on the page. Customise with `:focus-visible`, never remove entirely. See [Semantic HTML](conventions/html.md) and [Accessibility Checklist](checklists/accessibility-checklist.md).

### Foreign key

A column in a database table that references the primary key of another table, establishing a relationship between them. For example, a `comments` table might have a `post_id` foreign key pointing to the `posts` table. Enforces referential integrity — you cannot create a comment for a post that doesn't exist. See [Database](workflow/09-database.md).

### Framework

A pre-built structure for a specific type of software that handles common concerns (routing, rendering, state) so you can focus on application-specific logic. Frameworks are opinionated; libraries are not. React is a library; Next.js (which wraps React) is a framework. See [Frontend Tools](tools/frontend.md) and [Backend](workflow/08-backend.md).

---

## G

### Git

The standard distributed version control system. Tracks every change to every file, allowing you to revert, branch, and collaborate without overwriting each other's work. All web development workflows depend on it. See [Dev Environment Tools](tools/dev-environment.md) and [Version control](#version-control).

---

## H

### HTTPS

**HyperText Transfer Protocol Secure.** The encrypted version of HTTP, using TLS. Protects data in transit between browser and server. Required for all production sites — browsers mark HTTP-only sites as insecure, and many browser APIs (geolocation, service workers) refuse to work without it. Most hosting providers enable it automatically. See [Deployment](workflow/11-deployment.md).

### Hydration

The process where a server-rendered HTML page is taken over by JavaScript in the browser — event listeners are attached and the framework's state becomes active. A page can be visible (from server HTML) before hydration completes, making it feel faster. Partial hydration (Astro's "islands") only hydrates the interactive parts. See [Frontend Tools](tools/frontend.md).

---

## I

### Index

A database structure that speeds up queries on a particular column by maintaining a sorted copy of that data. Without an index, a query filters every row; with one, it jumps directly to the matching rows. Add indexes for columns used in `WHERE`, `JOIN`, and `ORDER BY` clauses. Too many indexes slow down writes. See [Database](workflow/09-database.md).

### Information architecture

The structural design of a site — how content is organised, labelled, and navigated. Includes the sitemap, navigation structure, and URL hierarchy. Defined before wireframes. Good IA makes a site self-explanatory; poor IA means users can't find what they came for. See [Information Architecture](workflow/04-information-architecture.md).

### Integration test

A test that verifies multiple parts of the system work correctly together — a database query plus the function that calls it, or an API route plus the auth middleware protecting it. Slower than unit tests but faster and more realistic than end-to-end tests. See [Testing](workflow/10-testing.md).

---

## J

### JWT

**JSON Web Token.** A compact, URL-safe token that encodes a payload (user ID, roles, expiry) and a cryptographic signature. Used for stateless authentication — the server signs the token on login; the client sends it with every request; the server verifies the signature without a database lookup. Compare with [session](#session)-based auth. See [Authentication](#authentication).

---

## L

### Linter

A tool that statically analyses code for errors, style violations, and potential bugs without running it. ESLint for JavaScript/TypeScript, markdownlint for Markdown, Stylelint for CSS. Catches mistakes at save time rather than at runtime. See [Dev Environment Tools](tools/dev-environment.md).

### Loading state

The UI shown while an async operation is in progress — a spinner, a skeleton screen, or a progress indicator. Every asynchronous action needs one. Without a loading state, users don't know whether the app is working or frozen. Pair with [error state](#error-state) and [empty state](#empty-state). See [Frontend](workflow/07-frontend.md).

### localStorage

A browser API that persists key/value data between page loads for a given origin. Unlike cookies, localStorage data is never sent to the server automatically. Used for theme preferences, UI state, and draft content. Limited to ~5MB and synchronous — do not use for large data or sensitive information.

---

## M

### Media query

A CSS rule that applies styles only when certain conditions are met — typically screen width. The foundation of [responsive design](#responsive-design). Mobile-first: write base styles for small screens, then use `@media (min-width: …)` to add styles for larger ones. See [CSS Architecture](conventions/css.md).

### Meta-framework

A framework built on top of another framework that adds routing, server-side rendering, static generation, and deployment conventions. Next.js is a meta-framework for React; SvelteKit is one for Svelte; Nuxt is one for Vue. Handles the build pipeline and deployment targets so you can focus on application code. See [Frontend Tools](tools/frontend.md).

### Middleware

Code that runs between a request arriving at a server and the route handler processing it. Common uses: authentication checks, request logging, input parsing, rate limiting, CORS headers. See [Backend](workflow/08-backend.md).

### Migration

A versioned, code-controlled change to a database schema — adding a column, creating a table, renaming a field. Migrations are checked into version control and run in sequence, so every environment (local, staging, production) can reach the same schema state. Never change a production schema by hand. See [Database](workflow/09-database.md).

---

## O

### ORM

**Object-Relational Mapper.** A library that lets you interact with a relational database using your programming language's objects rather than raw SQL. It translates method calls into queries and query results into objects. Examples: Prisma, Drizzle (TypeScript), SQLAlchemy (Python), ActiveRecord (Ruby). See [Database](workflow/09-database.md).

---

## P

### Package manager

A tool that installs, updates, and manages the third-party libraries (packages) a project depends on. For JavaScript: npm, pnpm, Bun. For Python: pip, uv. Manages a lock file that pins exact dependency versions so every developer and CI run uses the same code. See [Dev Environment Tools](tools/dev-environment.md).

### Parameterised query

A database query where user input is passed as a separate parameter rather than interpolated directly into the SQL string. Prevents SQL injection — the database treats the parameter as data, never as executable SQL. This is the correct way to handle all user input in database queries. See [Backend](workflow/08-backend.md).

### Product brief

A short document that defines what a product is, who it is for, what problems it solves, and what success looks like. Written before any design or code. See [Product Brief Template](starters/product-brief.md) and [Product Planning](workflow/03-product-planning.md).

### Progressive enhancement

A design philosophy that starts with a functional baseline (semantic HTML, no JavaScript) and adds layers of enhancement (CSS, JavaScript) on top. Pages remain functional for users on slow connections or with JavaScript disabled. Contrasts with building JavaScript-first and hoping it loads.

### Prototype

An interactive mockup — higher fidelity than wireframes, lower fidelity than final code — used to validate user flows before full implementation. Built in design tools (Figma) or as throwaway HTML/CSS. See [Workflow Overview](workflow/01-overview.md).

### Pull request

A formal proposal to merge a branch of code changes into another branch (usually `main`). The standard unit of code review. Includes a diff of all changes, a description, and a place for reviewers to leave comments. Also called a PR or merge request. See [Dev Environment Tools](tools/dev-environment.md).

---

## Q

### Query

A request to a database for data matching certain conditions. Written in SQL (`SELECT * FROM users WHERE active = true`) or via an [ORM](#orm)'s method interface. Performance-sensitive: queries without [indexes](#index) on large tables can be very slow.

---

## R

### Rate limiting

Restricting how many requests a client can make to a server in a given time window, to prevent abuse and denial-of-service attacks. Authentication endpoints are especially important to rate-limit — without it, an attacker can try millions of passwords. See [Backend](workflow/08-backend.md).

### Refactor

Restructuring existing code without changing its external behaviour. The goal is to make the code easier to read, test, or extend — not to add features. Refactoring with no tests to confirm behaviour is preserved is risky. See [AI Workflows](workflow/12-ai-workflows.md).

### Relational database

A database that organises data into tables (rows and columns) with explicit relationships between them, enforced by [foreign keys](#foreign-key). The dominant paradigm for structured data. SQL is the query language. Examples: PostgreSQL, MySQL, SQLite. Contrasts with a [document database](#document-database). See [Database](workflow/09-database.md).

### rem

A relative CSS unit equal to the font size of the root element (`<html>`). If the root font size is `16px`, then `1rem = 16px`. Scaling: `0.875rem = 14px`, `1.25rem = 20px`. Using `rem` for font sizes and spacing means user browser preferences are respected — users who set their browser to larger fonts get them. See [CSS Architecture](conventions/css.md).

### Repository

A directory under version control that contains a project's source code, configuration, and history. Hosted on GitHub, GitLab, or similar. Often shortened to **repo**. See [Dev Environment Tools](tools/dev-environment.md).

### Responsive design

A CSS approach where layouts adapt to the viewport size using [breakpoints](#breakpoint) and fluid units (`%`, `rem`, `fr`). Mobile-first: start with the smallest layout and layer in complexity as the screen grows. See [CSS Architecture](conventions/css.md) and [Responsive Checklist](checklists/responsive-checklist.md).

### REST

**Representational State Transfer.** A convention for designing HTTP APIs where resources (users, posts, orders) are addressed by URLs and manipulated with standard HTTP methods: `GET` (read), `POST` (create), `PUT`/`PATCH` (update), `DELETE` (remove). Most web APIs are REST or REST-like. See [Backend](workflow/08-backend.md).

### Rollback

Reverting a deployment to the previous working version after a bad deploy. Good hosting platforms support one-click rollbacks. The ability to roll back quickly is why keeping deploys small and frequent is safer than infrequent large ones. See [Deployment](workflow/11-deployment.md).

### Route map

A list of all the URLs in a site or app with their purposes, component or template names, and auth requirements. Written before implementation so you know what you're building. See [Route Map Template](starters/route-map.md) and [Information Architecture](workflow/04-information-architecture.md).

### Routing

The mechanism that maps a URL to a specific page, component, or handler. In frontend frameworks: file-based routing (Next.js, SvelteKit) maps file paths to URLs. In backend frameworks: route handlers are registered explicitly with the URL pattern and HTTP method they handle. See [Frontend](workflow/07-frontend.md) and [Backend](workflow/08-backend.md).

---

## S

### Sanitisation

Cleaning or stripping user input before processing it to remove dangerous content — HTML tags that could cause XSS, path traversal sequences, or other malicious payloads. Sanitisation is about making input safe; [validation](#validation) is about checking it meets expected constraints. Both are needed. See [Backend](workflow/08-backend.md).

### Schema

The definition of a database's structure — what tables exist, what columns they have, their data types, constraints, and relationships. The schema is declared in migration files and should be under version control. See [Database](workflow/09-database.md).

### Screen spec

A detailed written description of a single page or screen — its purpose, layout zones, components, states (loading, empty, error), and copy. Bridges the gap between wireframes and implementation. See [Screen Spec Template](starters/screen-spec.md).

### Seed data

A set of known, consistent sample records inserted into a database for local development and testing. Makes it possible to open the app locally and see realistic content without manually creating data. Checked into version control alongside migrations. See [Database](workflow/09-database.md).

### Semantic HTML

Using HTML elements according to their meaning, not their appearance. `<button>` for actions, `<a>` for navigation, `<h1>`–`<h6>` for heading hierarchy, `<nav>` for navigation landmarks. Semantic markup is accessible by default, more maintainable, and better for SEO. See [Semantic HTML](conventions/html.md).

### Serverless

A hosting model where server-side code runs in short-lived functions (often called "lambdas" or "edge functions") on-demand, rather than on a permanently running server. You pay per invocation, and the platform handles scaling. Good for intermittent workloads; less ideal for long-running processes or WebSockets. See [Website Types](workflow/02-website-types.md) and [Deployment](workflow/11-deployment.md).

### Session

A server-side record that tracks an authenticated user's state between requests. On login, the server creates a session, stores it in a database or cache, and gives the client a session ID (usually in a cookie). On each subsequent request, the server looks up the session to confirm the user is still authenticated. Compare with [JWT](#jwt)-based stateless auth. See [Backend](workflow/08-backend.md).

### Sitemap

A structured list of all the pages in a site, showing the hierarchy and relationships between them. Useful for planning navigation and information architecture before wireframing. Also refers to the `sitemap.xml` file that tells search engines what pages exist. See [Information Architecture](workflow/04-information-architecture.md).

### Skip link

A visually hidden link at the very top of a page that becomes visible on focus and jumps to the main content (`#main`). Keyboard users use it to skip past the navigation on every page. Required for accessibility. See [Semantic HTML](conventions/html.md) and [Accessibility Checklist](checklists/accessibility-checklist.md).

### Slug

A URL-safe string derived from a title or name — lowercase, hyphens instead of spaces, special characters removed. `/blog/how-to-build-a-design-system` is a slug. Used in routes and as human-readable identifiers. Usually stored as a unique column in the database. See [Route Map](starters/route-map.md).

### Soft delete

Marking a record as deleted (with a `deleted_at` timestamp) instead of removing it from the database. The record is excluded from normal queries but remains recoverable. Preferred over hard deletes for most user-facing data. See [Database](workflow/09-database.md).

### Specificity

The CSS mechanism that determines which rule wins when multiple rules target the same element and property. Calculated from the selector: inline styles beat IDs beat classes beat elements. High specificity leads to brittle, hard-to-override CSS. The best architecture minimises it — one class, no nesting. See [CSS Architecture](conventions/css.md) and [Design Tokens](design/design-tokens.md).

### SQL

**Structured Query Language.** The standard language for interacting with [relational databases](#relational-database). Used to create tables, insert data, and query records. Even when using an [ORM](#orm), understanding SQL helps when queries are slow or results are unexpected. See [Database](workflow/09-database.md).

### SSG

**Static Site Generation.** A build-time rendering strategy where HTML pages are generated once at build time and served as static files. No server required at runtime. Fast, cheap to host, and highly cacheable. Best for content that does not change per user or per request. Examples: Astro, Next.js (`generateStaticParams`). See [Frontend Tools](tools/frontend.md) and [Website Types](workflow/02-website-types.md).

### SSR

**Server-Side Rendering.** A rendering strategy where the server generates HTML for each request and sends it to the browser, rather than sending a mostly-empty page and rendering in JavaScript. Gives faster initial load and better SEO. Can be combined with client-side hydration. See [Frontend Tools](tools/frontend.md) and [Website Types](workflow/02-website-types.md).

### Static site

A site whose pages are pre-built HTML files served directly without server-side processing per request. Faster, cheaper to host, and simpler to deploy than [dynamic sites](#dynamic-site). A [CDN](#cdn) serves the files from a location close to the visitor. See [Website Types](workflow/02-website-types.md) and [Deployment](workflow/11-deployment.md).

---

## T

### TypeScript

A typed superset of JavaScript that adds static type annotations. The compiler catches type errors at edit time rather than at runtime. Now the default for most serious JavaScript projects. Type errors do not prevent the code from running in most frameworks — they are warnings, not hard failures. See [Frontend Tools](tools/frontend.md).

---

## U

### Unit test

A test that verifies one function or module in isolation, with all dependencies replaced by test doubles (mocks/stubs). Fast to run, easy to write for pure functions, but tests only a small unit — integration bugs are invisible. See [Testing](workflow/10-testing.md).

### Utility-first CSS

A CSS methodology where styles are applied by composing small, single-purpose utility classes directly in HTML, rather than writing custom CSS rules. Tailwind CSS is the dominant utility-first framework. Keeps styles co-located with markup and eliminates naming problems, but can make HTML verbose. See [Frontend Tools](tools/frontend.md) and [CSS Architecture](conventions/css.md).

---

## V

### Validation

Checking that input conforms to the expected shape — required fields present, email address formatted correctly, number within range. Happens server-side always, and optionally client-side for faster feedback. Zod and Joi are popular schema validation libraries for JavaScript. Validation checks shape; [sanitisation](#sanitisation) makes content safe. See [Backend](workflow/08-backend.md).

### Vendor lock-in

Depending on a specific vendor's proprietary features, APIs, or data formats in a way that makes switching difficult or expensive. Common with hosted databases, authentication services, and cloud-specific deployment APIs. Mitigated by abstracting third-party dependencies behind your own interfaces. See [Third-Party Services](tools/third-party.md).

### Version control

A system that tracks every change to every file in a project over time, with the ability to revert, branch, compare, and merge. [Git](#git) is the universal standard. Version control is the single most important tool in the developer workflow — all professional projects use it from day one. See [Dev Environment Tools](tools/dev-environment.md).

### Viewport

The visible area of a web page in the browser window. Its dimensions change with screen size and zoom level. Responsive design uses the viewport width as the trigger for [breakpoints](#breakpoint). The meta tag `<meta name="viewport" content="width=device-width, initial-scale=1">` tells mobile browsers not to scale the page down as if it were a desktop page. See [CSS Architecture](conventions/css.md) and [Testing](workflow/10-testing.md).

---

## W

### WCAG

**Web Content Accessibility Guidelines.** The international standard for web accessibility, published by the W3C. The most commonly required level is **AA**, which includes: 4.5:1 colour contrast for body text, keyboard navigability, screen reader compatibility, and captions for video. Meeting AA is both good practice and a legal requirement in many jurisdictions. See [Accessibility Checklist](checklists/accessibility-checklist.md) and [Semantic HTML](conventions/html.md).

### Webhook

An HTTP callback — your server registers a URL, and a third-party service calls that URL when an event happens (a payment succeeds, an email bounces, a form is submitted). Webhooks push data to you, rather than you polling the API repeatedly. Always verify the webhook signature before trusting the payload. See [Backend](workflow/08-backend.md).

### Wireframe

A low-fidelity layout sketch showing the structure and content hierarchy of a screen, without visual design — no colour, no final typography, no imagery. The goal is to validate layout and user flow quickly before investing in visuals. Can be drawn on paper, in Figma, or in any drawing tool. See [Wireframes](workflow/05-wireframes.md) and [Workflow Overview](workflow/01-overview.md).
