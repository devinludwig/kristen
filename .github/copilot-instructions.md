Purpose
This repository is a small static artist portfolio site. These instructions help AI coding agents make safe, high-value edits quickly without introducing new build tools or changing deployment-critical files.

Quick overview
- Project type: static HTML/CSS site (no Node/webpack/etc.). Primary files: `index.html`, `about.html`, `contact.html`, `portfolio.html` (currently empty), `style.css` and the `img/` asset folder.
- CDN dependencies: Bootstrap CSS/JS and Google Fonts are loaded via CDN in the HTML pages. Do not replace these with local packages unless requested.
- Deployment: domain recorded in `CNAME` (`www.kristendiederich.com`). Do not modify `CNAME` without explicit approval.

Key patterns and conventions
- Navigation: Each page contains a repeated nav block. When updating navigation, update `index.html`, `about.html`, and `contact.html` (and `portfolio.html` if used).
- Image handling: All assets live in `img/`. Filenames may contain spaces and parentheses (e.g. `IMG_0874 (1).jpeg`) — preserve filenames exactly when referencing or updating. To add a painting: add the file to `img/` and add a new `div.carousel-item` inside the `.carousel-inner` in `index.html` with `<img src="img/your-file.jpg" alt="Description">`.
- Carousel: The main gallery is a Bootstrap carousel (`#carouselPaintings`) with `data-ride="carousel"` and `data-interval="false"`. Keep new images as sibling `.carousel-item` blocks; the first item should retain the `active` class.
- Styling: All site styles live in `style.css`. Layout behavior (mobile vs desktop) is implemented via media queries — don't change layout semantics without testing in both breakpoints.

Developer workflows
- Local preview (recommended): run a simple HTTP server from the project root to preserve correct resource paths:
    cd /path/to/repo
    python3 -m http.server 8000
    # then open http://localhost:8000 in your browser

- Editing files: make edits directly to the HTML/CSS files. There is no build step; changes are visible immediately in a local server or by opening `index.html` in a browser.
- Grep examples (to find related markup quickly):
    grep -R "navbar-brand" -n .
    grep -R "carouselPaintings" -n .

Integration and external dependencies
- External services: pages link to external galleries and social profiles (e.g., Instagram links in `contact.html`). These are simple anchors — avoid changing external URLs unless instructed.
- No backend: there are no server-side endpoints or forms. Mailto links and commented-out email blocks exist but are inactive.

Guidance for AI agents (do/avoid)
- Do: make minimal, targeted edits; include examples in PR body (e.g., "Added carousel item for img/foo.jpg"). Update all pages when cross-cutting (nav, meta tags, footer text).
- Do: preserve image filenames and `CNAME` unless user explicitly asks to change domain or reorganize assets.
- Avoid: introducing build tooling, package managers, or compiling steps unless the user requests a migration. Avoid reformatting unrelated files.
- When renaming or optimizing images: update every HTML reference (use `grep` to find usages). If you must rename many images, propose a plan first.

Examples (common edits)
- Add a new painting: add file to `img/`, add a `div.carousel-item` in `index.html` inside `.carousel-inner`, and verify it displays in both desktop and mobile layouts.
- Update nav text or order: edit the nav block in each page to keep them consistent.
- Optimize CSS: prefer editing `style.css` and keep selector specificity minimal to avoid breaking the responsive layout.

Notes and cautions
- `portfolio.html` is currently empty — if you populate it, add it to the nav and ensure responsive behavior.
- The site uses Bootstrap 4.x CDN; replacing it with a different major version may require HTML/CSS changes.

If anything here is unclear or you want additional examples (e.g., a script to batch-update image references), tell me which operation and I will add step-by-step instructions.
