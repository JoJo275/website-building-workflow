# Backend

Backend handles server-side logic: authentication, data access, business rules, and integrations.

## Backend Responsibilities

| Responsibility | What it involves |
|---|---|
| **User accounts** | Registration, profile data, account settings, deactivation |
| **Authentication** | Login, logout, session management, token refresh, password reset |
| **Permissions** | Role-based or attribute-based access control — who can read, write, or delete what |
| **Database access** | Querying, writing, and migrating data; connection pooling; query optimisation |
| **API endpoints** | Request handling, input validation, response shaping, versioning |
| **File uploads** | Receiving files, validating type and size, storing to disk or object storage (S3, R2), returning a stable URL |
| **Email sending** | Transactional email (welcome, password reset, notifications) via a delivery service |
| **Payments** | Checkout flow, webhook handling, subscription lifecycle, refunds |
| **Admin tools** | Internal dashboards for viewing and managing data, impersonating users, triggering jobs |
| **Background jobs** | Async work that should not block a request: email queues, image processing, report generation, scheduled tasks |

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

## Common Tools

### Frameworks

- **FastAPI** — Python; fast, well-documented, automatic OpenAPI schema generation
- **Django** — Python; batteries-included with ORM, admin panel, and auth out of the box
- **Flask** — Python; minimal and flexible; good when you want to choose each component yourself
- **Express** — Node.js; minimal and widely used; large ecosystem of middleware
- **Hono** — Node.js / edge-compatible; lightweight and fast; works with Next.js API routes
- **Rails** — Ruby; convention-over-configuration; fast to build CRUD apps with
- **Laravel** — PHP; full-featured with ORM, queues, auth, and a polished developer experience
- **Spring** — Java / Kotlin; mature and widely used in enterprise environments
- **ASP.NET** — C#; Microsoft's framework; strong typing and good tooling in the .NET ecosystem

### Validation and testing

- **Zod or Joi** — schema validation for JavaScript/TypeScript; validate all request input at the boundary
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
