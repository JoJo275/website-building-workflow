# Third-Party Services

External services for authentication, payments, email, analytics, storage, and AI integration.

## Authentication

### Clerk

A hosted auth service with pre-built UI components for sign-up, sign-in, and user management.

- React and Next.js components included
- Social logins, email/password, MFA out of the box
- User management dashboard

**Good for:** Getting auth working in hours, not days.

<https://clerk.com>

### Auth0

A mature, enterprise-grade identity platform.

- Supports many identity providers and protocols
- More flexible and complex than Clerk
- Good for apps with complex permission requirements

<https://auth0.com>

### NextAuth.js / Auth.js

An open-source authentication library for Next.js (and other frameworks).

- Self-hosted, no vendor lock-in
- Supports many providers (Google, GitHub, credentials, etc.)
- Requires more setup than Clerk

<https://authjs.dev>

### Supabase Auth

PostgreSQL-based authentication built into Supabase.

- Included when using Supabase as your database
- Email/password, magic links, social logins
- Row-level security integration with the database

<https://supabase.com>

## Payments

### Stripe

The industry standard for payments. Handles card processing, subscriptions, invoices, refunds, and more.

- Excellent API and documentation
- Stripe Checkout for hosted payment pages
- Webhooks for subscription lifecycle events

**Required for:** Any app that charges money.

<https://stripe.com>

### Paddle

A payment processor and merchant of record. Handles VAT, tax, and compliance globally.

**Good for:** Digital products and SaaS selling internationally, where tax handling is complex.

<https://paddle.com>

### Lemon Squeezy

A simpler alternative to Paddle, also a merchant of record with built-in tax handling.

<https://lemonsqueezy.com>

## Email

### Resend

A developer-focused email sending API. Simple REST API, React Email component support, good deliverability.

```typescript
await resend.emails.send({
  from: 'hello@example.com',
  to: 'user@example.com',
  subject: 'Welcome',
  react: WelcomeEmail({ name }),
})
```

<https://resend.com>

### Postmark

A transactional email service focused on deliverability. Good for welcome emails, password resets, and notifications.

<https://postmarkapp.com>

### SendGrid

A high-volume email platform. Used for both transactional and marketing email.

<https://sendgrid.com>

## Analytics

### PostHog

An open-source product analytics platform. Tracks events, user behaviour, funnels, feature flags, and session replays.

- Self-hostable or cloud
- Feature flags built in
- Session recording

<https://posthog.com>

### Plausible

A lightweight, privacy-friendly analytics tool. GDPR-compliant with no cookies.

**Good for:** Public sites where simple traffic stats are enough.

<https://plausible.io>

### Umami

An open-source, self-hosted analytics alternative to Google Analytics.

<https://umami.is>

### Google Analytics (GA4)

The most widely used analytics platform. Free, powerful, but heavier and more complex than Plausible or Umami.

<https://analytics.google.com>

## Error Tracking

### Sentry

The standard tool for tracking runtime errors, exceptions, and performance issues.

- Captures stack traces with source maps
- Groups similar errors
- Alerts and integrations with Slack, GitHub, etc.

<https://sentry.io>

### Axiom

A log management and analytics platform.

**Good for:** Structured logging, querying logs across services.

<https://axiom.co>

## File Storage

### Cloudflare R2

S3-compatible object storage with no egress fees. Excellent for storing user uploads and assets.

<https://cloudflare.com/products/r2>

### AWS S3

The original and most widely used object storage service.

<https://aws.amazon.com/s3>

### Uploadthing

A file upload service with a simple TypeScript API, designed for Next.js apps.

<https://uploadthing.com>

## CMS

### Sanity

A headless CMS with a real-time content API and a customisable editing studio.

**Good for:** Content-heavy sites where editors need a custom interface.

<https://sanity.io>

### Contentful

A mature, enterprise headless CMS.

<https://contentful.com>

### Payload

An open-source, code-first headless CMS built with TypeScript and Next.js.

**Good for:** Teams that want CMS and app in the same repo.

<https://payloadcms.com>

## AI and LLM Integration

### OpenAI API

Provides access to GPT-4, DALL-E, embeddings, and Whisper (speech-to-text).

<https://platform.openai.com>

### Anthropic API

Provides access to the Claude model family.

<https://anthropic.com>

### Vercel AI SDK

A TypeScript library for building AI-powered UIs with streaming, tool calling, and support for multiple providers.

```typescript
import { streamText } from 'ai'
import { openai } from '@ai-sdk/openai'

const result = streamText({ model: openai('gpt-4o'), prompt })
```

<https://sdk.vercel.ai>

## Choosing Third-Party Services

| Need | Recommended |
|---|---|
| Auth (quickest setup) | Clerk |
| Auth (self-hosted) | Auth.js |
| Payments | Stripe |
| Payments + tax handling | Paddle or Lemon Squeezy |
| Transactional email | Resend |
| Product analytics | PostHog |
| Simple traffic analytics | Plausible |
| Error tracking | Sentry |
| File uploads | Cloudflare R2 or Uploadthing |
| AI streaming UI | Vercel AI SDK |
