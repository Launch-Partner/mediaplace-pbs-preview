# MediaPlace — AI Personal Brand Studio Launch

Private launch workspace. Co-launch between **Dopamine Digital (Jordan)** and **Thomas Dolso (Maesto LLC / MediaPlace)** at **20% revshare to Jordan**. Jordan owns the funnel sales pages; Thomas owns the product + checkout (his "Rapture" platform, Stripe Connect for the split).

**Launch target:** Tuesday June 9 2026 (or Wed June 10).
**List:** ~4,000 existing MediaPlace customers (warm, somewhat saturated).

**FE sales page (live preview):** https://launch-partner.github.io/mediaplace-pbs-preview/
Source of the page is `docs/index.html` here. Pages can't serve from this private repo on the current plan, so the public preview lives in the page-only repo `Launch-Partner/mediaplace-pbs-preview` (no call notes or economics there). Final HTML gets handed to Thomas to embed in Rapture.

> Access: private, Jordan only. Filip and Angela are intentionally excluded.

## What this is

The **AI Personal Brand Studio** is a new tab inside MediaPlace. Upload one selfie and the "One-Shot Brand Engine" produces a full personal brand: profile photos, banners, quote graphics, business cards, Zoom backgrounds, social content, headshot ads, and YouTube thumbnails. No training step. A stock set generates automatically per brand kit; the rest are generated on demand with credits.

## The funnel (CONFIRMED — June credits-only model)

| Stage | Price | What they get | Guarantee |
|---|---|---|---|
| Front End | $47 | Unlock the Studio + unlimited brand kits + 750 credits (~250 assets, "valued at $47, free") + 100 templates + 4K + auto-crop + zip export + social autopull | 30-Day Money-Back |
| Order Bump | $27 | +500 credits (~150 more assets). Inline checkout checkbox, no VSL | — |
| OTO1 | $67 | 1,000 templates + 1,500 credits (~500 assets) | The 10x Promise |
| Downsell | $47 | 750 credits (~250 assets), no templates (fires only on OTO1 decline) | 30-Day Remorse |
| OTO2 | $97 | Agency Pack (commercial + resell rights, Agency-In-A-Box kit) | The Agency Promise |

See `context/funnel-spec.md` for the authoritative build spec.

## Repo map

```
README.md
context/
  funnel-spec.md                          # SINGLE SOURCE OF TRUTH for the pages
  google-doc-snapshot.md                  # verbatim source Google Doc (2026-06-08)
  call-log.md                             # every Thomas call + what changed
  funnel-spec-LOCKED-may13-SUPERSEDED.md  # old Seats spec, kept for the record (do not build from)
  funnel-spec-WIP-history.md              # pre-lock iteration history
  transcripts/
    2026-02-06-fathom.md                  # background / context
    2026-05-11-fathom.md                  # funnel designed, 20% revshare agreed
    2026-06-01-tldv.md                    # terminology + UX, FE video killed
    2026-06-02-tldv.md                    # PIVOT: seats removed, credits-only
pages/
  index.html                              # FE $47 sales page (live deliverable)
```

## Status (2026-06-08)

- Funnel structure confirmed (credits-only, above).
- Thomas building product + checkout pages, removing seats, sending any final credit/asset numbers.
- Jordan's task: build the sales pages around the confirmed numbers. **FE page first**, then OTO1 / downsell / OTO2 + VSL scripts + launch email sequence.


## Handover to Thomas

The FE sales page lives at `docs/index.html` (single self-contained file). Public preview: https://launch-partner.github.io/mediaplace-pbs-preview/

**Status: launch-ready.** All page images are REAL (Jordan's photos/assets), WebP-optimized, and live in the public preview repo. FE total image weight ~1.3MB (largest single asset `hero-showcase.webp` ~169KB) — fast, no lag. Every `src` resolves to a committed file (verified 200 live). FE + OTO1 are mobile-clean (no horizontal overflow at 360/390). Pages tagged `fe-final-v3` / `oto1-final-v3`.

**Wire these up (only thing left for Thomas):**
- Point every checkout CTA to the Rapture checkout URL. They are the `YES! Unlock the Studio for $47` buttons (hero, both offer banners, value stack) + the topbar `Unlock for $47` + the `#pricing` anchors. Search `index.html` for `href="#"` and `href="#pricing"`. OTO1/downsell CTAs (`YES! Add to my order`) point to the one-click upsell endpoint.
- Set the real launch end: the FE countdown end is the fixed timestamp in the inline `<script>` (Sat Jun 13 14:00 UTC = 10am ET + 72h); it auto-hides when expired. OTO/downsell use a 30-min session timer (also hides on expiry).

**Swapping in real assets later** (keep the exact same filenames/paths so nothing else changes — all WebP):
- Hero showcase: `docs/assets/hero-showcase.webp` (~1600px wide). Credit box-shot: `docs/assets/creditbox.webp` (transparent PNG-style, ~760px).
- 9 FE category tiles: `docs/assets/cat/{profile,banners,thumbnails,quotes,cards,zoom,social,fun,ads}.webp` (~1200×900). OTO1 also uses `cat/{photoshoot,mockups}.webp`.
- How-it-works + feature screenshots: `docs/assets/{step1,step2,step3,feat1,feat2,feat3}.webp` (~1000px wide).
- Keep new uploads WebP + optimized (resize + q85-90) to preserve load speed.

## Image hosting (so nothing breaks when you embed the pages)

All images are hosted in the **public** repo `Launch-Partner/mediaplace-pbs-preview`, served by GitHub Pages at a stable, permanent URL base:

```
https://launch-partner.github.io/mediaplace-pbs-preview/assets/...
```

- **The OTO1 page (`oto1.html`) references every asset by its full absolute URL**, so you can paste the HTML into Rapture (or anywhere) and the images, logo and favicon will always resolve. Nothing is relative, nothing breaks.
- **To swap in real images:** keep the exact same filenames, drop the new files into `assets/` (and `assets/cat/`) in the `mediaplace-pbs-preview` repo, and push. The URLs stay identical, so both the preview and your embedded page update automatically with zero HTML changes.
- The MediaPlace favicon (pulled from mediaplace.io) is at `assets/favicon.png` and is wired into both pages so the browser tab matches the MediaPlace homepage.
