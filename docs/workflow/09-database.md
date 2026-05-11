# Database

Covers [schema](../glossary.md#schema) design, [migrations](../glossary.md#migration), and data management for development and production.

## What Database Covers

- Schema design and table structure
- [Migrations](../glossary.md#migration) and version-controlled schema changes
- Relationships, [foreign keys](../glossary.md#foreign-key), and [indexes](../glossary.md#index)
- [Seed data](../glossary.md#seed-data) for local development
- Environment separation (dev, test, production)
- Backup and restore strategy
- Soft deletes and data retention

## Schema Planning

Start with user tasks, not tables. Ask: what data does the app need to store to support each task?

## Common Tables

```text
users
organizations
projects
items
tags
comments
settings
audit_logs
```

## Key Decisions

| Decision | Notes |
|---|---|
| [Relational](../glossary.md#relational-database) vs [document](../glossary.md#document-database) | SQL for structured data with clear relationships |
| [Migrations](../glossary.md#migration) | Always use migration files, never manual schema changes |
| Seeds | Provide [seed data](../glossary.md#seed-data) for local development |
| [Soft delete](../glossary.md#soft-delete) | Prefer `deleted_at` over hard deletes for recoverable data |

## Development vs Production

- Use separate databases for development, test, and production
- Never point development at production
- Use environment variables for all connection strings

## Common Tools

### Databases

- **PostgreSQL** — the default choice for relational data; reliable, well-supported, and production-ready
- **MySQL** — widely used relational database; large hosting ecosystem; good for read-heavy workloads
- **SQLite** — file-based; no server required; ideal for local development, embedded apps, or small tools
- **MongoDB** — [document database](../glossary.md#document-database); stores JSON-like records; suits unstructured or highly variable data
- **Redis** — in-memory key/value store; used for caching, sessions, [rate limiting](../glossary.md#rate-limiting), and queues

### ORMs and clients

- **Prisma or Drizzle** — type-safe [ORMs](../glossary.md#orm) for Node.js; handle migrations, queries, and schema definition
- **Supabase** — managed PostgreSQL with auth, real-time, and file storage built in
- **TablePlus or DB Browser** — GUI clients for inspecting and querying your database locally

See [Backend & Database Tools](../tools/backend.md) for full details.

## Checklist

| Check | Status | Notes |
|-------|--------|-------|
| Schema matches what the application actually needs | To do | |
| Migrations are checked in to version control | To do | |
| [Indexes](../glossary.md#index) added for common query patterns | To do | |
| Seed data available for local development | To do | |
| Backup strategy defined for production | To do | |
