# RACCOOL Interactive — company website

One static page: `index.html` + `assets/`. No build step, no server code, no framework.

## Files

| Path | What |
|---|---|
| `index.html` | The whole site — HTML, CSS and the three.js card hero in one file |
| `assets/card-pyrodon.jpg` | Card face used by the 3D hero (perspective-corrected from the desk render) |
| `assets/desk.jpg`, `office.jpg`, `hearing.jpg` | Gallery images (concept renders) |
| `assets/foil.jpg`, `two-angles.jpg`, `capsule.jpg` | Spare images; `capsule.jpg` is the social-share preview (`og:image`) |
| `assets/raccool-*.svg` | Logo mark and lockup (dark-bone variants are the ones in use) |

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

## Before you publish — things still marked TODO

Search `index.html` for `data-todo`. Two links are placeholders (`href="#"`, drawn with a dashed
outline so they are easy to spot):

- **Wishlist on Steam** (hero button and footer) → the Steam store page URL once the
  Coming Soon page is live.
- **Discord** (footer) → the invite link.

Remove the `data-todo` attribute when you fill in a real URL and the dashed outline disappears.

## Editing text

All copy is plain HTML in `index.html`, top to bottom in page order:

- Hero title / subtitle: the `<h1>` inside `#hero`
- Pitch paragraphs and the three pillars: `<section id="game">`
- Gallery captions: `<figcaption>` inside `<section id="look">`
- Studio blurb, team cards, the three facts: `<section id="studio">`
- Email, links, copyright: `<footer>`

Keep the wording in industry-standard terms (vertical slice, playtest, demo). Do not add
internal document names or numbers.

## Editing images

- Replace a gallery image by overwriting the file in `assets/` with the same name, 1600 px wide,
  JPEG quality ~85. Keep each under ~450 KB.
- **When real in-game screenshots exist**, swap them in for the concept renders and change the
  caption under the gallery (`.note`) so it no longer says "concept renders".
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
