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

## Notes

- Always include a `.env.example` — commit it, never commit `.env`
- Keep `README.md` accurate: setup steps, env vars, how to run locally
- Match the structure to the framework conventions — do not fight the defaults
