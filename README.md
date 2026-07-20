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

# Environment
NEXT_PUBLIC_ENV=
```
