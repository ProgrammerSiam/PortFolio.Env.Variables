# Environment Variables

This document describes every environment variable used in this project, grouped by module. Each entry includes the variable's **purpose**, **where it's used**, and **where to get the value**.

## What This File Covers

- GitHub integration (contribution graph, API access)
- DMCA protection badge
- Analytics (PostHog, OpenPanel, Google Analytics, Umami, Vercel Analytics)
- Bot protection / anti-spam (reCAPTCHA, hCaptcha)
- SEO & site verification (Google, Bing, canonical URL)
- Social share / Open Graph
- Contact form / transactional email
- Coding stats widget (WakaTime)
- Blog / CMS integration
- Guestbook
- Newsletter signup
- Security & performance (rate limiting, cron protection, ISR revalidation, image domains)
- Cookie consent / GDPR
- Maintenance mode
- Resume/CV download
- Dynamic `robots.txt` & `sitemap.xml` setup

## Who Should Use This

- **Anyone setting up this project locally** — copy `.env.example` to `.env.local` and fill in the values described here.
- **Anyone deploying this project** (Vercel, VPS, etc.) — use this as the checklist for which secrets/keys to configure in the hosting provider's environment settings.
- **Contributors** — use this to understand what each integration does before touching related code.
- **Future you** — as a reference when a module is added, removed, or a key rotates.

### What Level of Knowledge Do You Need?

You don't need to be an expert in every service listed here — this guide is written so a **beginner-to-intermediate Next.js developer** can follow it without prior experience with any specific provider (PostHog, Resend, Upstash, etc.). That said, it helps most if you:

| If you are... | This guide helps you... |
|---|---|
| 🆕 **New to the project** | Understand what each variable does before blindly copy-pasting `.env.example` |
| 🛠️ **Setting up locally for the first time** | Know exactly which service to sign up for and where to grab each key |
| 🚀 **Deploying to production** | Confirm nothing is missing before the build fails on a hosting platform |
| 🤝 **Contributing a PR** | Add a new integration following the same documentation pattern |
| 🔁 **Rotating a leaked/expired key** | Quickly find which file/route uses that variable |

> If a term here is unfamiliar (e.g. "ISR", "REST token"), each entry links its purpose in plain language — you don't need prior knowledge of the specific tool to understand *why* the variable exists.

## Table of Contents

- [GitHub Integration](#github-integration)
- [DMCA](#dmca)
- [Analytics — PostHog](#analytics--posthog)
- [Analytics — OpenPanel](#analytics--openpanel)
- [Bot Protection / Anti-Spam](#bot-protection--anti-spam)
- [SEO / Site Verification](#seo--site-verification)
- [Additional Analytics Options](#additional-analytics-options)
- [Social Share / Open Graph](#social-share--open-graph)
- [Contact Form / Email](#contact-form--email)
- [WakaTime (Coding Stats)](#wakatime-coding-stats)
- [Blog / CMS](#blog--cms)
- [Guestbook](#guestbook)
- [Newsletter](#newsletter)
- [Security & Performance](#security--performance)
- [Cookie Consent / GDPR](#cookie-consent--gdpr)
- [Maintenance Mode](#maintenance-mode)
- [Resume / CV](#resume--cv)
- [robots.txt & sitemap.xml](#robotstxt--sitemapxml)
- [Full `.env.example`](#full-envexample)

---

## GitHub Integration

### `GITHUB_API_TOKEN`
- **Purpose:** Personal access token for authenticating GitHub API requests.
- **Used for:** Increasing API rate limits, fetching private repo/profile data.
- **Used in:** Server-side API calls (e.g. `/api/github/*` routes).
- **Get it from:** GitHub → Settings → Developer settings → Personal access tokens.

### `GITHUB_CONTRIBUTIONS_API_URL`
- **Purpose:** Base URL of a third-party API (jogruber.de) that returns GitHub contribution graph data.
- **Used for:** Rendering the contribution heatmap on the profile/portfolio page.
- **Used in:** Client or server fetch call that populates the heatmap component.

```env
GITHUB_API_TOKEN=
GITHUB_CONTRIBUTIONS_API_URL=
```

---

## DMCA

### `NEXT_PUBLIC_DMCA_URL`
- **Purpose:** URL for the DMCA protection badge/link.
- **Used for:** Displaying a "DMCA Protected" badge, typically in the footer.
- **Used in:** Footer component (client-side, hence `NEXT_PUBLIC_`).

```env
NEXT_PUBLIC_DMCA_URL=
```

---

## Analytics — PostHog

### `NEXT_PUBLIC_POSTHOG_PROJECT_TOKEN`
- **Purpose:** Project token that identifies your PostHog project.
- **Used for:** Tracking user behavior (page views, events, funnels).
- **Used in:** Client-side PostHog SDK initialization.

### `NEXT_PUBLIC_POSTHOG_HOST`
- **Purpose:** Host URL of the PostHog instance.
- **Used for:** Pointing the SDK to either PostHog Cloud or a self-hosted instance.
- **Used in:** Same PostHog SDK init as above.

```env
NEXT_PUBLIC_POSTHOG_PROJECT_TOKEN=
NEXT_PUBLIC_POSTHOG_HOST=
```

---

## Analytics — OpenPanel

### `NEXT_PUBLIC_OPENPANEL_CLIENT_ID`
- **Purpose:** Client ID for OpenPanel's client-side SDK.
- **Used for:** Browser-side event tracking.
- **Used in:** OpenPanel provider/init on the frontend.

### `OPENPANEL_PROJECT_ID`
- **Purpose:** Identifies which OpenPanel project the server should report to.
- **Used for:** Server-side analytics calls.
- **Used in:** Backend API routes sending events.

### `OPENPANEL_CLIENT_ID`
- **Purpose:** Server-side client ID (separate from the public one) for authenticated server requests.
- **Used for:** Server-to-server OpenPanel API auth.
- **Used in:** Backend event-sending logic.

### `OPENPANEL_CLIENT_SECRET`
- **Purpose:** Secret key that authorizes server-side OpenPanel API access.
- **Used for:** Sending events or reading data from the backend securely.
- **Used in:** Backend API routes, never exposed to the client.

```env
NEXT_PUBLIC_OPENPANEL_CLIENT_ID=
OPENPANEL_PROJECT_ID=
OPENPANEL_CLIENT_ID=
OPENPANEL_CLIENT_SECRET=
```

---

## Bot Protection / Anti-Spam

### `RECAPTCHA_SECRET_KEY`
- **Purpose:** Server-side secret to verify reCAPTCHA tokens.
- **Used for:** Validating form submissions aren't from bots.
- **Used in:** API route that verifies the reCAPTCHA response.

### `NEXT_PUBLIC_RECAPTCHA_SITE_KEY`
- **Purpose:** Public site key that renders the reCAPTCHA widget.
- **Used for:** Loading the reCAPTCHA challenge in the browser.
- **Used in:** Contact/comment forms on the frontend.

### `NEXT_PUBLIC_HCAPTCHA_SITE_KEY`
- **Purpose:** Public site key for hCaptcha, a privacy-friendlier alternative to reCAPTCHA.
- **Used for:** Rendering the hCaptcha widget client-side.
- **Used in:** Forms configured to use hCaptcha instead of/alongside reCAPTCHA.

### `HCAPTCHA_SECRET`
- **Purpose:** Server-side secret to verify hCaptcha responses.
- **Used for:** Validating hCaptcha tokens on submission.
- **Used in:** API route that verifies hCaptcha responses.

```env
RECAPTCHA_SECRET_KEY=
NEXT_PUBLIC_RECAPTCHA_SITE_KEY=
NEXT_PUBLIC_HCAPTCHA_SITE_KEY=
HCAPTCHA_SECRET=
```

---

## SEO / Site Verification

### `NEXT_PUBLIC_GOOGLE_SITE_VERIFICATION`
- **Purpose:** Verification code proving site ownership to Google.
- **Used for:** Enabling Google Search Console access for this domain.
- **Used in:** `<meta>` tag in the root layout/head, or via `metadata.verification` in Next.js.
- **Get it from:** Google Search Console → Settings → Ownership verification → HTML tag method.

### `NEXT_PUBLIC_BING_SITE_VERIFICATION`
- **Purpose:** Verification code proving site ownership to Bing.
- **Used for:** Enabling Bing Webmaster Tools access.
- **Used in:** `<meta>` tag in the root layout/head.
- **Get it from:** Bing Webmaster Tools → Site verification.

### `NEXT_PUBLIC_SITE_URL`
- **Purpose:** The canonical base URL of the deployed site.
- **Used for:** Building absolute URLs for sitemap.xml, robots.txt, canonical tags, and OG images.
- **Used in:** `app/sitemap.ts`, `app/robots.ts`, metadata generation.

```env
NEXT_PUBLIC_GOOGLE_SITE_VERIFICATION=
NEXT_PUBLIC_BING_SITE_VERIFICATION=
NEXT_PUBLIC_SITE_URL=
```

---

## Additional Analytics Options

### `NEXT_PUBLIC_GA_MEASUREMENT_ID`
- **Purpose:** Google Analytics 4 measurement ID.
- **Used for:** Tracking pageviews/events via GA4.
- **Used in:** GA script loaded in the root layout.

### `NEXT_PUBLIC_UMAMI_WEBSITE_ID`
- **Purpose:** Website ID for Umami, a self-hosted privacy-focused analytics tool.
- **Used for:** Tracking traffic without third-party cookies.
- **Used in:** Umami tracking script in the root layout.

### `NEXT_PUBLIC_VERCEL_ANALYTICS`
- **Purpose:** Flag/config to enable Vercel Analytics.
- **Used for:** Built-in Vercel traffic and Web Vitals tracking.
- **Used in:** `@vercel/analytics` component in the root layout.

```env
NEXT_PUBLIC_GA_MEASUREMENT_ID=
NEXT_PUBLIC_UMAMI_WEBSITE_ID=
NEXT_PUBLIC_VERCEL_ANALYTICS=
```

---

## Social Share / Open Graph

### `NEXT_PUBLIC_OG_IMAGE_API`
- **Purpose:** Endpoint that dynamically generates Open Graph preview images.
- **Used for:** Giving each page a unique social-share preview image.
- **Used in:** `generateMetadata` / `opengraph-image` for each route.

### `NEXT_PUBLIC_TWITTER_HANDLE`
- **Purpose:** Your Twitter/X handle.
- **Used for:** Populating the `twitter:site` / `twitter:creator` meta tags.
- **Used in:** Root metadata / Twitter card config.

```env
NEXT_PUBLIC_OG_IMAGE_API=
NEXT_PUBLIC_TWITTER_HANDLE=
```

---

## Contact Form / Email

### `RESEND_API_KEY`
- **Purpose:** API key for Resend, used to send transactional email.
- **Used for:** Delivering messages submitted through the "Contact Me" form.
- **Used in:** API route that handles the contact form submission (e.g. `/api/contact`).
- **Get it from:** Resend dashboard → API Keys.

### `EMAIL_TO`
- **Purpose:** The email address that receives contact-form submissions.
- **Used for:** Routing incoming messages to your inbox.
- **Used in:** Same contact-form API route, as the recipient address.

### `EMAIL_FROM`
- **Purpose:** The "From" address shown to the sender/service.
- **Used for:** Sending the contact-form confirmation or notification email.
- **Used in:** Resend send call in the contact-form API route.

```env
RESEND_API_KEY=
EMAIL_TO=
EMAIL_FROM=
```

---

## WakaTime (Coding Stats)

### `WAKATIME_API_KEY`
- **Purpose:** API key that authorizes requests to WakaTime.
- **Used for:** Pulling your coding activity stats (hours coded, top languages) to show a "Coding Activity" widget.
- **Used in:** Server-side fetch that feeds the stats widget, usually paired with the GitHub contribution graph.
- **Get it from:** WakaTime → Settings → API Key.

```env
WAKATIME_API_KEY=
```

---

## Blog / CMS

### `CONTENTFUL_SPACE_ID`
- **Purpose:** Identifies your Contentful space (or swap for Sanity/Notion/MDX equivalent).
- **Used for:** Fetching blog posts/content for the blog section.
- **Used in:** CMS client initialization, used by blog listing/detail pages.

### `CONTENTFUL_ACCESS_TOKEN`
- **Purpose:** Access token authorizing reads from the CMS.
- **Used for:** Authenticating content fetches from Contentful's API.
- **Used in:** Same CMS client as above.

```env
CONTENTFUL_SPACE_ID=
CONTENTFUL_ACCESS_TOKEN=
```

> If you use a different CMS (Sanity, Notion API, or local MDX files), swap these two for that provider's equivalent credentials.

---

## Guestbook

### `DATABASE_URL`
- **Purpose:** Connection string to a Postgres/Supabase database.
- **Used for:** Storing visitor guestbook entries (name, message, timestamp).
- **Used in:** Guestbook API route (create/list entries) and its ORM client.

```env
DATABASE_URL=
```

> If a guestbook is the only feature needing a database, this can be the same `DATABASE_URL` already used elsewhere in the project — no need to duplicate it.

---

## Newsletter

For a portfolio, the simplest and most maintainable option is **Resend Audiences** (Resend's built-in newsletter/broadcast feature) — since the contact form above already uses Resend, this avoids adding a second email provider. Alternatives like ConvertKit or Buttondown work too, but Resend keeps the stack to one API key.

### `RESEND_AUDIENCE_ID`
- **Purpose:** ID of the Resend Audience (subscriber list) that collects newsletter signups.
- **Used for:** Adding new subscribers when someone submits the newsletter signup form.
- **Used in:** API route for the newsletter signup form (e.g. `/api/newsletter/subscribe`).
- **Get it from:** Resend dashboard → Audiences → create an audience, copy its ID.

```env
RESEND_AUDIENCE_ID=
```

> Reuses `RESEND_API_KEY` from the Contact Form section above — no separate API key needed.

---

## Security & Performance

### `UPSTASH_REDIS_REST_URL`
- **Purpose:** REST endpoint for an Upstash Redis instance.
- **Used for:** Rate limiting the Contact Form and Newsletter signup endpoints to prevent spam/abuse.
- **Used in:** Middleware or API route wrapping form submission handlers.

### `UPSTASH_REDIS_REST_TOKEN`
- **Purpose:** Auth token for the Upstash Redis REST API.
- **Used for:** Authenticating rate-limit read/write calls.
- **Used in:** Same rate-limiting logic as above.

### `CRON_SECRET`
- **Purpose:** Shared secret that verifies scheduled/cron requests are legitimate.
- **Used for:** Protecting a cron endpoint (e.g. periodically refreshing GitHub contribution data) from being triggered by anyone who finds the URL.
- **Used in:** The cron API route, checked against the `Authorization` header.

### `REVALIDATE_SECRET`
- **Purpose:** Secret that authorizes manual ISR (Incremental Static Regeneration) triggers.
- **Used for:** Instantly refreshing a page's static content when a new blog post is published in the CMS.
- **Used in:** `/api/revalidate` route, called by a CMS webhook on publish.

### `NEXT_PUBLIC_IMAGE_DOMAINS`
- **Purpose:** Comma-separated list of external domains allowed for `next/image` optimization.
- **Used for:** Whitelisting image sources like the CMS, GitHub avatars, or OG image API.
- **Used in:** `next.config.js` → `images.remotePatterns` / `images.domains`.

```env
UPSTASH_REDIS_REST_URL=
UPSTASH_REDIS_REST_TOKEN=
CRON_SECRET=
REVALIDATE_SECRET=
NEXT_PUBLIC_IMAGE_DOMAINS=
```

---

## Cookie Consent / GDPR

### `NEXT_PUBLIC_COOKIEYES_ID`
- **Purpose:** ID for a cookie-consent provider (CookieYes, Cookiebot, or similar).
- **Used for:** Showing a cookie consent banner and blocking analytics scripts (PostHog, GA, Umami) until the visitor consents — required for GDPR compliance with EU visitors.
- **Used in:** Root layout, loaded before other analytics scripts.

```env
NEXT_PUBLIC_COOKIEYES_ID=
```

---

## Maintenance Mode

### `NEXT_PUBLIC_MAINTENANCE_MODE`
- **Purpose:** Boolean flag to toggle site-wide maintenance mode.
- **Used for:** Showing a "Site under maintenance" page instead of the normal site while you're making major changes.
- **Used in:** Root layout or middleware, checked before rendering normal pages.

```env
NEXT_PUBLIC_MAINTENANCE_MODE=
```

---

## Resume / CV

### `NEXT_PUBLIC_RESUME_URL`
- **Purpose:** Direct link to your resume/CV file (hosted on Google Drive, S3, or a CDN).
- **Used for:** Powering the "Download Resume" button on the portfolio.
- **Used in:** Hero/About section download button.

```env
NEXT_PUBLIC_RESUME_URL=
```

---

## robots.txt & sitemap.xml

A static `public/robots.txt` applies the same rules to every environment. Using a dynamic `app/robots.ts` instead lets production and staging behave differently — so a staging deployment doesn't accidentally get indexed by Google.

```ts
// app/robots.ts
import { MetadataRoute } from 'next'

export default function robots(): MetadataRoute.Robots {
  const isProd = process.env.NEXT_PUBLIC_ENV === 'production'

  return {
    rules: {
      userAgent: '*',
      allow: isProd ? '/' : '',
      disallow: isProd ? ['/api/', '/admin/'] : '/',
    },
    sitemap: `${process.env.NEXT_PUBLIC_SITE_URL}/sitemap.xml`,
  }
}
```

### `NEXT_PUBLIC_ENV`
- **Purpose:** Identifies the current deployment environment.
- **Used for:** Switching robots.txt rules (allow-all in production, disallow-all elsewhere).
- **Used in:** `app/robots.ts`.

> `NEXT_PUBLIC_SITE_URL` (already listed under SEO above) is reused here to build the sitemap URL, and again in `app/sitemap.ts` to build each page's absolute URL.

```env
NEXT_PUBLIC_ENV=                     # production / staging / development
```

---

## Full `.env.example`

```env
# GitHub Integration
GITHUB_API_TOKEN=
GITHUB_CONTRIBUTIONS_API_URL=

# DMCA
NEXT_PUBLIC_DMCA_URL=

# Analytics — PostHog
NEXT_PUBLIC_POSTHOG_PROJECT_TOKEN=
NEXT_PUBLIC_POSTHOG_HOST=

# Analytics — OpenPanel
NEXT_PUBLIC_OPENPANEL_CLIENT_ID=
OPENPANEL_PROJECT_ID=
OPENPANEL_CLIENT_ID=
OPENPANEL_CLIENT_SECRET=

# Bot Protection / Anti-Spam
RECAPTCHA_SECRET_KEY=
NEXT_PUBLIC_RECAPTCHA_SITE_KEY=
NEXT_PUBLIC_HCAPTCHA_SITE_KEY=
HCAPTCHA_SECRET=

# SEO / Site Verification
NEXT_PUBLIC_GOOGLE_SITE_VERIFICATION=
NEXT_PUBLIC_BING_SITE_VERIFICATION=
NEXT_PUBLIC_SITE_URL=

# Analytics (Additional)
NEXT_PUBLIC_GA_MEASUREMENT_ID=
NEXT_PUBLIC_UMAMI_WEBSITE_ID=
NEXT_PUBLIC_VERCEL_ANALYTICS=

# Social Share / Open Graph
NEXT_PUBLIC_OG_IMAGE_API=
NEXT_PUBLIC_TWITTER_HANDLE=

# Contact Form / Email
RESEND_API_KEY=
EMAIL_TO=
EMAIL_FROM=

# WakaTime (Coding Stats)
WAKATIME_API_KEY=

# Blog / CMS
CONTENTFUL_SPACE_ID=
CONTENTFUL_ACCESS_TOKEN=

# Guestbook
DATABASE_URL=

# Newsletter (reuses RESEND_API_KEY above)
RESEND_AUDIENCE_ID=

# Security & Performance
UPSTASH_REDIS_REST_URL=
UPSTASH_REDIS_REST_TOKEN=
CRON_SECRET=
REVALIDATE_SECRET=
NEXT_PUBLIC_IMAGE_DOMAINS=

# Cookie Consent / GDPR
NEXT_PUBLIC_COOKIEYES_ID=

# Maintenance Mode
NEXT_PUBLIC_MAINTENANCE_MODE=

# Resume / CV
NEXT_PUBLIC_RESUME_URL=

# Environment
NEXT_PUBLIC_ENV=
```
