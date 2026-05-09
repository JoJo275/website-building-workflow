# Database

Covers schema design, migrations, and data management for development and production.

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
| Relational vs document | SQL for structured data with clear relationships |
| Migrations | Always use migration files, never manual schema changes |
| Seeds | Provide seed data for local development |
| Soft delete | Prefer `deleted_at` over hard deletes for recoverable data |

## Development vs Production

- Use separate databases for development, test, and production
- Never point development at production
- Use environment variables for all connection strings

## Tools

- **PostgreSQL** — the default choice for relational data in production; reliable and well-supported
- **SQLite** — good for local development or lightweight apps that don't need a separate server
- **Prisma or Drizzle** — type-safe ORMs for Node.js; handle migrations, queries, and schema definition
- **Supabase** — managed PostgreSQL with auth, real-time, and file storage built in
- **TablePlus or DB Browser** — GUI clients for inspecting and querying your database locally

See [Backend & Database Tools](../tools/backend.md) for full details.

## Checklist

| Check | Status | Notes |
|-------|--------|-------|
| Schema matches what the application actually needs | To do | |
| Migrations are checked in to version control | To do | |
| Indexes added for common query patterns | To do | |
| Seed data available for local development | To do | |
| Backup strategy defined for production | To do | |
