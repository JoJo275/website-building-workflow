# Backend & Database Tools

Server frameworks, databases, ORMs, and related tools for building the server-side of a web app.

## Backend Frameworks

### FastAPI (Python)

A modern, fast Python framework for building APIs. Automatic OpenAPI docs, async support, type hints throughout.

**Good for:** Python-first teams, data-heavy apps, quick API development.

```text
GET  /items
POST /items
PATCH /items/{id}
```

<https://fastapi.tiangolo.com>

### Django (Python)

A batteries-included Python framework with a built-in admin panel, ORM, auth, and more.

**Good for:** Full-featured apps where you want the most functionality out of the box.

<https://djangoproject.com>

### Flask (Python)

A minimal Python framework. More control, less built-in.

**Good for:** Small APIs, microservices, prototypes.

<https://flask.palletsprojects.com>

### Express (Node.js)

The most widely used Node.js framework. Minimal and flexible.

**Good for:** JavaScript-only stacks, microservices, lightweight APIs.

<https://expressjs.com>

### Fastify (Node.js)

A faster alternative to Express with a plugin system and built-in schema validation.

<https://fastify.dev>

### Hono (Node.js / Edge)

A lightweight, fast web framework that runs on Node.js, Cloudflare Workers, and other edge runtimes.

**Good for:** Edge deployments, API routes in Next.js or SvelteKit.

<https://hono.dev>

### Rails (Ruby)

A full-stack framework with conventions for everything. Extremely productive for standard CRUD apps.

**Good for:** Startups and teams that want to move fast with conventional structure.

<https://rubyonrails.org>

### Laravel (PHP)

A full-featured PHP framework. Strong ecosystem, Eloquent ORM, built-in auth scaffolding.

**Good for:** PHP environments, content-heavy apps.

<https://laravel.com>

## Databases

### PostgreSQL

The recommended default for serious relational data.

- Full SQL support with advanced features (JSON columns, full-text search, window functions)
- Open source, widely hosted
- Better default choice than SQLite for production apps

<https://postgresql.org>

### SQLite

A file-based database requiring no server. Excellent for development, simple apps, and small deployments.

- Zero configuration
- Single file
- Not suitable for high-concurrency production workloads

<https://sqlite.org>

### MySQL / MariaDB

Widely used relational database. Good compatibility and performance.

<https://mysql.com>

### MongoDB

A document (NoSQL) database storing data as JSON-like documents.

**Good for:** Flexible schemas, content, or data that does not fit a relational model.

<https://mongodb.com>

### Redis

An in-memory key-value store used for caching, sessions, queues, and real-time features.

**Good for:** Caching API responses, storing sessions, background job queues.

<https://redis.io>

## Hosted Database Services

| Service | Database | Notes |
|---|---|---|
| Supabase | PostgreSQL | Includes auth, storage, and real-time |
| Neon | PostgreSQL | Serverless, scales to zero |
| PlanetScale | MySQL | Branching workflow, serverless |
| Turso | SQLite (libSQL) | Edge-optimised SQLite |
| MongoDB Atlas | MongoDB | Fully managed |
| Upstash | Redis | Serverless Redis |

## ORMs and Query Builders

### Prisma (TypeScript/JavaScript)

A type-safe ORM with a declarative schema and auto-generated TypeScript types.

```typescript
const user = await prisma.user.findUnique({ where: { id: 1 } })
```

<https://prisma.io>

### Drizzle (TypeScript/JavaScript)

A lightweight, type-safe query builder closer to raw SQL than a traditional ORM.

<https://orm.drizzle.team>

### SQLAlchemy (Python)

The standard Python ORM. Powerful and flexible, supports both ORM and Core (raw SQL) modes.

<https://sqlalchemy.org>

### Django ORM (Python)

Built into Django. Simple, readable, good for standard CRUD operations.

## Choosing a Database

| Situation | Recommended |
|---|---|
| New relational app | PostgreSQL |
| Local development / simple app | SQLite |
| Need built-in auth + storage | Supabase (PostgreSQL) |
| Serverless / edge deployment | Neon or Turso |
| Flexible document data | MongoDB |
| Caching and sessions | Redis |
