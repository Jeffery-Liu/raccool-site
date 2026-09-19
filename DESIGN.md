# DESIGN.md — RACCOOL Interactive Inc.

Design system for anything that carries the RACCOOL name: website, store pages, decks, documents,
social posts, and the studio-level UI in our games. Coding agents: read this before generating or
editing any RACCOOL-branded surface. Source of truth for the logo is
`Logo/Final/RACCOOL-Brand-Guidelines-Final.pdf` (in the company folder, not this repo) (v1.0); this file restates it and adds the
digital layer the PDF does not cover.

## 1. Identity in one paragraph

RACCOOL makes games about looking closely. The name fuses RAC(coon) with COOL; the mark fuses a
raccoon's two most recognisable features — the eye mask and the ringed tail — into one closed ring.
The brand is grounded, quiet and precise: a desk lamp, not a neon sign. Nothing glows, nothing
bounces, nothing shouts. Confidence comes from specificity.

## 2. Colour

Two palettes, **paired to ground, never mixed**. This is the single most common mistake — the
guidelines say it "must be followed, not corrected".

### Palette 01 — Northern · light grounds (white / near-white)

| Token | Name | Hex | Use |
|---|---|---|---|
| `--ink` | Charcoal Black | `#131313` | mask, wordmark, primary text |
| `--fur` | Warm Gray | `#827B73` | tail band, secondary text, rules |
| `--accent` | Burnt Orange | `#C96A24` | the COOL in the wordmark, links, one CTA per view |

### Palette 02 — Albino · dark grounds (`#1A1A1A` and darker)

| Token | Name | Hex | Use |
|---|---|---|---|
| `--bone` | Bone White | `#EDE4D6` | coat, wordmark, primary text — warm, never pure white |
| `--taupe` | Taupe | `#9B8E7E` | tail band, secondary text, rules |
| `--accent` | Albino Rose | `#B5786C` | the COOL in the wordmark, links, one CTA per view |

### Palette 03 — Blackout · tonal apparel only

`#333333` / `#4A443D` / `#B5786C`. Garment printing on grounds darker than `#1A1A1A`. Not for screens.

### Grounds and surfaces (digital layer, not in the PDF)

| Token | Hex | Use |
|---|---|---|
| `--ground-dark` | `#131313` | page background on dark sites |
| `--surface-dark` | `#181A1D` | cards, panels on dark ground |
| `--line-dark` | `#2A2D31` | hairlines on dark ground |
| `--ground-light` | `#F6F3EE` | page background on light sites (warm, not `#FFFFFF`) |
| `--surface-light` | `#FFFFFF` | cards, panels on light ground |
| `--line-light` | `#DDD7CE` | hairlines on light ground |

### Rules

- Dark ground → Palette 02. Light ground → Palette 01. The accent changes with the ground.
- **One accent per view.** A page has one orange (or rose) call to action; everything else is
  ink/bone and gray/taupe.
- Do not recolour outside these palettes. No gradients, glows, drop shadows, bevels or outlines
  on the logo or on brand type.
- Semantic colours (error, success) are not brand colours; when needed use `#B23A2E` (error) and
  `#3F7D5A` (success), never the accent.

## 3. Logo

Files: `Logo/Final/files_polished/*.svg` — the only approved set (names match the PDF File Index). The SVGs in the `Logo/Final/` root and `Logo/Final/files/` are earlier iterations; do not use them.

| Configuration | When | File pattern |
|---|---|---|
| Lockup (mark above wordmark) | whenever there is room | `raccool-lockup-*.svg` |
| Wordmark (type only) | headers, footers, one-line uses | `raccool-wordmark*.svg` |
| Mark (symbol only) | avatars, favicons, app icons | `raccool-mark-*.svg` |

Variants: `light` / `mono-light` on light grounds; `dark` (bone + taupe + rose) / `mono-dark` on
dark grounds; `blackout` for tonal apparel.

Minimum sizes: lockup **300 px** tall; wordmark **200 px** wide; mark **32 px** tall. Below the
lockup minimum, use the wordmark or the mark — never a shrunken lockup (the INTERACTIVE INC. line
becomes illegible).

Clear space: 2× the cap height of RACCOOL on every side.

Never: stretch, rotate, recolour, add effects, rebuild the wordmark in another typeface, separate
the mark from the wordmark inside a lockup, or place the logo on a busy photo or a ground with
less than 3:1 contrast.

## 4. Typography

The wordmark is custom geometry — never typeset it. For everything else:

| Role | Face | Fallback | Notes |
|---|---|---|---|
| Display / headings | **Barlow Condensed** 700–800 | Impact, Arial Narrow | Uppercase for H1/H2, `line-height: 0.9–0.95`, tracking `+0.01em` |
| Body | **Source Serif 4** 400/600 | Georgia | 17 px base on web, `line-height: 1.6`, measure ≤ 65 ch |
| Labels / data / captions | **IBM Plex Mono** 400/500 | ui-monospace | 11–12 px, uppercase, tracking `+0.10–0.14em`, taupe or gray |

All three are on Google Fonts. Display is loud so body can be quiet; do not use the display face
below 20 px, and do not set body copy in it.

Type scale (web): 12 · 13 · 15 · 17 · 19–23 (lede) · 26 (H3) · 40–72 (H2, fluid) · 64–150 (H1, fluid).

## 5. Layout and components

- Max content width 1180 px; side gutter `clamp(16px, 5vw, 64px)`.
- Section rhythm: `padding-block: clamp(72px, 10vw, 140px)`.
- Two-column splits at ≥ 860 px, single column below. Nothing horizontal-scrolls on a phone.
- Cards and panels: 1 px hairline border, 6 px radius, surface colour one step above ground.
  No drop shadows. Hierarchy comes from spacing and type, not from boxes.
- Buttons: display face, uppercase, tracking `+0.06em`, 14 px × 22 px padding, 4 px radius.
  Primary = accent fill; secondary = 1 px bone/ink outline.
- Images: 16:9 or the card's 5:7. Real screenshots are captioned as screenshots; concept renders
  are always labelled "concept render" or "target look".
- Motion: only where it demonstrates something (the tilting card). No parallax for its own sake,
  no scroll-triggered fades. Respect `prefers-reduced-motion`.

## 6. Voice

- Plain, concrete, specific. Short sentences. Numbers over adjectives.
- Industry-standard terms only: vertical slice, playtest, demo, wishlist, alpha. **Never**
  internal document names, IDs or codes (design-doc numbers, decision-record numbers, measured
  constant names). Say what is true, not which file records it.
- No hype words ("revolutionary", "immersive", "next-gen"). No exclamation marks.
- We say "we" for the studio and name the game as **SLABBED** (internal) or
  **SLABBED: TCG Card Grader** (store-facing). The in-game company is **Burrard Card Grading
  (BCG)** — never PCG.
- English is the working language of every published surface.

## 7. Product layer — SLABBED

The game has its own look that sits *inside* the brand, not on top of it. Use these only for
SLABBED marketing and in-game UI; never on the corporate lockup.

| Token | Hex | Meaning |
|---|---|---|
| `--desk` | `#0F1113` | the desk mat, deep neutral |
| `--lamp` | `#F0C98C` | warm lamp light; flaw-found highlight |
| `--paper` | `#E8E2D4` | inspection record, manual pages |
| `--stamp` | `#B23A2E` | reject codes, altered-grade marks |

Fluorescent-lit realism: muted, grounded, slightly worn. The card is the only thing allowed to
be glossy. The UI is paperwork — forms, slips, ledgers — rendered as objects on the desk, not as
floating panels.

## 8. Checklist before publishing anything

- [ ] Ground decided → palette matches it (dark = Albino, light = Northern)
- [ ] One accent CTA per view
- [ ] Logo at or above minimum size, correct variant, clear space respected
- [ ] Display / body / mono faces in their roles; no wordmark typeset in a font
- [ ] Copy uses industry terms; no internal IDs; no hype
- [ ] Concept renders labelled; screenshots real
- [ ] Works at 400 px wide with no horizontal scroll
