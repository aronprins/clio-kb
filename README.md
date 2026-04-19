# Clio KB

Clio KB is a lightweight static knowledge base for Markdown docs.

It keeps the content model deliberately simple:

- `docs/` contains your Markdown pages
- `site/content.json` defines the navigation
- `site/` contains the static shell, styling, and build script

## Quick Start

```sh
npm run docs:build:auto
npm run docs:serve
```

Then open `http://localhost:4321`.

## Project Structure

- `docs/` author-facing documentation content
- `site/index.html` shell markup
- `site/app.js` client-side navigation and rendering
- `site/styles.css` visual system
- `site/build-release.mjs` release bundle builder
- `scripts/publish-gh-pages.sh` GitHub Pages publishing helper

## Publishing

For GitHub Pages under `https://aronprins.github.io/clio-kb/`:

```sh
npm run docs:build
```

For any other host or subpath:

```sh
node site/build-release.mjs --base-path /your-base-path/ --out-dir .site
```

If you publish this under a different repo slug, update the GitHub links in `site/app.js`, `site/index.html`, and `.github/ISSUE_TEMPLATE/`.
