## Repository snapshot

- Type: Static marketing site / template (HTML + CSS + JS). No backend code.
- Main entry: `index.html` (site pages: `index.html`, `article.html`, `coming-soon.html`, `privacy.html`, `terms.html`).
- Assets: `css/`, `js/`, `images/`, `webfonts/`.

## Big-picture architecture (what AI agents must know)

- This is a client-side static template derived from an Inovatik Bootstrap template (see `readme/readme.txt`).
- All behaviour is implemented in `js/scripts.js` using jQuery and a few plugins (Swiper, Magnific Popup). Key patterns:
  - Smooth-scrolling links use the `page-scroll` class and are handled in `js/scripts.js` (see the `page-scroll` click handler).
  - Site navigation toggles and off-canvas menu behavior are in `js/scripts.js` (search for `offcanvas` and `toggleClass('open')`).
  - Carousels use Swiper initialized with selector classes like `.text-slider` / `.mySwiper` (see `index.html` + `js/scripts.js`).

## Developer workflows & commands

- No build step or package manager is present. Typical dev flow:
  1. Open `index.html` directly in a browser for basic checks.
 2. For full plugin behavior (and to avoid CORS issues), run a local static server from the project root. Example (PowerShell):

```powershell
# from project root
python -m http.server 8000
# or, if you have Node installed: npx http-server -c-1 .
```

- Debugging: use browser DevTools. Find interactive behavior in `js/scripts.js` and style rules in `css/styles.css`.

## Project-specific conventions & patterns

- Single-source-of-truth pages: `index.html` contains the main content and includes the rest of the pages via separate HTML files in the root.
- All custom styling is in `css/styles.css` (see the large table-of-contents at the top of that file). Modify there instead of editing vendor CSS.
- Iconography and fonts are provided by local files in `webfonts/` and `css/fontawesome-all.css`, plus remote Google Fonts links in `index.html`.
- JS uses the jQuery pattern `(function($){ ... })(jQuery);` — maintain jQuery compatibility when adding scripts.

## Integration points & external dependencies

- Local/plugin copies (already bundled): `js/jquery.min.js`, `js/bootstrap.min.js`, `js/swiper.min.js`, `js/jquery.magnific-popup.js`, `js/jquery.easing.min.js`.
- External CDNs used in `index.html`: Google Fonts & Bootstrap Icons (these are optional fallbacks; template includes local vendor assets).

## Concrete examples agents should reuse (do this, not that)

- When adding a new interactive feature, follow the pattern in `js/scripts.js`: attach handlers on document ready / `(function($){})` wrapper; reuse existing classes like `page-scroll` and `popup-with-move-anim` for consistent UX.
- To add a new section with cards that match design, copy the structure used under `<div class="services">` in `index.html` (cards inside `.swiper-wrapper` / `.swiper-slide`) and let Swiper handle navigation.
- To change slider speed or behavior, edit the `/* Text Slider - Swiper */` block in `js/scripts.js` (see `readme/readme.txt` note pointing to Swiper demos).

## What NOT to change lightly

- Vendor files in `css/` and `js/` (bootstrap, swiper, magnific-popup, jquery) — prefer overriding in `css/styles.css` or adding a new custom JS file.
- Paths referenced in `index.html` are relative — moving files may break references. Keep existing folder layout unless you update all paths.

## Questions an agent should ask the human

- Is there a desired hosting environment (GitHub Pages, Netlify, custom server)? That determines whether we should add CI/publish scripts.
- Are we adding build tooling (npm, bundler, minifier) or keeping the repo zero-dependency static?

## Quick checklist for PRs affecting UI/UX

- Run site locally and verify: navigation, Swiper slides, Magnific Popup lightboxes, and the `Back to Top` link.
- Update `readme/readme.txt` if you change asset attributions or swap licensed images.
- Keep commits focused: "css: adjust header spacing" or "js: add contact form notEmpty handler" — link UI screenshots in PR when layout changes.

---

If any of these sections look incomplete or you'd like the instructions tuned toward CI, hosting, or adding a JS build step, tell me which area to expand and I will iterate.
