# Repo Layouts

Reference structures for common project types. Copy the pattern that fits your project and adjust as needed.

---

## Static Site

Portfolio, landing page, documentation, or blog. No server required.

```text
my-site/
├── public/                 # Static assets (images, fonts, favicon)
├── src/
│   ├── pages/              # One file per route
│   ├── components/         # Reusable UI pieces
│   ├── styles/             # Global CSS or Tailwind config
│   └── content/            # Markdown or JSON content files
├── index.html              # Entry point (if no framework)
├── package.json
└── README.md
```

Good for: Astro, Eleventy, plain HTML/CSS, Jekyll, Hugo.

---

## Next.js App (App Router)

SaaS product, dashboard, or content-heavy app with server rendering.

```text
my-app/
├── public/                 # Static assets
├── src/
│   ├── app/                # Routes (App Router convention)
│   │   ├── (auth)/         # Route group — auth pages
│   │   │   ├── login/
│   │   │   │   └── page.tsx
│   │   │   └── signup/
│   │   │       └── page.tsx
│   │   ├── (dashboard)/    # Route group — app pages behind auth
│   │   │   ├── dashboard/
│   │   │   │   └── page.tsx
│   │   │   └── settings/
│   │   │       └── page.tsx
│   │   ├── layout.tsx      # Root layout
│   │   └── page.tsx        # Home page
│   ├── components/
│   │   ├── ui/             # Base UI components (button, input, etc.)
│   │   └── [feature]/      # Feature-specific components
│   ├── lib/                # Utilities, helpers, API clients
│   ├── hooks/              # Custom React hooks
│   ├── types/              # Shared TypeScript types
│   └── styles/
│       └── globals.css
├── .env.local              # Local environment variables (never commit)
├── .env.example            # Committed template for env vars
├── next.config.ts
├── tailwind.config.ts
├── tsconfig.json
├── package.json
└── README.md
```

Good for: SaaS apps, dashboards, auth flows, e-commerce, marketing + app combos.

---

## Python / FastAPI Backend

API-only backend or backend to pair with a separate frontend.

```text
my-api/
├── app/
│   ├── api/
│   │   └── v1/
│   │       ├── routes/         # One file per resource group
│   │       │   ├── users.py
│   │       │   └── items.py
│   │       └── __init__.py
│   ├── core/
│   │   ├── config.py           # Settings from environment variables
│   │   └── security.py         # Auth helpers
│   ├── db/
│   │   ├── models.py           # SQLAlchemy or similar ORM models
│   │   └── session.py          # Database session factory
│   ├── schemas/                # Pydantic request/response schemas
│   ├── services/               # Business logic, separated from routes
│   └── main.py                 # FastAPI app entry point
├── tests/
│   ├── test_users.py
│   └── test_items.py
├── alembic/                    # Database migrations
├── .env
├── .env.example
├── pyproject.toml
└── README.md
```

Good for: REST APIs, data pipelines, backend services, auth servers.

---

## Full-Stack Monorepo

Frontend and backend in one repo. Useful for solo developers or small teams.

```text
my-project/
├── apps/
│   ├── web/                    # Frontend (Next.js, Astro, etc.)
│   └── api/                    # Backend (FastAPI, Express, etc.)
├── packages/
│   ├── ui/                     # Shared component library (optional)
│   ├── types/                  # Shared TypeScript types (optional)
│   └── config/                 # Shared ESLint, Tailwind, tsconfig
├── .github/
│   └── workflows/
│       ├── ci.yml              # CI pipeline
│       └── deploy.yml          # Deployment workflow
├── docker-compose.yml          # Local dev environment
└── README.md
```

Good for: SaaS products, internal tools, projects where frontend and backend are tightly coupled.

---

## SvelteKit App

Full-stack app using SvelteKit's file-based routing and server routes.

```text
my-app/
├── src/
│   ├── lib/
│   │   ├── components/         # Reusable Svelte components
│   │   │   ├── ui/             # Base UI (Button.svelte, Input.svelte, etc.)
│   │   │   └── [feature]/      # Feature-specific components
│   │   ├── server/             # Server-only utilities (db, auth, email)
│   │   ├── stores/             # Svelte writable/derived stores
│   │   └── utils/              # Shared helpers
│   ├── routes/
│   │   ├── (auth)/             # Route group — login, signup
│   │   │   ├── login/
│   │   │   │   └── +page.svelte
│   │   │   └── signup/
│   │   │       └── +page.svelte
│   │   ├── (app)/              # Route group — authenticated pages
│   │   │   ├── dashboard/
│   │   │   │   ├── +page.svelte
│   │   │   │   └── +page.server.ts
│   │   │   └── settings/
│   │   │       └── +page.svelte
│   │   ├── api/                # API routes (+server.ts files)
│   │   │   └── webhooks/
│   │   │       └── +server.ts
│   │   ├── +layout.svelte      # Root layout
│   │   └── +page.svelte        # Home page
│   ├── app.html                # HTML shell
│   └── app.css                 # Global styles
├── static/                     # Static assets (images, fonts, favicon)
├── .env
├── .env.example
├── svelte.config.js
├── vite.config.ts
├── package.json
└── README.md
```

Good for: SaaS apps, dashboards, and full-stack projects that prefer Svelte's syntax. Lucia Auth and Drizzle ORM integrate well with this layout.

---

## Astro Content Site

Blog, documentation, or marketing site with content-heavy pages and minimal JavaScript.

```text
my-site/
├── public/                     # Copied as-is: favicons, OG images, fonts
├── src/
│   ├── components/
│   │   ├── layout/             # Header, Footer, Navigation
│   │   │   ├── Header.astro
│   │   │   ├── Footer.astro
│   │   │   └── Nav.astro
│   │   ├── ui/                 # Reusable UI (Button, Card, Badge, etc.)
│   │   └── blog/               # Blog-specific components
│   ├── content/
│   │   ├── blog/               # Markdown blog posts
│   │   │   └── my-first-post.md
│   │   └── config.ts           # Content collection schemas
│   ├── layouts/
│   │   ├── Base.astro          # HTML shell with <head>
│   │   ├── Page.astro          # Generic page wrapper
│   │   └── Post.astro          # Blog post layout
│   ├── pages/
│   │   ├── index.astro         # Home page
│   │   ├── about.astro
│   │   ├── blog/
│   │   │   ├── index.astro     # Blog listing
│   │   │   └── [...slug].astro # Dynamic post page
│   │   └── rss.xml.ts          # RSS feed
│   ├── styles/
│   │   └── global.css
│   └── utils/
│       └── formatDate.ts
├── astro.config.mjs
├── tailwind.config.mjs         # If using Tailwind
├── tsconfig.json
├── package.json
└── README.md
```

Good for: Blogs, documentation sites, marketing pages. Mix in React, Vue, or Svelte components (Astro islands) for interactive sections without shipping JS to the whole page.

---

## Express + React (Separate Frontend/Backend)

API server and frontend decoupled — each deployed independently.

```text
my-project/
├── client/                     # React frontend (Vite)
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── ui/             # Base UI components
│   │   │   └── [feature]/
│   │   ├── pages/              # Route-level components
│   │   │   ├── Home.tsx
│   │   │   ├── Dashboard.tsx
│   │   │   └── Login.tsx
│   │   ├── hooks/              # Custom React hooks
│   │   ├── lib/                # API client, utilities
│   │   ├── store/              # State (Zustand, Redux, etc.)
│   │   ├── types/
│   │   ├── App.tsx
│   │   └── main.tsx
│   ├── index.html
│   ├── vite.config.ts
│   └── package.json
│
└── server/                     # Express backend (Node.js)
    ├── src/
    │   ├── routes/
    │   │   ├── auth.ts
    │   │   ├── users.ts
    │   │   └── items.ts
    │   ├── middleware/
    │   │   ├── auth.ts         # JWT or session validation
    │   │   └── errorHandler.ts
    │   ├── controllers/        # Route handlers separated from routing
    │   ├── services/           # Business logic
    │   ├── models/             # Database models (Prisma schema or ORM)
    │   ├── db/
    │   │   └── client.ts       # Prisma client or DB connection
    │   ├── utils/
    │   └── app.ts              # Express app setup
    ├── prisma/
    │   └── schema.prisma
    ├── .env
    ├── .env.example
    ├── tsconfig.json
    └── package.json
```

Good for: Projects where the frontend and backend need different deployment targets, different scaling, or will eventually be split across teams. The client calls the server via a REST or tRPC API.

---

## Custom Component Library

A standalone package of reusable UI components, separate from any app. Used as an internal design system shared across multiple projects.

```text
my-ui/
├── src/
│   ├── components/
│   │   ├── Button/
│   │   │   ├── Button.tsx
│   │   │   ├── Button.stories.tsx   # Storybook story
│   │   │   ├── Button.test.tsx      # Unit/component tests
│   │   │   └── index.ts             # Re-export
│   │   ├── Input/
│   │   │   ├── Input.tsx
│   │   │   ├── Input.stories.tsx
│   │   │   └── index.ts
│   │   ├── Modal/
│   │   ├── Toast/
│   │   └── index.ts                 # Barrel — exports all components
│   ├── tokens/
│   │   ├── tokens.css               # CSS custom properties
│   │   └── tokens.ts                # JS/TS token constants (optional)
│   ├── hooks/                       # Shared hooks (useMediaQuery, etc.)
│   └── utils/                       # Shared utilities (cn, formatDate, etc.)
├── .storybook/
│   ├── main.ts
│   └── preview.ts
├── dist/                            # Build output — do not edit
├── tsconfig.json
├── vite.config.ts                   # Library build mode
├── package.json                     # name, exports, peerDependencies
└── README.md
```

Good for: Teams building multiple apps that share a design system. Consumers install it as a package (`npm install @my-org/ui`) and import components directly. Storybook is the primary development environment.

---

## T3 Stack (Next.js + tRPC + Prisma + NextAuth)

A popular opinionated stack for type-safe full-stack apps. tRPC replaces a conventional REST API — types flow from server to client with no code generation step.

```text
my-app/
├── prisma/
│   └── schema.prisma               # Database schema
├── public/
├── src/
│   ├── app/                        # Next.js App Router
│   │   ├── api/
│   │   │   ├── auth/
│   │   │   │   └── [...nextauth]/
│   │   │   │       └── route.ts    # NextAuth handler
│   │   │   └── trpc/
│   │   │       └── [trpc]/
│   │   │           └── route.ts    # tRPC HTTP handler
│   │   ├── dashboard/
│   │   │   └── page.tsx
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── components/
│   │   ├── ui/
│   │   └── [feature]/
│   ├── server/
│   │   ├── api/
│   │   │   ├── routers/            # tRPC routers (one per feature)
│   │   │   │   ├── user.ts
│   │   │   │   └── item.ts
│   │   │   ├── root.ts             # Merge all routers
│   │   │   └── trpc.ts             # tRPC init and middleware
│   │   ├── auth.ts                 # NextAuth config
│   │   └── db.ts                   # Prisma client
│   ├── styles/
│   │   └── globals.css
│   └── trpc/                       # tRPC client-side helpers
│       ├── react.tsx
│       └── server.ts
├── .env
├── .env.example
├── next.config.ts
├── tailwind.config.ts
├── tsconfig.json
├── package.json
└── README.md
```

Good for: Type-safe SaaS apps where you want end-to-end type safety without writing a separate API schema. The tradeoff is framework lock-in — all of T3's pieces are tightly coupled.

---

## Notes

- Always include a `.env.example` — commit it, never commit `.env`
- Keep `README.md` accurate: setup steps, env vars, how to run locally
- Match the structure to the framework conventions — do not fight the defaults
- In monorepos, keep shared packages in `packages/` and deployable apps in `apps/`
- A custom component library deserves its own repo once it is shared across two or more apps
