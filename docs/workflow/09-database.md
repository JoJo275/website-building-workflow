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

## Checklist

- [ ] Schema matches what the application actually needs
- [ ] Migrations are checked in to version control
- [ ] Indexes added for common query patterns
- [ ] Seed data available for local development
- [ ] Backup strategy defined for production
