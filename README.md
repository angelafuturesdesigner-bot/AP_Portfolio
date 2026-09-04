# Angela Piazza — Portfolio

Static site. No build step, no dependencies to install.

## Files

- `index.html` — the whole site (Home + My Work as two tabs, all animations, contact modal)
- `support.js` — runtime required by index.html (must stay next to it)
- `image-slot.js` — image placeholder component used by index.html
- `assets/` — all images (portrait, project screenshots)
- `work/niew-hero-audit.html` — the AI-built landing page embedded in the "New Design System Offer" project

All four items are required. Keep the folder structure exactly as it is.

## Run locally

Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Publish on GitHub Pages

1. Create a repository and push the contents of this folder to the root of the `main` branch.
2. Repository → Settings → Pages → Source: `Deploy from a branch`, Branch: `main` / `/ (root)`.
3. The site goes live at `https://<user>.github.io/<repo>/`.

Nothing else to configure — `index.html` is at the root, so it is served automatically and fills the browser window.

## Notes

- The page is designed at 1440px wide and centred; it is not a responsive mobile layout.
- The embedded landing page (`work/niew-hero-audit.html`) is loaded in an iframe, which is why it must be served from the same folder.
- The contact modal copies email/phone to the clipboard. Clipboard access requires `https://` or `localhost` — on GitHub Pages this works.
- `mailto:` and `tel:` links depend on the visitor's own mail/phone app.

## Editing

`index.html` is a single self-contained document: markup at the top inside `<x-dc>`, styles in the `<style>` block in the head, behaviour in the `class Component` script at the bottom (view switching, carousels, auto-scrolls, contact modal, hero animation).
