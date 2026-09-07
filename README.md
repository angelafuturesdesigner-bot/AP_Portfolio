# Angela Piazza — Design Portfolio

Static single-page site. Two views (Home / My Work) switched in JavaScript, no build step,
no dependencies to install. Open `index.html` and it runs.

## Deploy to GitHub Pages

1. Create a new repository (e.g. `angela-portfolio`).
2. Copy the contents of this folder into the repository root:

   index.html
   support.js
   image-slot.js
   assets/            (24 images: portrait + project screenshots)
   work/
     niew-hero-audit.html   (self-contained landing page loaded in an iframe)

3. Commit and push to `main`.
4. Repo → Settings → Pages → Source: "Deploy from a branch", Branch: `main`, Folder: `/ (root)`.
5. The site publishes at `https://<user>.github.io/<repo>/` in ~1 minute.

Custom domain: add a `CNAME` file at the root containing the domain, then point a CNAME DNS
record at `<user>.github.io`.

Note: file paths are relative, so the site also works from a subfolder or opened locally
(the iframe requires being served over http:// — with `file://` some browsers block it;
use `python3 -m http.server` locally).

## What is in the page

index.html is one self-contained document: markup + an inline component class holding all
behaviour. Fonts (Lato, Montserrat) load from Google Fonts; everything else is local.

### Home
- Sticky header with avatar, name, Home / My Work tabs, "Contact me".
- Hero: rotating headline phrases, decorative bars ("tasselli") peeking in from the left
  edge, layered background washes. Hovering a bar pauses the cycle and shows its phrase.
- Three case-study rows (01, 02, 03). All three text columns share one grid track width;
  images take the remainder.
  - 01: fanned stack of four screens.
  - 02: cross-fading screenshot showcase with clickable dots. The frame is locked to the
    screenshots' own 1366:768 ratio so there are no white bands. The tall documentation
    page pans vertically. The cycle only starts once the section scrolls into view.
  - 03: a vertical auto-scrolling column of six screens, capped at 620px tall so the track
    always overflows and keeps moving.
- "Small AI builds" strip (dark card): two equal-size browser-chrome cards — the weekly
  hours tracker (auto-panning screenshot) and the NiEW hero audit (live iframe).
- Footer with email / phone / LinkedIn / Behance.

### My Work
- Sticky header, sticky left menu, horizontal snap galleries per project, case sections
  01–04, click-to-zoom lightbox.

## Behaviour notes (data attributes drive everything)

| Attribute | What it does |
|---|---|
| `data-view="home" / "work"` | The two page views; tabs toggle `display`. |
| `data-nav` | Header tab buttons. |
| `data-cue` / `data-cuewrap` | Hero bars; one highlights per headline rotation. |
| `data-showcase`, `data-shot`, `data-dot` | Project 02 cross-fade showcase. IntersectionObserver gates the cycle. `data-pan="slow"` marks the tall shot. |
| `data-vscroll` / `data-vtrack` | Auto-scrolling vertical image column (project 03). |
| `data-panbox` / `data-autopan` | Auto-panning tall screenshot. `data-panspeed` sets px/frame (default 0.28). |
| `data-gallery` | Horizontal snap gallery in My Work. |
| `data-embed` / `data-embed-inner` | Iframe scaled to its container by a ResizeObserver; the inner page is authored at 1440px wide. |
| `iframe[data-autoscroll]` | Slowly scrolls the embedded landing page. |
| `data-copy-hint` | Footer contact links: mailto/tel plus clipboard copy and a toast. |

## Responsiveness

Fluid from ~1024px laptops upward: horizontal padding is `clamp(24px,4.5vw,80px)`,
type uses `clamp()`, grids use `minmax(0,1fr)` tracks, galleries use `min(88%, Npx)` card
widths. Avoid re-introducing fixed pixel `width`/`height` on rows or cards — that is what
causes horizontal page scroll and mismatched columns.

## Editing

Content and styling are inline in index.html — edit the markup directly. The one place with
logic is the component class near the bottom of the file (view switching, animations,
contact copy, lightbox).

## Contacts in the page

angela.futures.designer@gmail.com · +39 351 4936432 ·
linkedin.com/in/angelapiazzadesigner
