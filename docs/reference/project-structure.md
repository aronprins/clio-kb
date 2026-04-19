# Project Structure

This repository separates content from presentation.

## Top-level folders

### `docs/`

Source Markdown pages. Keep these grouped in a way that makes sense for your readers.

### `site/`

The static front-end shell:

- `index.html` defines the page frame
- `app.js` handles routing, rendering, search, and UI behavior
- `styles.css` defines the visual design
- `content.json` defines sections and page links
- `build-release.mjs` copies the required files into a deployable bundle

### `scripts/`

Utility scripts for publishing or maintenance.

## Release output

The build script writes a self-contained bundle into `.site/`. That bundle contains:

- the shell assets
- the navigation JSON
- the referenced Markdown pages
- copied image assets that are reachable from the docs
