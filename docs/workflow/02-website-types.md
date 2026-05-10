# Website Types

| Type | Main Workflow |
|---|---|
| Landing page | Copy → wireframe → visual design → static frontend → deploy |
| Portfolio | Content/examples → design → static frontend → deploy |
| Blog/docs | Information architecture → CMS/static generator → content → deploy |
| SaaS app | Product flows → UI design → frontend/backend/database → auth → deploy |
| E-commerce | Catalog → checkout → payments → inventory/orders |
| Dashboard app | Data model → user tasks → components → API integration → states |

## Goals by Type

**Marketing site:** Get visitors to understand the product and sign up.

**Portfolio:** Show credibility and examples of work.

**SaaS app:** Let users sign up, log in, and complete workflows.

**E-commerce:** Help users browse, compare, buy, and manage orders.

**Blog/content site:** Publish searchable, readable articles.

The goal determines everything else — structure, features, and hosting.

## Static vs Dynamic Sites

**Static sites** serve pre-built HTML files with no server-side processing per request.

- Faster and cheaper to host
- No database required
- Best for: landing pages, portfolios, blogs, docs

**Dynamic sites** generate pages on the server or client per request.

- Requires a server or serverless functions
- Handles user-specific data, auth, and payments
- Best for: SaaS apps, dashboards, e-commerce

## What Makes Up a Website

Most websites are composed of some combination of these layers:

| Layer | What it is | Examples |
|---|---|---|
| HTML | Structure and content | Pages, headings, forms, links |
| CSS | Visual presentation | Layout, colour, typography, spacing |
| JavaScript | Interactivity and logic | UI behaviour, API calls, state |
| Assets | Static files | Images, fonts, icons, videos |
| Backend | Server-side logic | APIs, auth, business rules |
| Database | Persistent data | Users, content, orders, settings |
| CDN | Edge delivery | Cached HTML, images, JS, CSS |
| Third-party services | External integrations | Payments, email, analytics, storage |

Not every site needs every layer. A landing page may only need HTML, CSS, and a CDN. A SaaS app needs most of them.

The workflow pages cover each layer in turn: [Frontend](07-frontend.md), [Backend](08-backend.md), [Database](09-database.md), [Deployment](11-deployment.md).
