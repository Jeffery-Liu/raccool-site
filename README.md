# RACCOOL Interactive — company website

One static page: `index.html` + `assets/`. No build step, no server code, no framework.

## Files

| Path | What |
|---|---|
| `index.html` | The whole site — HTML, CSS and the three.js card hero in one file |
| `assets/card-pyrodon.jpg` | Card face used by the 3D hero (perspective-corrected from the desk render) |
| `assets/desk.jpg`, `office.jpg` | Gallery concept art; `hearing.jpg` is retained as an unused historical asset |
| `assets/batch-review.png` | Current Unity batch-review screenshot; replaces the hearing image in the public gallery |
| `assets/foil.jpg`, `two-angles.jpg`, `capsule.jpg` | Spare images; `capsule.jpg` is the social-share preview (`og:image`) |
| `robots.txt`, `sitemap.xml` | Crawl rules and the URL list for search engines |
| `assets/raccool-*.svg` | Logo mark and lockup — the `-dark` files from `Logo/Final/files_polished/` (Palette 02); the SVGs in `Logo/Final/` root are superseded |

## Preview locally

WebGL will not load textures from a file opened by double-click (`file://`). Serve the folder over
HTTP instead:

```
cd "RACCOOL INTERACTIVE INC\Website\raccool-site"
python -m http.server 8765
```

Then open http://127.0.0.1:8765/ in Chrome. Stop the server with Ctrl+C.

## Go live on GitHub Pages (free, no domain needed)

1. Create a public GitHub repository named `raccool-site` under your own GitHub account (Jeffery-Liu is fine — the account name only shows in the free URL, and a custom domain hides it).
2. Upload the contents of this folder so that `index.html` sits at the repository root
   (not inside a sub-folder).
3. Repository **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*,
   Branch = `main`, Folder = `/ (root)` → Save.
4. After one to two minutes the site is at `https://<account>.github.io/raccool-site/`.
   That URL is fine to put in the Creative BC form.
5. Custom domain later: buy `raccool.com` or `raccool.ca` (~$15–20/yr), enter it on the same
   Pages settings page, and add the DNS records GitHub shows there. Tick *Enforce HTTPS* once it
   turns green.

Every later change is just: edit `index.html` → commit → the site updates itself.

## Domains and search

- `raccool.ca` is the only site. `CNAME` points GitHub Pages at it; DNS lives in Cloudflare
  (records are DNS-only, not proxied). Google Search Console is verified via a
  `google-site-verification` TXT record there — don't delete it.
- `raccoolinteractive.com` (Cloudflare Registrar) does not host anything: a Cloudflare Redirect Rule
  sends every URL on it, and on `www.`, to `https://raccool.ca/` with a 301.
- `robots.txt` and `sitemap.xml` are at the root. Update `<lastmod>` in `sitemap.xml` after a
  substantial content change.
- The `<head>` of `index.html` carries Organization / WebSite / VideoGame structured data (JSON-LD).
  Keep the Organization name, description, founder and location consistent with the visible studio
  introduction and team cards. Add each verified company profile to the Organization `sameAs`
  and the footer. Game store pages belong in the VideoGame `sameAs`, not the Organization.
  Confirm ownership before adding a profile; similarly named Raccoon companies are unrelated.
- Official profiles verified on October 21, 2026:
  - YouTube: https://www.youtube.com/@Raccool-Interactive
    (channel ID `UCuxtjspCJx5pyDCa6y53F9g`; its About text names RACCOOL INTERACTIVE INC. and SLABBED).
  - Discord: https://discord.gg/XxAbsrMjBB (SLABBED server).
  No LinkedIn company page has been provided.
- Steam game page verified on October 22, 2026:
  https://store.steampowered.com/app/5462900/SLABBED_Card_Grader/
  The public title is **SLABBED: Card Grader**; both developer and publisher are
  **RACCOOL Interactive Inc.** The hero wishlist button and footer Steam link point here.
  Keep the full game name consistent in the hero, studio copy, metadata and VideoGame data.
- Current gameplay trailer (verified October 23, 2026):
  https://www.youtube.com/watch?v=dsgODcNVBlY
  **SLABBED: Card Grader - Gameplay Trailer 1**, 80 seconds, on the official RACCOOL channel.
  The game section and gallery note link here; the VideoGame `trailer` data includes its public
  title, thumbnail, upload date and duration. Update all three when replacing the trailer.
  The footer YouTube link and Organization `sameAs` continue to identify the channel itself.
- `dc/` and `discord/` are `noindex` redirect pages; keep them out of the sitemap.
- `privacy/` is the privacy policy (linked from the footer, listed in the sitemap). If you add a
  service that receives visitor data (a form, newsletter, another analytics tool), update it.
- Visit stats: Cloudflare Web Analytics (cookieless). The beacon `<script>` sits just before
  `</body>` in `index.html` and `privacy/index.html`; add it to any new page.

## Editing text

All copy is plain HTML in `index.html`, top to bottom in page order:

- Hero title / subtitle: the `<h1>` inside `#hero`
- Pitch paragraphs and the three pillars: `<section id="game">`
- Gallery captions: `<figcaption>` inside `<section id="look">`
- Studio blurb, team cards, the three facts: `<section id="studio">`
- Email, links, copyright: `<footer>`

Keep public copy aligned with the latest approved application facts: the game is in production,
with surface inspection, batch review and sealing playable in the current build. Distinguish
features in development from the intended full game. Use both card-grading simulation and narrative
thriller, including multiple endings. Steam Deck compatibility remains a testing goal. Do not publish
fixed campaign days, antagonists, specific offers, twists or an ending list, including in captions,
alt text or metadata. Avoid obsolete prototype/vertical-slice milestone wording. Do not add internal
document names, budget details or funding-application commentary to public pages.

## Editing images

- Replace a gallery image by overwriting the file in `assets/` with the same name, 1600 px wide,
  JPEG quality ~85. Keep each under ~450 KB.
- Label each image accurately. The desk and office gallery images remain concept art;
  `batch-review.png` is an unaltered runtime screenshot from 23 October 2026. Keep the gallery note
  explicit about the mixed sources. Do not restore the hearing image: its binder reveals a fixed
  campaign length. Do not edit game UI to fabricate progress evidence.
- The hero card face is `assets/card-pyrodon.jpg` (640 × 896). To use a different card, export the
  card art straight-on at the same size and overwrite the file. If the new card has a baked-in
  scratch in a different place, update `SCRATCH_A` / `SCRATCH_B` (UV coordinates, 0–1, origin
  bottom-left) near the top of the `<script type="module">` block.

## How the card hero works (for whoever edits it later)

- `three.js` 0.160 is loaded from jsDelivr via an import map; nothing is bundled.
- The card is one plane with a custom shader: rounded-corner mask, paper + varnish lighting from a
  single fixed lamp (`LAMP`), a holographic band inside the art window, and a scratch that is a
  tiny tilted facet along a UV segment — it only lights up when the card's angle brings that facet
  into the lamp's reflection.
- The same scratch rule is evaluated again in plain JavaScript (`scratchGlint()`); when it fires,
  the "Surface flaw — hairline scratch" label appears. Screen and answer key use one formula.
- Pointer position drives the tilt (max ±24° / ±32°, matching the game). After 2.6 s with no
  input the card drifts on its own. `prefers-reduced-motion` gets a static tilt.
- Tuning knobs at the top of the module script: `LAMP` (moves where the glint happens),
  `SCRATCH_TILT` (how narrow the glint angle is), `MAX_X` / `MAX_Y` (tilt range).

## Brand

Colours from the brand guidelines: Charcoal `#131313`, Bone `#EDE4D6`, Taupe `#9B8E7E`,
Burnt Orange `#C96A24`, plus a warm lamp tint `#F0C98C`. Fonts (Google Fonts): Barlow Condensed
for display, Source Serif 4 for body, IBM Plex Mono for labels.
