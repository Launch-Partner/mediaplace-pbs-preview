# MediaPlace — AI Personal Brand Studio funnel (deploy guide)

Copy/paste-ready sales pages for the AI Personal Brand Studio launch. Every page is a single self-contained HTML file. All assets are absolute WebP URLs served from this repo via GitHub Pages, so you can paste the HTML into Rapture (or anywhere) and nothing breaks.

**Live preview:** https://launch-partner.github.io/mediaplace-pbs-preview/

## Pages

| File | Role | Price | Live URL |
|---|---|---|---|
| `index.html` | Front end | $47 | …/index.html |
| `oto1.html` | Upsell 1 — "The 1,000 Bundle" (1,000+ templates + 1,500 credits) | $67 | …/oto1.html |
| `downsell.html` | Downsell — template library only, no credits (fires on OTO1 decline) | $47 | …/downsell.html |
| `oto2.html` | Upsell 2 — 10,000 AI credits | $197 | …/oto2.html |
| `oto2-downsell.html` | Downsell — 5,000 AI credits (fires on OTO2 decline) | $97 | …/oto2-downsell.html |
| `bump.html` | Order-bump reference (+500 credits) | $27 | …/bump.html |
| `thank-you-base.html` | Owns **nothing extra** — offers Bundle $67 + 10k credits $197 | — | …/thank-you-base.html |
| `thank-you-credits-5k.html` | Owns **5,000 credits** — offers Bundle $67 | — | …/thank-you-credits-5k.html |
| `thank-you-credits-10k.html` | Owns **10,000 credits** — offers Bundle $67 | — | …/thank-you-credits-10k.html |
| `thank-you-library.html` | Owns the **$47 library (no credits)** — offers 10k credits $197 | — | …/thank-you-library.html |
| `thank-you-bundle.html` | Owns the **$67 bundle (with credits)** — offers 10k credits $197 | — | …/thank-you-bundle.html |
| `thank-you-all.html` | Owns **both upsells** — pure confirmation, no cards | — | …/thank-you-all.html |

Thank-you pages **only ever offer the two upsells** (Bundle $67 + 1,500 credits, 10k credits $197). Downsells are never re-offered. Owned/greyed cards name the exact product bought (library = "no AI credits", credits = the real amount).

## What to wire (the only thing left to do)

**1. Checkout CTAs.** Point every CTA `href="#"` to your Rapture endpoint:
- `index.html` — `YES! Unlock the Studio for $47` buttons (hero, offer banner, value stack) + topbar `Unlock for $47` + `#pricing` anchors → FE checkout.
- `oto1.html` / `downsell.html` — `YES! Add to my order ($67/$47)` buttons → one-click upsell/downsell endpoint (charges the saved card).
- Thank-you pages — `Open MediaPlace` button → the app.

**2. Decline routing (mid-funnel).**
- `oto1.html` "No thanks" → `downsell.html`. `oto2.html` "No thanks" → `oto2-downsell.html`.
- The hero CTA on the downsells has no decline by design; every other CTA does.

**2b. Thank-you routing (4 static pages, no logic — just point each funnel EXIT at the right URL).**
There are 5 plain thank-you pages, one per end-state. Each is a fixed URL with the correct cards baked in — nothing to detect, nothing that can misfire. The page a buyer lands on depends on **both** decisions (templates slot AND credits slot), so route by the combination below:

| Templates slot (OTO1 / DS1) | Credits slot (OTO2 / DS2) | Send them to |
|---|---|---|
| bought nothing | bought nothing | `thank-you-base.html` |
| bought nothing | bought the 5k | `thank-you-credits-5k.html` |
| bought nothing | bought the 10k | `thank-you-credits-10k.html` |
| bought the **$47 library** | bought nothing | `thank-you-library.html` |
| bought the **$67 bundle** | bought nothing | `thank-you-bundle.html` |
| bought either templates product | bought either credit pack | `thank-you-all.html` |

6 pages. The 5 with an offer name the exact product the buyer owns (library = "no AI credits", credit pack = the real 5k/10k amount, bundle = "with 1,500 credits") and only ever offer the two upsells. The 6th (`thank-you-all`) is a plain "your full order is in your account" confirmation with no product cards, covering all four "bought everything" combos.

Because the final step (OTO2/DS2) only knows the credits decision, the funnel must carry the templates decision through to pick the right page. Two clean ways in PayKickstart: (a) if a redirect URL can carry the cart/purchased products, branch on it; or (b) split the OTO2 step so the "bought templates" path and "skipped templates" path use separate OTO2 instances, each ending on its matching pair of thank-you pages. Pick whichever your funnel supports — happy to set this up with you.

The thank-you "Add to my order" buttons are `href="#"` — wire them to your Rapture one-click endpoint too.

**3. Countdowns (already coded, just confirm the date).**
- FE: fixed end timestamp in the inline `<script>` — **Sat Jun 13 2026 14:00 UTC** (10am ET + 72h). Auto-hides when expired. Move the date if launch shifts.
- OTO1 / downsell / OTO2 / oto2-downsell: **20-minute** session timer from page open (localStorage). Thank-you last-chance: **15-minute**. All auto-hide on expiry (timers never freeze at 00:00).

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
