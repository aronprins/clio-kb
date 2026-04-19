# Clio KB

> Named after **Clio** — the Greek Muse of history and record-keeping. She was the keeper of knowledge, the one who made sure nothing worth remembering was lost. Clio KB does the same for your docs.

Clio KB is a lightweight static knowledge base for Markdown docs: keep your content in `docs/`, define navigation in `site/content.json`, run one build command, and publish the result as plain static files.

<img width="2688" height="2646" alt="screencapture-aronprins-github-io-clio-kb-2026-04-19-12_24_14" src="https://github.com/user-attachments/assets/72a2998d-077a-49bf-9774-fa0c45ee927a" />

## How it works

Clio KB separates content from presentation:

- `docs/` contains your Markdown pages
- `site/content.json` defines the sidebar, landing cards, section descriptions, and page order
- `site/` contains the static shell, styling, and build script

The build is driven by [`site/build-release.mjs`](site/build-release.mjs). It copies the shell assets, rewrites navigation for release output, and includes the Markdown files and linked local assets referenced by your docs.

There are no npm dependencies in this repository. The build uses Node.js plus the files already in the repo.

## Quick start

```sh
# Clone the repo
git clone https://github.com/aronprins/clio-kb.git
cd clio-kb

# Build the docs bundle into .site/
npm run docs:build:auto

# Preview locally
npm run docs:serve
# -> http://localhost:4321
```

To replace the starter content:

1. Add or edit Markdown files under `docs/`
2. Register those pages in `site/content.json`
3. Rebuild the site

There is no filesystem auto-discovery. If a page is not listed in `site/content.json`, it will not appear in navigation.

## npm scripts

| Script | What it does |
| --- | --- |
| `npm run docs:build` | Builds the site with the fixed GitHub Pages base path `/clio-kb/` |
| `npm run docs:build:auto` | Builds with automatic base-path detection for local preview or unknown hosting prefixes |
| `npm run docs:serve` | Serves `.site/` locally on port `4321` via Python's HTTP server |
| `npm run docs:publish` | Builds and publishes the site to `gh-pages` via `scripts/publish-gh-pages.sh` |

## Project structure

```text
clio-kb/
├── site/                     Static docs shell and release builder
│   ├── index.html
│   ├── app.js
│   ├── styles.css
│   ├── content.json
│   └── build-release.mjs
├── docs/                     Markdown source content
│   ├── getting-started/
│   ├── customization/
│   ├── reference/
│   └── deployment/
├── scripts/
│   └── publish-gh-pages.sh
├── .github/ISSUE_TEMPLATE/
└── .site/                    Generated output; rebuild instead of editing
```

## Configuration

The build script accepts two main flags:

| Flag | Description |
| --- | --- |
| `--base-path <path|auto>` | Public URL base path. Use `/clio-kb/` for GitHub Pages under `aronprins/clio-kb`, `/` for a root deployment, or `auto` for local preview and fallback detection. |
| `--out-dir <dir>` | Output directory for the release bundle. The CLI default is `site/release`; the npm scripts write to `.site/`. |

Example:

```sh
node site/build-release.mjs --base-path /docs/ --out-dir .site
```

## Deploying

For this repository's default GitHub Pages setup:

```sh
npm run docs:publish
```

The publish script builds the site, clones the current repository into a temporary directory, checks out or creates `gh-pages`, replaces the published files, commits, and pushes.

If you are deploying under a different repo slug or base path, update the relevant repo metadata together:

- `package.json`
- `scripts/publish-gh-pages.sh`
- `site/app.js`
- `site/index.html`
- `.github/ISSUE_TEMPLATE/`

## Contributing

For content changes, prefer editing Markdown in `docs/` and updating `site/content.json` rather than hardcoding docs copy into the site shell.

If you add or move a page:

1. Create or move the Markdown file in `docs/`
2. Update `site/content.json`
3. Rebuild the site
4. Verify the page loads and internal links still resolve

## License

MIT

*Clio was the daughter of Zeus and Mnemosyne — goddess of memory. Between the two of them, nothing worth remembering was lost.*
