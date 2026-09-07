# Angela Piazza — Design Portfolio

Static single-page site. Two views (Home / My Work) switched in JavaScript. No build step,
no dependencies, nothing to install. Open `index.html` and it runs.

Last updated: 7 September 2026

---

## What is in this folder

    index.html                  the site (self-contained: markup + inline logic)
    support.js                  runtime that renders the component
    image-slot.js               drag-and-drop image placeholder component
    assets/                     24 images (portrait + all project screenshots)
    work/
      niew-hero-audit.html      self-contained landing page shown in an iframe
    source/
      Portfolio.dc.html         EDITABLE SOURCE — see "Reopening the project"
      assets/, work/            same files, so source/ works standalone
    README.md                   this file

`index.html` and `source/Portfolio.dc.html` are byte-identical: the same file serves as
both the deployable site and the editable source. Keep them in sync if you edit one.

---

## Deploy to GitHub Pages

1. Create a repository (e.g. `angela-portfolio`) and push the contents of this folder to
   the root of `main`. (`source/` can stay — it is ignored by Pages.)
2. Settings → Pages → Source: "Deploy from a branch", Branch `main`, Folder `/ (root)`.
3. Publishes at `https://<user>.github.io/<repo>/` in about a minute.

Custom domain: add a `CNAME` file at the root containing the domain, then point a CNAME
DNS record at `<user>.github.io`.

## Running locally

All paths are relative, but the iframe is blocked under `file://` in some browsers, so
serve it:

    python3 -m http.server 8000     # then open http://localhost:8000

## Reopening the project

**In Claude Design** — start a project and upload `source/Portfolio.dc.html` together with
`source/assets/` and `source/work/`. The `.dc.html` extension is what makes it editable as
a component again (live preview, click-to-edit text and colors). `support.js` is provided
by the environment; the local copy here is only needed for plain hosting.

**In VS Code or any editor** — open `index.html`. Everything is inline: markup, styles and
the behaviour class near the bottom of the file. No toolchain, no npm, no compile step.
Edit, save, refresh the browser.

---

## Structure of the page

### Home
- Sticky header: avatar, name, Home / My Work tabs, "Contact me".
- Hero: five rotating headline phrases, decorative bars ("tasselli") peeking in from the
  left page edge, layered background washes. Hovering a bar pauses the rotation and shows
  that phrase.
- Selected work — three case rows in a centred `max-width: 1560px` container. All three
  text columns share one grid track, so they are identical width; images take the rest.
  Dividers have exactly 40px of clear space above and below.
  - 01 Service platform — fanned stack of screens plus a technician phone. The wrapper
    clips (`overflow: hidden`) and takes its height from the front-most card in normal
    flow, so it cannot spill into project 02 at any width.
  - 02 Design system — cross-fading screenshot showcase with clickable dots, locked to the
    screenshots' native 1366:768 ratio (no white bands). The tall documentation shot pans
    vertically. The cycle starts only once the section scrolls into view.
  - 03 Field operations — vertical auto-scrolling column of screens, capped at 620px so
    the track always overflows and keeps moving.
- Small AI builds — dark strip with two equal-size browser-chrome cards: the weekly hours
  tracker (auto-panning screenshot) and the NiEW hero audit (live iframe).
- Footer: email, phone, LinkedIn, Behance. Full-bleed, same as the header.

### My Work
Sticky header, sticky left project menu, horizontal snap galleries, four case sections,
click-to-zoom lightbox.

### The five headline phrases
1. the problem is bigger than the brief
2. nobody agrees on what to build first
3. the product works but nobody understands it
4. the team needs clear direction and cohesion
5. decisions need a measurable value behind them

---

## How the behaviour is wired

Everything is driven by data attributes, handled in the component class at the bottom of
the file:

| Attribute | Behaviour |
|---|---|
| `data-view="home" / "work"` | The two page views; the tabs toggle `display`. |
| `data-nav` | Header tab buttons. |
| `data-cue`, `data-cuewrap` | Hero bars; one highlights per headline rotation, hover pauses. |
| `data-fan` | Project 01 clipping wrapper. |
| `data-showcase`, `data-shot`, `data-dot` | Project 02 cross-fade. An IntersectionObserver (threshold 0.35) gates the cycle; `data-pan="slow"` marks the tall shot. |
| `data-vscroll`, `data-vtrack` | Project 03 auto-scrolling column. |
| `data-panbox`, `data-autopan` | Auto-panning tall screenshot; `data-panspeed` sets px/frame (default 0.28). Hover pauses, manual scroll allowed. |
| `data-gallery` | Horizontal snap gallery (My Work) with dimming of off-centre cards. |
| `data-embed`, `data-embed-inner` | Iframe authored at 1440px wide, scaled to its container by a per-box ResizeObserver. |
| `iframe[data-autoscroll]` | Slowly scrolls the embedded landing page. |
| `data-copy-hint` | Footer contacts: mailto/tel plus clipboard copy with a toast. |

---

## Responsive rules — important when editing

Fluid from roughly 1024px laptops upward:

- horizontal padding is `clamp(24px, 4.5vw, 80px)` everywhere;
- type sizes use `clamp()`;
- grids use `minmax(0, 1fr)` tracks, never fixed columns;
- gallery cards use `min(88%, Npx)` widths;
- header and footer are full-bleed; the header is `position: sticky; top: 0`.

**Do not add fixed pixel `width` / `height` to rows, cards or media wrappers.** That is
what previously caused horizontal page scroll, mismatched text columns, clipped cards and
collapsed iframes. If something looks wrong after an edit in a visual editor, look for a
stray `width: 1078px`-style value first.

---

## Fonts and colours

Montserrat (headings, labels) and Lato (body), loaded from Google Fonts.

    ink          #1C1F26      body text     #3F4652 / #5A6474
    accent       #4A5C8C      muted label   #8C9BBF
    hairline     #D6DDE8      light fill    #EDF1F7
    deep navy    #2E3C61      footer/dark   #1C1F26

---

## Contacts shown in the page

angela.futures.designer@gmail.com · +39 351 4936432 ·
linkedin.com/in/angelapiazzadesigner
