# MediaPlace — AI Personal Brand Studio funnel (deploy guide)

Copy/paste-ready sales pages for the AI Personal Brand Studio launch. Every page is a single self-contained HTML file. All assets are absolute WebP URLs served from this repo via GitHub Pages, so you can paste the HTML into Rapture (or anywhere) and nothing breaks.

**Live preview:** https://launch-partner.github.io/mediaplace-pbs-preview/

## Pages

| File | Role | Price | Live URL |
|---|---|---|---|
| `index.html` | Front end | $47 | …/index.html |
| `oto1.html` | Upsell 1 — "The 1,000 Bundle" (1,000+ templates + 1,500 credits) | $67 | …/oto1.html |
| `downsell.html` | Downsell — template library only, no credits (fires on OTO1 decline) | $47 | …/downsell.html |
| `bump.html` | Order-bump reference (+500 credits) | $27 | …/bump.html |
| `thank-you-base.html` | Confirmation — declined upsell + downsell | — | …/thank-you-base.html |
| `thank-you-upsell.html` | Confirmation — took the 1,000 Bundle | — | …/thank-you-upsell.html |
| `thank-you-downsell.html` | Confirmation — took the downsell | — | …/thank-you-downsell.html |

## What to wire (the only thing left to do)

**1. Checkout CTAs.** Point every CTA `href="#"` to your Rapture endpoint:
- `index.html` — `YES! Unlock the Studio for $47` buttons (hero, offer banner, value stack) + topbar `Unlock for $47` + `#pricing` anchors → FE checkout.
- `oto1.html` / `downsell.html` — `YES! Add to my order ($67/$47)` buttons → one-click upsell/downsell endpoint (charges the saved card).
- Thank-you pages — `Open MediaPlace` button → the app.

**2. Decline routing.**
- `oto1.html` "No thanks, I will pass on the bundle" → already links to `downsell.html`.
- `downsell.html` "No thanks…" links → already point to `thank-you-base.html`.
- The hero CTA on the downsell has no decline by design; every other CTA does.

**3. Countdowns (already coded, just confirm the date).**
- FE: fixed end timestamp in the inline `<script>` — **Sat Jun 13 2026 14:00 UTC** (10am ET + 72h). Auto-hides when expired. Move the date if launch shifts.
- OTO1 + downsell: **20-minute** session timer from page open (localStorage), also auto-hides on expiry. (Timers never freeze at 00:00.)

## Swapping in real assets later

All images live in `assets/` (and `assets/cat/`). To swap one, keep the **exact same filename**, drop the new file in, and push — every page updates automatically, zero HTML changes. Keep new files **WebP, optimized** (resize + q85-90) to preserve load speed.

- Hero: `assets/hero-showcase.webp`. Credit box-shots: `assets/creditbox.webp` ($47), `assets/creditbox67.webp` ($67).
- FE category tiles: `assets/cat/{profile,banners,thumbnails,quotes,cards,zoom,social,fun,ads}.webp`.
- OTO/downsell category tiles: `assets/cat/oto-{photoshoot,cards,banners,ads,thumbnails,quotes,stories,callbg,mockups}.webp` + `assets/oto-bundle-collage.webp` + `assets/oto-fiverr.webp`.
- How-it-works + feature screenshots: `assets/{step1,step2,step3,feat1,feat2,feat3}.webp`.
- Favicon + logo: `assets/favicon.png`, `assets/mediaplace-logo.svg`.

## Quality bar (verified)

- Mobile-clean: zero horizontal overflow at 360 / 768 / 1280; every image loads.
- Light + fast: each page ≈ 1.4–1.6 MB, all images lazy-loaded below the fold, heaviest single asset 227 KB.
- All branding is MediaPlace (Lexend, magenta→pink). No em-dashes, identical CTA copy per page.
