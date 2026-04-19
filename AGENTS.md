# AGENTS

Operational notes for contributors and coding agents working in `Clio KB`. Reader-facing usage stays in [README.md](README.md).

## Repo layout

```text
site/                     Static docs shell and release builder
├── index.html            Main shell markup
├── app.js                Client-side routing, rendering, search, and UI logic
├── styles.css            Site styling
├── content.json          Navigation manifest and landing-page source of truth
└── build-release.mjs     Produces a standalone bundle in .site/
docs/                     Markdown source content
├── getting-started/      Intro and setup docs
├── customization/        Authoring and navigation docs
├── reference/            Internal structure and technical reference
└── deployment/           Hosting and publishing docs
scripts/
└── publish-gh-pages.sh   Builds and pushes the gh-pages branch
.github/ISSUE_TEMPLATE/   Support, bug, and docs feedback templates
.site/                    Generated output; do not edit by hand
```

## Commands

```sh
# Build the static site into .site/ using the GitHub Pages base path
npm run docs:build

# Build with automatic base-path detection for local preview
npm run docs:build:auto

# Serve .site/ on http://localhost:4321/
npm run docs:serve

# Build and push the published site to gh-pages
npm run docs:publish
```

## Working model

- Treat `docs/` as source content and `site/` as the presentation layer.
- Treat `site/content.json` as the source of truth for sidebar structure, landing cards, section descriptions, and page order.
- Treat `.site/` as build output only. Rebuild it instead of editing generated files.
- Keep file paths in `site/content.json` relative to `site/`, usually `../docs/...`.

## Base paths

`site/build-release.mjs` accepts `--base-path <path|auto>`.

- Use `/clio-kb/` for GitHub Pages under `aronprins/clio-kb`.
- Use `auto` for local preview or unknown hosting prefixes.
- Use an explicit custom prefix for self-hosting, for example `--base-path /docs/`.

Base-path mismatch is the most common deployment failure. If generated asset URLs point at `/clio-kb/` but the bundle is served from `/`, the site will appear broken even though the build succeeded.

## Adding or moving pages

1. Create or move the Markdown file inside `docs/`.
2. Update `site/content.json`.
3. Rebuild the site.
4. Verify that the new page loads and that internal links still resolve.

There is no filesystem auto-discovery. If a page is not registered in `site/content.json`, it will not appear in navigation.

## Navigation and icons

Each section in `site/content.json` contains:

- `title`
- `icon`
- `desc`
- `pages`

Section icons use [Lucide](https://lucide.dev/) kebab-case ids such as `rocket`, `palette`, `book-open`, or `cloud`. If an icon name is invalid, the placeholder will render empty.

## Internal links and slugs

- Internal Markdown links should stay relative between docs pages.
- App routes are derived from page file paths.
- Heading anchors are generated in the browser from heading text.

When renaming or moving docs files, check:

- links inside Markdown
- references in `site/content.json`
- the resulting route after rebuild

## Repo identity

The repo slug is currently assumed to be `aronprins/clio-kb` in a few places:

- `site/app.js` for per-page edit and feedback links
- `site/index.html` for footer and GitHub links
- `.github/ISSUE_TEMPLATE/` for issue guidance
- `package.json` and `scripts/publish-gh-pages.sh` for the default Pages base path

If the repository moves, update all of those together.

## Issue templates

`.github/ISSUE_TEMPLATE/` contains three templates:

- `01-support.yml`
- `02-bug.yml`
- `03-docs-feedback.yml`

The docs feedback template is linked from rendered pages in `site/app.js`, so its filename and expected query params should stay aligned with that code.

## Publishing

`scripts/publish-gh-pages.sh` builds the site, clones the current repo into a temporary directory, checks out or creates `gh-pages`, replaces the published files, commits, and pushes.

It is designed to leave the working tree untouched.

## Editing guidance

- Prefer editing Markdown content in `docs/` rather than hardcoding prose into the shell.
- Prefer changing navigation in `site/content.json` rather than adding special-case logic to `site/app.js`.
- Keep the shell generic. Product- or org-specific wording should live in docs content unless it is true repository metadata.
- After meaningful changes to docs structure or routing, run a fresh build and verify the generated `.site/` output.
