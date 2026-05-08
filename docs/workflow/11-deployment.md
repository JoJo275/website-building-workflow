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
