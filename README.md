# ModelWay Landing

Static landing page for **modelway.dev** — unified AI API gateway for Claude / GPT / Gemini.

Single HTML file, no build step, no external dependencies. Deployed on Cloudflare Pages.

## Stack

- `index.html` — single-file landing, inline CSS + JS, bilingual (zh/en)
- `_headers` — Cloudflare Pages response headers (CSP, caching, HSTS)
- `robots.txt` / `sitemap.xml` — SEO
- `favicon.ico` / `favicon-32.png` / `apple-touch-icon.png` / `og-image.png` — site assets
- `logo.svg` / `logo-white.svg` — brand marks
- `legal/` — Privacy / Terms HTML fragments for Sub2API Custom Pages
- `brand/` — design system + logo sources (docs only, crawlers skip via `robots.txt`)

## Local preview

```bash
cd /Users/jackwu/modelway-landing
python3 -m http.server 8766
# open http://localhost:8766
```

## Deployment

Auto-deployed via **Cloudflare Pages** on push to `main`. See [`DEPLOY.md`](./DEPLOY.md) for one-time CF Pages setup.

## Integration with Sub2API

`api.modelway.dev` (Sub2API) iframe-embeds this landing at `/home` via the admin `home_content` field. Our `_headers` includes `Content-Security-Policy: frame-ancestors 'self' https://api.modelway.dev …` to allow it. See [`brand/SUB2API_REPLACEMENT_GUIDE.md`](./brand/SUB2API_REPLACEMENT_GUIDE.md) for the admin walkthrough (logo upload, favicon, custom pages, footer URLs).

## Brand

See [`brand/DESIGN.md`](./brand/DESIGN.md) for the full design system (colors, typography, spacing, components). Tokens are aligned with Sub2API for zero-cost cross-domain parity.
