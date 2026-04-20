# ModelWay Landing — Deployment Guide

> Deploy `modelway.dev` on **Cloudflare Pages** via Git push.

---

## One-time setup (10 min)

### 1. Put this directory under Git

```bash
cd /Users/jackwu/modelway-landing
git init
git add .
git commit -m "chore: initial modelway landing page"
# Push to GitHub / GitLab
git remote add origin git@github.com:<your-user>/modelway-landing.git
git branch -M main
git push -u origin main
```

### 2. Create a Cloudflare Pages project

1. Go to https://dash.cloudflare.com/ → **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**
2. Select the `modelway-landing` repo
3. Build settings:
   ```
   Framework preset:    None
   Build command:       (leave empty)
   Build output dir:    /
   Root directory:      /
   Environment:         Production
   ```
4. Save & Deploy — first build should succeed in under 30 s

### 3. Attach custom domain

In Pages project → **Custom domains** → **Set up a custom domain**:
- Add `modelway.dev`
- Add `www.modelway.dev`

Cloudflare automatically provisions TLS certificates and routes DNS (if modelway.dev is on Cloudflare DNS).

### 4. Verify

After DNS propagates:
- https://modelway.dev → Landing loads
- https://www.modelway.dev → redirects or mirrors
- `curl -I https://modelway.dev` → check headers match `_headers` file

### 5. Link Sub2API

In `api.modelway.dev/admin` → Settings → Homepage → `home_content`:

```
https://modelway.dev
```

Sub2API will iframe-embed the Landing at `api.modelway.dev/home`. Our `_headers` file already allows this via `Content-Security-Policy: frame-ancestors 'self' https://api.modelway.dev`.

---

## Per-commit deploys

After setup, any `git push` to `main` auto-deploys. Preview deploys are generated for PRs.

```bash
# Edit index.html
vim index.html

# Ship
git add index.html
git commit -m "feat: update hero copy"
git push
# → New production build starts within seconds
```

---

## File structure (what CF Pages serves)

```
modelway-landing/
├── index.html           ← Main landing page (single file, ~1000 lines)
├── _headers             ← CF Pages response headers (CSP, caching, HSTS)
├── robots.txt           ← SEO
├── sitemap.xml          ← SEO
├── favicon.ico          ← /favicon.ico
├── favicon-32.png       ← /favicon-32.png
├── apple-touch-icon.png ← iOS home screen icon
├── og-image.png         ← Social sharing (1200×630)
├── logo.svg             ← Teal brand icon (for hot-link)
├── logo-white.svg       ← White-on-dark variant
└── brand/               ← Source assets + design docs (excluded via robots.txt)
```

The `brand/` directory is in the repo for history but crawlers skip it. If you want to also exclude it from CF Pages serving entirely, add `brand/*` to `.cfignore` or delete the directory before pushing.

---

## Health checks after deploy

- [ ] `https://modelway.dev` loads under 1 s (first paint)
- [ ] Dark / Light toggle works + persists across reload
- [ ] 中/EN toggle works + persists across reload
- [ ] All CTA links point to `https://api.modelway.dev/...`
- [ ] Terminal animation cycles through 3 demos
- [ ] Mobile menu opens on narrow screens
- [ ] `curl -I https://modelway.dev` shows `Content-Security-Policy: frame-ancestors 'self' https://api.modelway.dev ...`
- [ ] Embed test: `api.modelway.dev/home` displays Landing in iframe (after setting `home_content` in admin)
- [ ] `View source` → no reference to Google Fonts / external CDNs

---

## Rollback

Cloudflare Pages keeps every deploy. Dashboard → **Deployments** → select any previous deployment → **Roll back to this deployment**.

---

## Performance targets (to verify in DevTools Lighthouse)

- Performance: 95+
- Accessibility: 95+
- SEO: 95+
- Best Practices: 95+
- LCP < 1.2s
- CLS < 0.05
- No render-blocking external resources (we have none)

If any of these regress, check:
- Terminal animation painting — if it causes CLS, defer it
- Mesh gradient size — shrink radial radii if paint is slow
- Images missing explicit width/height — add them

---

## Next: alternate landings / A/B

For a second variant, duplicate `index.html` → `index-b.html` and configure CF Pages Functions or Rules to route % traffic. Not needed for v1.
