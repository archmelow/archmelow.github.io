<!-- .github/copilot-instructions.md - guidance for AI coding agents working on this repo -->

# Quick orientation

This repository is a single-page static website (username.github.io). There is no build system or package manager. The site is served directly from the repository root HTML/CSS and static assets.

Key facts:
- Entry point: `index.html`
- Global styles: `stylesheet.css`
- Static assets: `files/` (e.g. `files/CV.pdf`) and `images/` (e.g. `images/profile_photo.jpg`, `images/Affogato.jpg`)
- Template origin: adapted from Jon Barron (comment in `index.html`)

## Big-picture architecture

- Very small, static site. All content is authored as HTML and referenced assets. There are no JS frameworks, no build step, and no tests. Edits are typically direct HTML/CSS updates.
- Layout: table-based responsive layout with inline styles in `index.html` and site-wide rules in `stylesheet.css`. Treat changes carefully — a single replacement from tables -> flex/grid can break spacing and mobile behavior.
- Navigation is implicit: links are root-relative (e.g. `/affogato` project page link in `index.html`) and asset paths are relative to repository root.

## Files and patterns to reference
- `index.html` — single template. Publications are listed as table rows with image on the left and metadata on the right. To add a publication, copy an existing `<tr>` block and update the image and links.
- `stylesheet.css` — global styling and the primary place to change fonts, colors, and timeline styles. The font-family is loaded from Google Fonts in `index.html`.
- `files/` — binary documents (CV). Keep original filenames; links in `index.html` reference `files/CV.pdf`.
- `images/` — media used by the page. Note: repository runs on Linux so filenames are case-sensitive.

## Developer workflows (what to run)
- Local preview: open `index.html` in a browser or run a lightweight HTTP server to avoid cross-origin issues:

  python3 -m http.server 8000

  then open http://localhost:8000 in your browser (run from the repo root).
- Deploy: this is a GitHub Pages user site. Push to the `main` branch of `dmsgk724.github.io` to publish. (If Pages settings differ, adjust accordingly.)

## Project-specific conventions and gotchas
- Keep inline table structure and inline style attributes unless intentionally refactoring: the design relies on table sizing and inline paddings.
- Image and file paths are relative and case sensitive. Verify the exact filename in `images/` and `files/` before updating links.
- External resources: Google Fonts and external links (arXiv, project pages) are used; network access is expected in production browsers.
- Avoid adding a JS build pipeline unless you add a clear README and CI, because the current project expects direct HTML edits and GitHub Pages will serve the root.

## Editing examples (how to make common changes)
- Add a publication: duplicate the `<tr>` block under the Publications section in `index.html`, update `<img src='images/...'` and the metadata (authors, links). Keep the same table structure to preserve layout.
- Update profile image: replace `images/profile_photo.jpg` or update the `<img src>` path in `index.html` and ensure the new file is committed under `images/`.

## Debugging checklist
- If an image or file doesn't load: confirm correct relative path and exact filename (case-sensitive).
- If CSS changes have no effect: verify browser cache; also check whether inline styles in `index.html` override `stylesheet.css`.
- For layout regressions: compare changed `<table>`/`<td>` paddings and widths to existing rows — small spacing differences can cascade.

## When to ask for human review
- Any refactor that replaces table-based layout with modern layout (flex/grid). These changes affect visual spacing and require visual QA on desktop and mobile.
- Adding third-party tooling (npm, bundlers, CI) — get agreement and update README + deployment instructions.

If anything here is unclear or you'd like instructions expanded for a new workflow (e.g., adding CI or switching to a Hugo/Jekyll static site generator), tell me which direction and I will update this file.
