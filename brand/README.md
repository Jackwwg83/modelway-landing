# ModelWay — Brand Package

**Status**: Phase 0 ✅ · Phase 1 ✅ · Phase 2+ (Sub2API replacement) ✅ · Phase 2 (Landing) ⏳

---

## 🎯 Quick Links — What you need right now

### Ready to ship (copy-paste to Sub2API admin)
```
exports/logo-80.png              ← Sub2API Settings · Logo
exports/logo-256.png             ← Higher-res fallback
exports/favicon-32.png           ← Sub2API Settings · Favicon
exports/favicon.ico              ← Multi-size fallback
exports/apple-touch-icon-180.png ← Optional, iOS
exports/custom-pages/privacy-en.html  ← Settings · Custom Pages · /custom/privacy
exports/custom-pages/privacy-zh.html  ← /custom/privacy-zh
exports/custom-pages/terms-en.html    ← /custom/terms
exports/custom-pages/terms-zh.html    ← /custom/terms-zh
```

### Step-by-step guides
- **`SUB2API_REPLACEMENT_GUIDE.md`** → 10-15 min walkthrough to replace Sub2API branding
- **`CONSTRAINTS.md`** → Technical constraints from Sub2API (locked decisions)
- **`DESIGN.md`** → Full design system (color, typography, components)

---

## 📂 Directory map

```
brand/
├── README.md                      ← This file (nav)
├── CONSTRAINTS.md                 ← Sub2API integration constraints + locked decisions
├── DESIGN.md                      ← Full design system v0.1
├── SUB2API_REPLACEMENT_GUIDE.md   ← Admin dashboard replacement walkthrough
│
├── showcase.html                  ← Interactive 6-variant exploration (port 8765)
├── variations-v4.html             ← V4 Hub Mesh deep iteration
│
├── logos/
│   ├── primary-icon.svg           ← ⭐ CANONICAL Logo (currentColor, V4C)
│   ├── primary-icon-teal.svg      ← Hardcoded #14b8a6 (for raster export)
│   ├── primary-icon-white.svg     ← White on dark
│   ├── primary-wordmark.svg       ← Icon + "ModelWay" horizontal
│   ├── primary-wordmark-domain.svg ← Icon + "ModelWay.dev"
│   ├── favicon.svg                ← Favicon SVG
│   ├── og-image.svg               ← Social share (1200×630)
│   └── 0[1-6]-*.svg               ← Archive: original 6 variants
│
├── logos-v4/                      ← Archive: V4 iterations (A/B/C/D)
│
└── exports/
    ├── logo-80.png                ← ⭐ Sub2API Logo upload
    ├── logo-180.png
    ├── logo-256.png
    ├── logo-512.png
    ├── logo-1024.png
    ├── logo-white-512.png
    ├── favicon-16.png
    ├── favicon-32.png             ← ⭐ Sub2API Favicon upload
    ├── favicon-48.png
    ├── favicon.ico                ← ⭐ Multi-size (.ico)
    ├── apple-touch-icon-180.png
    ├── og-image-1200x630.png      ← Social card
    └── custom-pages/
        ├── privacy-en.html
        ├── privacy-zh.html
        ├── terms-en.html
        └── terms-zh.html
```

---

## 🔒 Locked decisions (ground truth)

| Decision | Value | Source |
|---|---|---|
| Logo | V4C Hexagon Lock | User pick, 2026-04-19 |
| Primary color | `#14b8a6` (teal-500) | Align with `sub2api/frontend/tailwind.config.js` |
| Secondary (deep) | `#0d9488` (teal-600) | Same |
| Font | Inter + JetBrains Mono | Align with Sub2API |
| Deployment | Cloudflare Pages | `modelway.dev` + `www` |
| Dashboard | `api.modelway.dev` runs Sub2API (white-labeled) | Existing |

---

## 🖼 View the showcases

```bash
cd /Users/jackwu/modelway-landing/brand
python3 -m http.server 8765
```

Then open:
- http://localhost:8765/showcase.html — Original 6 variants
- http://localhost:8765/variations-v4.html — V4 deep iteration

---

## ⏭️ Next: Phase 2 — Landing Page

Waiting on user decisions (see CONSTRAINTS.md §8):
- Landing page copy drafts (English-first, user to finalize per prior commitment)
- Astro project scaffold decision (we'll start fresh or iterate in place)
- UI icon library (Lucide default, @lobehub/icons for Sub2API parity)
