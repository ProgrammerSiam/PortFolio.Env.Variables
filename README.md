# Environment Variables

This document describes every environment variable used in this project, grouped by module. Each entry includes the variable's **purpose**, **where it's used**, and **where to get the value**.

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

# Environment
NEXT_PUBLIC_ENV=
```
