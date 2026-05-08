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

## Checklist

- [ ] All routes require appropriate auth
- [ ] Input is validated before hitting the database
- [ ] Passwords are hashed, never stored plain
- [ ] Environment variables used for secrets
- [ ] Error messages do not expose internals
- [ ] API returns consistent error shapes
