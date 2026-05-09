# Backend

Backend handles server-side logic: authentication, data access, business rules, and integrations.

## Backend Responsibilities

- Authentication and sessions
- User accounts and permissions
- API routes
- Database access
- Email sending
- Payments
- Background jobs
- Admin tooling

## Example API Routes

```text
GET    /items
POST   /items
PATCH  /items/{id}
DELETE /items/{id}
POST   /auth/login
POST   /auth/signup
POST   /auth/logout
GET    /auth/me
```

## Security Basics

- Never trust client input — validate and sanitise server-side
- Use parameterised queries, never string-interpolated SQL
- Hash passwords with bcrypt or argon2
- Use HTTPS everywhere
- Apply least-privilege to database credentials
- Rate-limit auth endpoints

## Tools

- **Next.js API routes or Hono** — lightweight option for apps already using a JavaScript frontend framework
- **FastAPI** — fast, well-documented Python framework with automatic OpenAPI schema generation
- **Express or Fastify** — minimal Node.js options for more control over structure and middleware
- **Zod or Joi** — schema validation libraries; validate all request input at the boundary
- **Postman or HTTPie** — test API routes manually and inspect responses during development

See [Backend & Database Tools](../tools/backend.md) for a full list of frameworks and libraries.

## Checklist

| Check | Status | Notes |
|-------|--------|-------|
| All routes require appropriate auth | To do | |
| Input is validated before hitting the database | To do | |
| Passwords are hashed, never stored plain | To do | |
| Environment variables used for secrets | To do | |
| Error messages do not expose internals | To do | |
| API returns consistent error shapes | To do | |
