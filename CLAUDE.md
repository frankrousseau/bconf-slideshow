# Blender Conference 2026 — Kitsu booth slideshow

Single-file HTML slideshow that loops on the booth screen at Blender Conference 2026 (Amsterdam). Adapted from the MIFA 2026 deck (`index-prev.html` is older still). CGWire shows it between live demos of Kitsu (open-source production tracking for animation and VFX studios).

## Files

- `index.html` — the whole slideshow. CSS and JS are inline. No build, no framework, no npm.
- `assets/` — image assets referenced by the slideshow. Most are placeholders to be replaced.
- `design/` — reference design source (`slideshow-calm.html` + assets). Not shipped, not loaded by `index.html`. Treat as a frozen reference; live changes go in `index.html`.

## How it runs

Open `index.html` in Chrome or Firefox. Press `F` for fullscreen.

- Auto-advances per slide (`data-duration` in seconds, fallback 10), loops forever. `#N` in the URL opens slide N.
- 600ms crossfade between slides
- Persistent chrome at the top: Kitsu badge + `Blender Conference 2026 - Amsterdam` (no booth number)
- Bottom footer: thin green progress bar, `01 / 19` counter (computed from the DOM), dot indicators, "Auto-advance · 10s" label
- Keyboard: `F` fullscreen, `Space` pause, `←` / `→` (or PageUp/PageDown) navigate, `Home` restart

## Slide order (19 slides)

Each content slide has an **eyebrow** (small uppercase green label) above a single-color **h1**. The `<em>` tags left in h1s are neutralized in CSS (`color: inherit`): no two-tone titles, and no middle dots as separators (use a hyphen), both read as AI-generated. `data-slide` ids are historical and not in display order; DOM order is what plays.

1. Logo intro
2. "The context changed" / "Animation productions changed" (2x2 grid)
3. "Today" / "Production is scattered across a dozen tools"
4. "New solution" / "A unified workspace" (screenshot)
5. "Built-in review" / "Powered by a review engine" (screenshot)
6. "Smart scheduling" / "And a planning system" (screenshot)
7. "Open source" / "Run it your way" — cloud / on-premise / self-hosted + pills (AGPL license, GitHub stars, contributors, public roadmap). Moved up early for the Blender audience.
8. "Blender pipeline" / "Made to work with Blender" — Blender add-on / Python API (Gazu) / Used by Blender Studio
9. "Made with Kitsu and Blender" — posters (Flow, Unicorn Wars, Seven Bears, Woolly Woolly, Coop Troop, Wing It!)
10. "Built for everyone" / "One tool, every role" (hexagon)
11. "Multi-studio, by design" / "One backbone, many studios"
12. "Infrastructure" / "Distributed by design"
13. "Coming from spreadsheets?" / "Why teams switch"
14. "Adoption" / "Grown by the community" (numbers)
15. "Studios and schools" / "Teams that ship with Kitsu" (logo grid, Blender first)
16. "The next generation" / "Students learn on Kitsu" (schools)
17. "Selected at Annecy 2026" — posters
18. "What's new in Kitsu" — Plugin System / Enhanced playlists / Smart scheduling
19. Contact — "See Kitsu live, ask for a demo" + www.cg-wire.com/kitsu + QR

## Visual conventions

Authentic Kitsu / CGWire palette (don't substitute approximations):

- Background `#25282E` (k-dark-grey), elevated `#2D2E36`, soft `#36393F`, deep `#202225`
- Accent green `#00B242`, light `#7AE3A0`, dark `#008732`
- Text white `#FEFEFE`, muted `rgba(255,255,255,0.62)`, faint `rgba(255,255,255,0.38)`
- Borders `rgba(255,255,255,0.08)` / `0.16`
- Font: Lato (Google Fonts), weights 300/400/700/900. Black (900) for h1/h2/wordmark/numbers, 700 for eyebrows/labels, 400 for body.
- Subtle radial vignette over the stage
- Large, centered text, lots of whitespace
- No bullet points
- No em dashes (use commas or periods)
- Never mention competitors (Flow, ftrack, AYON, ShotGrid)
- "Open source" is central for this audience (Blender Conference), state it plainly
- Tone: factual and confident, not aggressive

## Asset placeholder pattern

Each image asset has a styled visual fallback rendered behind it. The `<img>` covers the fallback when it loads; `onerror="this.remove()"` strips the broken `<img>` so the fallback shows through. Drop the file at the expected path and it just appears, no HTML edit needed.

```html
<div class="poster" style="--ph-a:#3a4a5e;--ph-b:#0f1218">
  <div class="placeholder">…rich styled fallback (badge, silhouette, title, subtitle)…</div>
  <img src="./assets/poster-01.jpg" alt="" onerror="this.remove()">
</div>
```

The fallbacks are rich (mock UI for the screenshot, mono+name tile for logos, gradient+silhouette+title for posters, fake QR grid with the Kitsu mark in the center) — the slideshow looks intentional even with no assets at all.

## Assets expected in `./assets/`

- `kitsu-mark-styled.svg` — already present, used on slides 1 and 13. Authoritative copy lives in `design/assets/`.
- `screenshot-ui.png` — Kitsu interface screenshot (16:10 ideal, covers the mock UI on slide 3)
- `review.png` — Kitsu review-engine screenshot (covers the play-icon fallback on slide 4)
- `schedule.png` — Kitsu scheduling-view screenshot (covers the calendar-icon fallback on slide 5)
- `logo-client-01.png` … `logo-client-12.png` — client studio logos (any aspect, inverted to white via CSS filter)
- `poster-01.jpg` … `poster-04.jpg` — film/series posters (portrait, 2:3 ideal)
- `qr-code.png` — QR pointing to kitsu.cg-wire.com or a cloud trial form

## SVG diagrams (slides 7 & 8)

Both diagrams are SVG inline, no asset needed. The hexagons are written with raw point coordinates; if you need to resize or reposition labels, edit the `viewBox` and `<text>` x/y directly.

The Kitsu wolf mark is duplicated as inline SVG paths in the chrome and slides 7, 8, and the QR center on slide 13. Slides 1 and 13 use `<img src="./assets/kitsu-mark-styled.svg">` instead. If the SVG is updated, refresh all five occurrences.

## What is NOT in scope

- Mobile / responsive (booth screen is 1920x1080+ landscape only)
- Localization (English only)
- Analytics, tracking, anything network beyond Google Fonts
- Build tooling
