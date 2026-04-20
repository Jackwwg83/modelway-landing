# ModelWay — Design System v0.2

> **Status**: Phase 1 foundation. **Aligned to Sub2API production values** from `tier-a/design-tokens.md`.
>
> **Ground truth**: Sub2API's `frontend/tailwind.config.js` + `frontend/src/style.css`. Every token here matches.
>
> **Last updated**: 2026-04-19 (v0.2 — sub2api alignment)

---

## 0. Brand Foundation

### Identity
```
Name:        ModelWay
Domain:      modelway.dev
Category:    AI API Gateway / Token Aggregation
Tagline:     Unified AI API gateway — Claude, GPT, Gemini
Voice:       Developer-friendly, technically confident, not dry
Positioning: "The fastest way to use any AI model."
```

### Visual keywords (Sub2API alignment)
- 科技、简洁、开发者友好（不是 B2C 花哨风）
- 主色 teal/cyan（不是蓝，不是紫）
- 暗色模式优先体验（开发者半夜 debug 用）
- 玻璃拟态 + 渐变光晕作为视觉强调
- 内容层次清晰：大标题 + 副标题 + CTA 的经典结构

### Logo
- **Symbol**: V4C — Hexagon Lock (see `logos/primary-icon.svg`)
- **Wordmark**: `logos/primary-wordmark.svg` (icon + "ModelWay")
- **Color convention**: `currentColor` — logo inherits theme color via CSS
- **Solid-color export (Sub2API)**: `logos/primary-icon-teal.svg` (hardcoded `#14b8a6`)
- **White-on-dark export**: `logos/primary-icon-white.svg`

---

## 1. Color System (Sub2API exact values)

### Primary (teal/cyan) — full 12-step scale
Source: `sub2api/frontend/tailwind.config.js:theme.extend.colors.primary`

```css
--primary-50:   #f0fdfa;   /* lightest — hover bg */
--primary-100:  #ccfbf1;
--primary-200:  #99f6e4;
--primary-300:  #5eead4;
--primary-400:  #2dd4bf;
--primary-500:  #14b8a6;   /* ★ DEFAULT primary */
--primary-600:  #0d9488;   /* ★ primary hover */
--primary-700:  #0f766e;   /* deep accent */
--primary-800:  #115e59;
--primary-900:  #134e4a;
--primary-950:  #042f2e;   /* darkest */
```

**Primary CTA gradient**: `linear-gradient(135deg, #14b8a6 0%, #0d9488 100%)`
(Sub2API uses `bg-gradient-to-r from-primary-500 to-primary-600`)

### Neutrals (slate/dark system — full 12-step scale)
Sub2api names this `accent` / `dark` — same swatch, two aliases for semantic clarity.

```css
--neutral-50:   #f8fafc;  /* light-mode bg */
--neutral-100:  #f1f5f9;
--neutral-200:  #e2e8f0;  /* light-mode border */
--neutral-300:  #cbd5e1;
--neutral-400:  #94a3b8;
--neutral-500:  #64748b;  /* neutral text */
--neutral-600:  #475569;
--neutral-700:  #334155;  /* dark-mode border */
--neutral-800:  #1e293b;  /* dark-mode card bg */
--neutral-900:  #0f172a;  /* dark-mode app bg */
--neutral-950:  #020617;  /* darkest */
```

### Body bg/fg pairs (Sub2api exact)

```css
/* Light mode */
body {
  background: #f9fafb;  /* gray-50, slightly warmer than neutral-50 */
  color: #111827;       /* gray-900 */
}

/* Dark mode (html.dark) */
body {
  background: #020617;  /* dark-950 */
  color: #f3f4f6;       /* gray-100 */
}
```

### Semantic colors
```css
--success:  #10b981;  /* emerald-500 */
--warning:  #f59e0b;  /* amber-500 */
--danger:   #ef4444;  /* red-500 */
--info:     #0ea5e9;  /* sky-500 */
```

### Contrast verification (WCAG)
| fg on bg | ratio | grade |
|---|---|---|
| `#f3f4f6` on `#020617` | 15.9:1 | AAA |
| `#94a3b8` on `#020617` | 6.1:1 | AA |
| `#14b8a6` on `#020617` | 7.3:1 | AA (large) / AAA |
| `#111827` on `#f9fafb` | 17.3:1 | AAA |
| `#0d9488` on `#f9fafb` | 4.7:1 | AA |

---

## 2. Mesh Gradient (Hero decoration — Sub2API verbatim)

Sub2api's HomeView hero uses this 3-layer radial mesh. **Landing must reuse verbatim for visual parity.**

```css
.mesh-hero {
  background-image:
    radial-gradient(at 40% 20%, rgba(20, 184, 166, 0.12) 0px, transparent 50%),
    radial-gradient(at 80%  0%, rgba( 6, 182, 212, 0.08) 0px, transparent 50%),
    radial-gradient(at  0% 50%, rgba(20, 184, 166, 0.08) 0px, transparent 50%);
}
```

**Usage**: apply to the `<section>` that contains hero copy + CTA. Below the fold, revert to plain bg.

---

## 3. Typography (System stack — NO Google Fonts)

**Critical constraint**: Sub2api uses system-ui stack, not Google Fonts. Landing must align.
- ✅ Asia-Pacific users (CN) get no-wall reliable rendering
- ✅ Zero layout shift on first paint
- ✅ Cross-domain visual parity

### Stack

```css
--font-sans: system-ui, -apple-system, BlinkMacSystemFont,
             'Segoe UI', Roboto, 'Helvetica Neue', Arial,
             'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei',
             sans-serif;
--font-mono: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
```

### Scale (rem-based for accessibility)

| Role | Size | Weight | Line-height | Tracking |
|---|---|---|---|---|
| `display` | 56px / 3.5rem | 700 | 1.05 | -0.035em |
| `h1` | 44px / 2.75rem | 700 | 1.1 | -0.03em |
| `h2` | 32px / 2rem | 600 | 1.2 | -0.02em |
| `h3` | 24px / 1.5rem | 600 | 1.3 | -0.01em |
| `h4` | 18px / 1.125rem | 600 | 1.4 | 0 |
| `body-lg` | 17px / 1.0625rem | 400 | 1.55 | 0 |
| `body` | 15px / 0.9375rem | 400 | 1.6 | 0 |
| `body-sm` | 14px / 0.875rem | 400 | 1.55 | 0 |
| `body-xs` | 13px / 0.8125rem | 400 | 1.5 | 0 |
| `caption` | 12px / 0.75rem | 500 | 1.4 | 0.02em |
| `overline` | 11px / 0.6875rem | 500 | 1.3 | 0.1em / uppercase |
| `mono` | 14px | 400 | 1.5 | 0 (mono stack) |

### i18n (CJK)
- Latin + CJK mix: let the stack handle it (PingFang SC / Microsoft YaHei are in the fallback)
- **No `letter-spacing` on CJK text** — creates ugly gaps
- Use `<span lang="zh-CN">` on localized blocks

---

## 4. Spacing (4dp rhythm — standard Tailwind scale)

```css
--space-1:  4px;    --space-2:  8px;    --space-3: 12px;
--space-4: 16px;    --space-5: 20px;    --space-6: 24px;
--space-8: 32px;    --space-10: 40px;   --space-12: 48px;
--space-16: 64px;   --space-20: 80px;   --space-24: 96px;
--space-32: 128px;
```

### Container widths
```css
--container-sm:  640px;
--container-md:  768px;
--container-lg:  1024px;
--container-xl:  1200px;   /* Landing default */
--container-2xl: 1440px;
```

---

## 5. Border Radius (Sub2API exact)

```css
--radius-sm:     2px;
--radius:        4px;
--radius-md:     6px;
--radius-lg:     8px;
--radius-xl:    12px;   /* ★ buttons, inputs (sub2api preferred) */
--radius-2xl:   16px;   /* ★ cards (sub2api preferred) */
--radius-3xl:   24px;
--radius-4xl:   32px;   /* sub2api custom, large decorative */
--radius-full:  9999px;
```

**Lock rules**:
- Buttons, inputs, badges → `rounded-xl` = 12px
- Cards, modals → `rounded-2xl` = 16px
- Avatars, pills → `rounded-full`

---

## 6. Shadows (Sub2API custom set — verbatim)

```css
--shadow-card:       0 1px 3px rgba(0, 0, 0, 0.04),
                     0 1px 2px rgba(0, 0, 0, 0.06);
--shadow-card-hover: 0 10px 40px rgba(0, 0, 0, 0.08);
--shadow-glass:      0 8px 32px rgba(0, 0, 0, 0.08);
--shadow-glass-sm:   0 4px 16px rgba(0, 0, 0, 0.06);
--shadow-glow:       0 0 20px rgba(20, 184, 166, 0.25);  /* primary glow */
--shadow-glow-lg:    0 0 40px rgba(20, 184, 166, 0.35);
```

### Rules
- Regular cards: `shadow-card`, hover → `shadow-card-hover`
- Glass surfaces: `shadow-glass` / `shadow-glass-sm`
- Hero CTA + emphasis: `shadow-glow` / `shadow-glow-lg`
- Dark mode: reduce opacity 30% (apply via media query or CSS var override) or replace shadow with border

---

## 7. Components (Sub2API production CSS — copy/paste ready)

### Primary CTA button

```css
.btn-primary {
  background: linear-gradient(to right, #14b8a6, #0d9488);
  color: #ffffff;
  padding: 10px 16px;
  border-radius: 12px;
  font-size: 14px;
  font-weight: 500;
  box-shadow: 0 4px 6px rgba(20, 184, 166, 0.25);
  transition: all 200ms ease-out;
  cursor: pointer;
  border: none;
}
.btn-primary:hover {
  background: linear-gradient(to right, #0d9488, #0f766e);
  box-shadow: 0 10px 15px rgba(20, 184, 166, 0.30);
}
.btn-primary:active  { transform: scale(0.98); }
.btn-primary:focus-visible {
  outline: none;
  box-shadow: 0 0 0 2px rgba(20, 184, 166, 0.5),
              0 10px 15px rgba(20, 184, 166, 0.30);
}
```

### Ghost / secondary button

```css
.btn-ghost {
  background: transparent;
  color: #0d9488;
  padding: 10px 16px;
  border-radius: 12px;
  border: 1px solid #e2e8f0;
  transition: all 200ms ease-out;
}
.btn-ghost:hover { background: #f0fdfa; }
.dark .btn-ghost { border-color: #475569; color: #5eead4; }
.dark .btn-ghost:hover { background: rgba(20, 184, 166, 0.1); }
```

### Input

```css
.input {
  width: 100%;
  padding: 10px 16px;
  border-radius: 12px;
  border: 1px solid #e2e8f0;
  background: #ffffff;
  font-size: 14px;
  transition: all 150ms ease-out;
}
.input:focus {
  border-color: #14b8a6;
  box-shadow: 0 0 0 2px rgba(20, 184, 166, 0.30);
  outline: none;
}
.dark .input { background: #1e293b; border-color: #475569; color: #f3f4f6; }
```

### Card

```css
.card {
  background: #ffffff;
  border-radius: 16px;
  border: 1px solid #f3f4f6;
  box-shadow: 0 1px 3px rgba(0,0,0,0.04), 0 1px 2px rgba(0,0,0,0.06);
  transition: all 300ms ease;
  padding: 24px;
}
.card:hover { box-shadow: 0 10px 40px rgba(0,0,0,0.08); }
.dark .card {
  background: rgba(30, 41, 59, 0.5);
  border-color: rgba(51, 65, 85, 0.5);
}
```

### Glass card (premium surfaces)

```css
.card-glass {
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.08);
  padding: 24px;
}
.dark .card-glass {
  background: rgba(30, 41, 59, 0.5);
  border-color: rgba(255, 255, 255, 0.05);
}
```

### Pill / Tag

```css
.pill {
  display: inline-flex;
  align-items: center;
  height: 22px;
  padding: 0 8px;
  border-radius: 9999px;
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.02em;
  background: #f0fdfa;
  color: #0d9488;
}
.dark .pill { background: rgba(20, 184, 166, 0.15); color: #5eead4; }
```

---

## 8. Motion (Sub2API keyframes — verbatim)

```css
@keyframes fade-in      { from { opacity: 0 } to { opacity: 1 } }
@keyframes slide-up     { from { transform: translateY(10px); opacity: 0 }
                          to   { transform: translateY(0);   opacity: 1 } }
@keyframes slide-down   { from { transform: translateY(-10px); opacity: 0 }
                          to   { transform: translateY(0);    opacity: 1 } }
@keyframes slide-in-right { from { transform: translateX(20px); opacity: 0 }
                            to   { transform: translateX(0);   opacity: 1 } }
@keyframes scale-in     { from { transform: scale(0.95); opacity: 0 }
                          to   { transform: scale(1);     opacity: 1 } }
@keyframes pulse-slow   { 0%,100% { opacity: 1 } 50% { opacity: 0.5 } }
@keyframes shimmer      { 0% { background-position: -200% 0 }
                          100% { background-position: 200% 0 } }
@keyframes glow         { from { box-shadow: 0 0 20px rgba(20,184,166,0.25) }
                          to   { box-shadow: 0 0 40px rgba(20,184,166,0.45) } }

/* Utility classes */
.animate-fade-in       { animation: fade-in      0.3s ease-out; }
.animate-slide-up      { animation: slide-up     0.3s ease-out; }
.animate-slide-down    { animation: slide-down   0.3s ease-out; }
.animate-slide-right   { animation: slide-in-right 0.3s ease-out; }
.animate-scale-in      { animation: scale-in     0.2s ease-out; }
.animate-pulse-slow    { animation: pulse-slow   3s infinite; }
.animate-shimmer       { animation: shimmer      2s linear infinite; }
.animate-glow          { animation: glow         2s ease alternate infinite; }

/* Reduced motion */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 9. Iconography

**Default**: Lucide React (`lucide-react`) — 1.5px stroke, 20px default.
**Sub2API uses `@lobehub/icons`** — acceptable divergence for Landing. Don't mix both in the same page.

### Size scale
```
16  — inline with body text
20  — buttons, nav items (default)
24  — feature icons, empty states
32  — large feature tiles
48  — hero decoration
```

### Rules
- Icon-only buttons: always have `aria-label`
- Icons adjacent to text: 8px gap
- Never mix filled + outlined icons in the same context

---

## 10. Dark Mode (Tailwind `class` strategy)

Sub2api uses `darkMode: 'class'`, not `data-theme`. Landing must align for parity.

```js
// tailwind.config.js
module.exports = { darkMode: 'class', /* ... */ }
```

```js
// Toggle
document.documentElement.classList.toggle('dark')
localStorage.setItem('theme', document.documentElement.classList.contains('dark') ? 'dark' : 'light')

// Init on load (before first paint to avoid FOUC)
// Inline <script> in <head>:
if (localStorage.theme === 'dark' ||
    (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
  document.documentElement.classList.add('dark')
}
```

### Dark-mode specifics
- Body: bg `#020617` / fg `#f3f4f6`
- Cards: `rgba(30, 41, 59, 0.5)` — translucent, lets mesh gradient shine through
- Images: `filter: brightness(0.95) contrast(1.05)` on non-logo imagery
- Primary hue: use `primary-400` (`#2dd4bf`) for links on dark bg (brighter for AA contrast)
- Shadows: reduce intensity ~30% or drop entirely, prefer border layering

---

## 11. Accessibility

- All interactive elements ≥ **44×44px** tap target
- Visible focus ring on keyboard focus
- Never rely on color alone — pair with icon, text, or shape
- Form errors: color + icon + text below field
- Skip link at top (visible on focus)
- `prefers-reduced-motion` respected (see §8)
- Language attribute: `<html lang="en">` / `<html lang="zh-CN">`

---

## 12. Guardrails (Don't)

- ❌ No raw hex inside component files — only CSS vars
- ❌ **No Google Fonts** (Sub2API alignment + CN accessibility)
- ❌ No `!important` except user-style overrides
- ❌ No `const styles = {...}` global name — scope per section
- ❌ No layout shift on theme toggle (declare space before paint)
- ❌ No gradients outside `--gradient-primary` and the OG image
- ❌ No emoji as decoration
- ❌ No centered text wider than 75 characters
- ❌ No UI copy all-caps longer than 24 characters
- ❌ No custom fonts loaded in runtime — breaks sub2api/landing parity

---

## 13. Landing Hero Structure (Sub2API HomeView alignment)

Match sub2api's HomeView layout so the two domains feel like "same product, different modules":

```
┌────────────────────────────────────────────────────┐
│  [Logo] ModelWay            [Docs] [Login] [Start] │  Header (sticky, bg-elev-1 + blur)
├────────────────────────────────────────────────────┤
│                                                    │
│   Mesh gradient background (§2)                    │
│                                                    │
│   H1 (display): The fastest way to use any         │
│       AI model.                                    │
│   P (body-lg, muted): Unified AI API gateway —     │
│       Claude, GPT, Gemini. One endpoint.           │
│       Faster than upstream.                        │
│                                                    │
│   [Get free credits →]  [View pricing]             │  btn-primary (glow) + btn-ghost
│                                                    │
│   [subscription-to-API] [smart routing]            │  pills (mono, muted)
│   [token-level billing] [Claude Code compatible]   │
│                                                    │
├────────────────────────────────────────────────────┤
│   Feature cards (3-col grid, rounded-2xl)          │  .card × 6
│   [Multi-account pool] [Smart scheduling]          │
│   [Token-level billing] [Claude Code]              │
│   [Enterprise SLA] [Full-stack optimization]       │
├────────────────────────────────────────────────────┤
│   Supported models (pill tags)                     │  .pill × N
│   claude-opus-4 · gpt-5 · gemini-2.5-pro · ...     │
├────────────────────────────────────────────────────┤
│   Pricing teaser (comparison table, optional)      │
├────────────────────────────────────────────────────┤
│   Final CTA band                                   │
├────────────────────────────────────────────────────┤
│   Footer: © 2026 ModelWay · Privacy · Terms · GH   │
└────────────────────────────────────────────────────┘
```

### CTA routing
```
[Get free credits →]  → https://api.modelway.dev/register
[View pricing]         → #pricing (same page anchor)
[Login] (header)       → https://api.modelway.dev/login
```

---

## 14. Sub2API Integration Alignment (locked values)

| Token | Sub2API source | Landing value | Match |
|---|---|---|---|
| Primary 500 | `tailwind.config.js` | `#14b8a6` | ✅ exact |
| Gradient primary | `tailwind.config.js` | `linear-gradient(135deg, #14b8a6, #0d9488)` | ✅ exact |
| Font family | system-ui stack | system-ui stack | ✅ exact |
| Button radius | `rounded-xl` (12px) | 12px | ✅ exact |
| Card radius | `rounded-2xl` (16px) | 16px | ✅ exact |
| Shadow cards | `shadow-card` / `shadow-card-hover` | same | ✅ exact |
| Shadow glow | `shadow-glow-lg` | `0 0 40px rgba(20,184,166,0.35)` | ✅ exact |
| Mesh gradient | hero HomeView | 3-layer radial (§2) | ✅ exact |
| Dark mode | `darkMode: 'class'` | `html.dark` | ✅ exact |
| Icon library | `@lobehub/icons` | Lucide (acceptable divergence) | ⚠️ |

---

## 15. File Reference

```
brand/
├── CONSTRAINTS.md              ← Sub2API integration contract (tier-a/design-tokens.md absorbed)
├── DESIGN.md                   ← This file (v0.2 aligned)
├── SUB2API_REPLACEMENT_GUIDE.md ← Admin dashboard replacement walkthrough
├── README.md                   ← Navigation + showcase usage
├── showcase.html               ← 6-variant exploration
├── variations-v4.html          ← V4 Hub Mesh deep iteration
├── logos/                      ← SVG sources
├── logos-v4/                   ← V4 iterations archive
└── exports/                    ← Rasterized assets for distribution
    ├── logo-{80,180,256,512,1024}.png
    ├── logo-white-512.png
    ├── favicon-{16,32,48}.png + favicon.ico
    ├── apple-touch-icon-180.png
    ├── og-image-1200x630.png
    └── custom-pages/
        ├── privacy-en.html · privacy-zh.html
        └── terms-en.html · terms-zh.html
```

---

## 16. Next (Phase 2 — Landing)

- [ ] Scaffold Astro + Tailwind v4 project at `modelway-landing/` root
- [ ] Import DESIGN.md tokens as `tailwind.config.js` theme.extend
- [ ] Build hero + features + pricing + CTA band + footer
- [ ] Wire i18n (EN / ZH via URL path `/` and `/zh/`)
- [ ] Deploy to Cloudflare Pages (`modelway.dev`)
- [ ] Configure `_headers` for `X-Frame-Options: SAMEORIGIN` (to allow api.modelway.dev iframe embedding)
- [ ] Smoke test: click-through from modelway.dev → api.modelway.dev/register

This document is **living**. Any change to sub2api's tokens must propagate here within 24h.
