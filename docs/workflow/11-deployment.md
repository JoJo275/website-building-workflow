# Deployment

Covers hosting, CI/CD pipelines, domains, and monitoring.

## Static Site Hosting

```text
GitHub Pages
Netlify
Vercel
Cloudflare Pages
```

## Dynamic App Hosting

```text
Railway
Render
Fly.io
Vercel serverless
AWS / GCP / Azure
```

## Tools

- **GitHub Actions** — the standard CI/CD pipeline for GitHub repos; runs tests, lint, and deploys on push
- **Vercel or Netlify** — simplest deployment for Next.js and static sites; auto-deploys from the main branch
- **Railway or Render** — managed hosting for full-stack apps and databases without cloud provider complexity
- **Sentry** — error tracking in production; captures exceptions with full stack traces and context
- **Better Uptime or UptimeRobot** — monitors that the site responds and alerts you on downtime
- **Plausible or PostHog** — privacy-friendly analytics for tracking real visitor and usage data

See [Third-Party Services](../tools/third-party.md) for a full list of monitoring and analytics tools.

## Pre-Deployment Checklist

- [ ] Environment variables configured in the hosting provider
- [ ] Production database provisioned and migrated
- [ ] Domain purchased and DNS configured
- [ ] HTTPS enabled
- [ ] Build succeeds locally with production config

## CI/CD Pipeline

The recommended pattern:

```text
Push to main
→ CI runs tests and lint
→ Build step produces artefacts
→ Deploy step publishes to host
→ Smoke test confirms live site
```

## Post-Deployment

- [ ] Live URLs load correctly
- [ ] Auth flow works on production
- [ ] Environment-specific config is correct (no dev URLs, test keys, etc.)
- [ ] Error monitoring is active (e.g. Sentry)
- [ ] Uptime monitoring configured
- [ ] Sitemap submitted if public SEO matters

## Rolling Back

Document the rollback procedure before going live. Know how to:

- Revert a bad deploy
- Restore a database backup
- Disable a feature flag

## Monitoring and Analytics

After launch, instrument the app to understand what is happening in production.

Add:

- Error tracking (e.g. Sentry)
- Uptime checks (e.g. Better Uptime, UptimeRobot)
- Analytics (e.g. Plausible, PostHog, Google Analytics)
- Performance monitoring (e.g. Core Web Vitals, Datadog)
- User feedback tools (e.g. in-app surveys, support inbox)
- Structured logs for API errors

Questions monitoring should answer:

- Are users signing up?
- Where do they drop off?
- Which pages are slow?
- What errors are happening?
- Are API requests failing?
