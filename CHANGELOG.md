# Changelog — sdl.life

## [2026-10-02] Comprehensive domain-sales optimization

### I. Technical foundation
- Security + cache headers (`public/_headers`): HSTS, nosniff, DENY framing,
  strict Referrer/Permissions policy, CSP (free-plan compatible), immutable
  caching for css/js/fonts/images.
- SEO head overhaul (`BaseLayout`): canonical, robots max-image-preview,
  theme-color, preconnect/dns-prefetch/preload hero image, OG 1200×630 +
  Twitter large-image, manifest + icons.
- Structured data: Organization, WebSite, **Product/Offer** (price on request,
  serious offers from $25k), FAQPage, BreadcrumbList.
- Sitemap via `@astrojs/sitemap` now covers `/`, `/faq/`, `/valuation-guide/`;
  `robots.txt` points at `sitemap-index.xml`.

### II. SEO
- Title format: `sdl.life | Premium Domain for Sale | SDL Luxury Living Scottsdale`.
- Meta description with price/availability + CTA + UVP; domain-focused keywords.
- Single H1 (`sdl.life`), 8 semantic H2s, skip link, 50 ARIA hooks.
- Internal linking: portfolio, `/faq/`, `/valuation-guide/`, cross-domain links.

### III. CRO
- Above-the-fold price panel (Price on request / from $25k) + live viewer counter.
- Triple CTAs by tier: Buy Now / Make an Offer / Contact Agent (+ sticky mobile bar).
- Trust signals: Escrow.com, SSL/registrar-lock, transaction guarantee, 24–48h SLA.
- Urgency: 1-of-1 asset badge, weekly viewers, spots-left microcopy.
- Social proof: 3 testimonials + comparable-sales ticker ($18k–$75k).
- Real inquiry form → `POST /api/inquire` (Worker) with validation, honeypot,
  mailto fallback, success state, `data-track` analytics hooks.
- Exit-intent email capture → `POST /api/subscribe` (desktop mouse-out + 45s
  mobile fallback, 7-day frequency cap).

### IV. Mobile
- Hamburger menu, all interactive elements `min 48px` (54 tap-targets),
  16px base font, `viewport-fit=cover`, `overflow-x: clip`, no horizontal scroll.

### V. Authority content
- New `/faq/` (escrow steps, timelines, installments, bundles).
- New `/valuation-guide/` (scarcity, extension fit, Scottsdale affluence, comps,
  offer playbook) — weekly-blog ready.
- Portfolio section with live search + category filters (all/geo/beauty/brandable).

### VI. Design modernization
- Dark/light toggle (persisted, respects OS; dark default for hero brand).
- Scroll-reveal animations, card hover lifts, FAQ accordions, reduced-motion support.
- Visible focus rings (WCAG), custom 404 page.

### VII. Validation
- `astro build`: 4 pages, 0 errors. `wrangler deploy --dry-run`: 13 asset files,
  3.26 KiB, ASSETS binding OK (Workers free plan).
- H1×1 / H2×8, 0 duplicate IDs, 7 form labels, 7 mailto fallbacks.

### Deployment
- Worker `src/worker.ts`: `GET /api/health`, `POST /api/inquire`,
  `POST /api/subscribe`, CORS locked to `https://sdl.life`, `run_worker_first: [/api/*]`.
- Stays on Cloudflare Workers free plan (static assets + edge APIs, no paid bindings).
- Post-deploy: monitor errors/analytics 48h; submit updated sitemap in Google
  Search Console (manual step).
