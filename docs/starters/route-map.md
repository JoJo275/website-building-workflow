# Route Map

## Public Routes

```text
/                         Homepage / marketing
/features                 Features overview
/pricing                  Pricing page
/login                    Log in
/signup                   Create account
/forgot-password          Request password reset
/reset-password           Set new password (token via query param)
```

## App Routes (authenticated)

```text
/app                      Redirects to /app/inbox
/app/inbox                Notifications and assigned tasks
/app/projects             All projects in the workspace
/app/projects/new         Create a new project
/app/projects/:id         Project board (Kanban view)
/app/projects/:id/list    Project list view
/app/projects/:id/timeline  Project timeline view
/app/projects/:id/settings  Project settings
/app/tasks/:id            Single task detail
/app/settings             Workspace settings
/app/settings/members     Manage workspace members
/app/settings/billing     Subscription and billing
/app/profile              User profile and preferences
```

## Admin Routes

```text
/admin                    Admin dashboard (internal use only)
/admin/workspaces         List all workspaces
/admin/users              List all users
```

## Notes

- All `/app/*` routes require authentication — redirect to `/login` if no valid session.
- All `/admin/*` routes require the `admin` role — return `403` otherwise.
- `/reset-password` requires a valid, non-expired token in the `token` query parameter.
- `/app/projects/:id` defaults to the Kanban view; the list and timeline views are sub-routes sharing the same project layout.
