# MediaPlace Relaunch Page — Handoff

This folder (`relaunch/`) is the complete, self-contained relaunch sales page (the "$47, now with AI editing, 24-hour" page).

## What it is
- **One static HTML file** (`index.html`) + an **`assets/`** folder of images. That's it.
- No build step, no framework, no server, no database. Plain HTML/CSS/JS.
- All image paths are **relative**, so the page works from any location as long as `index.html` and the `assets/` folder stay together.
- Fonts load from Google Fonts over the internet (no action needed).

## Deploy (3 steps)
1. **Get the folder.** Pull/clone `Launch-Partner/mediaplace-pbs-preview` (branch `main`) and take the `relaunch/` folder — or just download that folder.
2. **Upload it** to wherever the relaunch page should live on MediaPlace (any static host, CDN, or your platform). Keep `assets/` in the **same directory** as `index.html`. The page is then live as-is.
3. **Wire the buttons.** The "Unlock for $47" / checkout buttons currently link to placeholders. Point them at the real Stripe / Rapture checkout (search `index.html` for the CTA links). The bump/OTO/downsell flow is yours to connect.

## Notes
- The 24-hour countdown ends **12:00 PM US Eastern, Fri Jun 19 2026**. To change it, edit the one line near the bottom of `index.html`: `var end=Date.UTC(2026,5,19,16,0,0);` (UTC time — 16:00 UTC = 12:00 ET). When it hits zero the countdown bar hides itself.
- Everything is in this one folder — nothing references the preview repo, so you can host it anywhere independently.
