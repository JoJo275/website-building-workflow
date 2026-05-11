# Route Map

A route map is a plain list of every URL in the site or app — written before implementation so the team agrees on the shape of the product before touching a framework router. It is not a sitemap diagram; it is the authoritative reference for what routes exist, what they do, who can access them, and what edge cases apply.

---

## Conventions

### URL format

- Lowercase only — never `/UserProfile`, always `/user-profile`
- Hyphens to separate words — never underscores or camelCase
- No trailing slash — `/settings`, not `/settings/`
- Plural for collections, singular for single resources: `/projects` (list), `/projects/:id` (one project)
- Dynamic segments use `:param` notation in templates; actual frameworks may use `[id]`, `{id}`, or `<id>`

### Route groups

Prefix routes by access level to make auth requirements obvious at a glance:

| Prefix | Access |
|---|---|
| `/` (no prefix) | Public — no auth required |
| `/app/…` | Authenticated — valid session required |
| `/admin/…` | Admin role required |
| `/api/…` | API endpoints — auth varies per endpoint |

Adjust prefixes to your app's needs. The point is consistency — every developer should be able to infer auth requirements from the URL alone.

### Auth behaviour

State the redirect rule explicitly for each protected group:

- Unauthenticated request to `/app/*` → redirect to `/login?next=<original-url>`
- Non-admin request to `/admin/*` → `403 Forbidden` (never redirect — that leaks route existence)
- Expired or invalid token on `/reset-password` → redirect to `/forgot-password` with an error message

### Dynamic routes

Document what the dynamic segment refers to and what happens when it is missing or invalid:

| Route | Segment | Fallback |
|---|---|---|
| `/app/projects/:id` | Project UUID | 404 if not found; 403 if no access |
| `/app/tasks/:id` | Task UUID | 404 if not found |
| `/reset-password` | `?token=` query param | Redirect to `/forgot-password` |
| `/blog/:slug` | Post slug | 404 |

### Route redirects

Redirects are part of the route map. Document them:

```text
/app               →  /app/dashboard     (default app landing)
/account           →  /app/profile       (legacy URL support)
/home              →  /                  (alias)
```

### API routes

If the API lives in the same repo (Next.js routes, SvelteKit `+server.ts`, Express), list them here too, or in a separate `api-routes.md`. At minimum, capture the method, path, auth requirement, and one-line description.

```text
GET    /api/projects          Auth required   List projects for current workspace
POST   /api/projects          Auth required   Create a new project
GET    /api/projects/:id      Auth required   Get single project
PATCH  /api/projects/:id      Auth required   Update project
DELETE /api/projects/:id      Auth required   Delete project
POST   /api/auth/login        Public          Exchange credentials for session
POST   /api/auth/logout       Auth required   Invalidate session
POST   /api/webhooks/stripe   Public + sig    Stripe payment events
```

### Naming rules

These apply across public, app, admin, and API routes:

**Use the resource name, not the action.** REST convention: the URL names the thing, the HTTP method names the action.

| Wrong | Right | Reason |
|---|---|---|
| `/get-projects` | `GET /projects` | Verb belongs in the method, not the URL |
| `/create-user` | `POST /users` | Same — POST implies creation |
| `/delete-post/:id` | `DELETE /posts/:id` | Method carries the intent |
| `/user-settings-edit` | `/settings` or `PATCH /settings` | No verb, no redundant suffix |

**Be consistent with tense and plurality.** Pick a pattern and never break it:

- Collections are always plural: `/posts`, `/users`, `/projects`
- Single resources always use the collection parent: `/posts/:id`, not `/post/:id`
- Avoid mixing: never `/post` for creation and `/posts` for listing

**Avoid encoding state or format in the URL.** State belongs in query params; format belongs in the `Accept` header or a suffix:

| Wrong | Right |
|---|---|
| `/projects-active` | `/projects?status=active` |
| `/projects.json` | `Accept: application/json` header |
| `/projects-archived-list` | `/projects?status=archived` |

**Keep routes shallow.** More than three segments is usually a design smell:

```text
Good:  /projects/:id/settings
Avoid: /workspaces/:wid/projects/:pid/tasks/:tid/comments/:cid
```

When routes go deep, the parent resource is probably a better anchor. A task comment can be `/comments/:id` — the task relationship lives in the response, not the URL.

**Don't leak implementation details.** URLs are a public API — they should reflect the user-facing model, not the database schema or internal naming:

| Leaks internals | User-facing |
|---|---|
| `/tbl_users/:uuid` | `/users/:id` |
| `/sys/admin_panel` | `/admin` |
| `/v1/api/graphql_endpoint` | `/api/graphql` |

### Query parameters

Query params are for filtering, sorting, and pagination — not for identifying a resource. The resource ID always belongs in the path.

| Use case | Convention |
|---|---|
| Filter | `?status=active` `?type=bug` |
| Sort | `?sort=created_at&order=desc` |
| Pagination | `?page=2&per_page=25` or `?cursor=<token>` |
| Search | `?q=search+term` |
| Multi-value filter | `?tag=design&tag=ux` (repeated param) |

Document any query params that affect route behaviour (auth, content, layout) in the route's notes row — they are easy to forget and hard to discover later.

### Versioning API routes

Version the API path when you need to ship breaking changes without breaking existing clients:

```text
/api/v1/projects     ← current stable version
/api/v2/projects     ← new version under development
```

Only version when you have to. Internal APIs used only by your own frontend rarely need versioning — you deploy both sides together. External or public APIs always do.

---

## Template

Replace the content below with your own routes. Keep the section headings — they are the minimum set most apps need.

### Public routes

```text
/                         Homepage
/features                 Features overview
/pricing                  Pricing page
/blog                     Blog listing
/blog/:slug               Individual blog post
/about                    About page
/contact                  Contact form
/login                    Log in
/signup                   Create account
/forgot-password          Request password reset email
/reset-password           Set new password (requires ?token= query param)
/terms                    Terms of service
/privacy                  Privacy policy
```

### App routes (authenticated)

```text
/app                      Redirect → /app/dashboard
/app/dashboard            Main dashboard
/app/[resource]           List view for primary resource
/app/[resource]/new       Create new resource
/app/[resource]/:id       Detail / edit view
/app/settings             Account settings
/app/settings/profile     Profile and preferences
/app/settings/billing     Subscription and billing
```

### Admin routes (admin role required)

```text
/admin                    Admin dashboard
/admin/users              User list and management
/admin/[resource]         Manage resource type
```

### API routes

```text
GET    /api/[resource]        Auth required   List
POST   /api/[resource]        Auth required   Create
GET    /api/[resource]/:id    Auth required   Read one
PATCH  /api/[resource]/:id    Auth required   Update
DELETE /api/[resource]/:id    Auth required   Delete
POST   /api/auth/login        Public          Authenticate
POST   /api/auth/logout       Auth required   End session
```

---

!!! example "Worked example — SaaS project management app"

    ### Public routes

    ```text
    /                         Homepage / marketing
    /features                 Features overview
    /pricing                  Pricing page
    /login                    Log in
    /signup                   Create account
    /forgot-password          Request password reset
    /reset-password           Set new password (requires ?token= query param)
    ```

    ### App routes (authenticated)

    ```text
    /app                      Redirect → /app/inbox
    /app/inbox                Notifications and assigned tasks
    /app/projects             All projects in the workspace
    /app/projects/new         Create a new project
    /app/projects/:id         Project board (default: Kanban view)
    /app/projects/:id/list    Project list view (shares project layout)
    /app/projects/:id/timeline  Project timeline view (shares project layout)
    /app/projects/:id/settings  Project settings
    /app/tasks/:id            Single task detail panel
    /app/settings             Workspace settings
    /app/settings/members     Manage workspace members
    /app/settings/billing     Subscription and billing
    /app/profile              User profile and preferences
    ```

    ### Admin routes (admin role required)

    ```text
    /admin                    Admin dashboard (internal only)
    /admin/workspaces         List all workspaces
    /admin/users              List all users
    ```

    ### API routes

    ```text
    GET    /api/projects          Auth required   List workspace projects
    POST   /api/projects          Auth required   Create project
    GET    /api/projects/:id      Auth required   Get project
    PATCH  /api/projects/:id      Auth required   Update project
    DELETE /api/projects/:id      Auth required   Delete project
    GET    /api/tasks/:id         Auth required   Get task
    PATCH  /api/tasks/:id         Auth required   Update task
    POST   /api/auth/login        Public          Log in
    POST   /api/auth/logout       Auth required   Log out
    POST   /api/webhooks/stripe   Public + sig    Stripe billing events
    ```

    ### Notes

    - All `/app/*` routes redirect unauthenticated users to `/login?next=<url>`.
    - All `/admin/*` routes return `403` for non-admin users — no redirect.
    - `/reset-password` validates the token server-side on load; expired tokens redirect to `/forgot-password`.
    - `/app/projects/:id` defaults to Kanban; list and timeline views share the same project layout shell.
