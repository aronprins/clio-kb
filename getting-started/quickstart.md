# Quickstart

This starter does not require a framework build chain for development.

## Build the docs bundle

```sh
npm run docs:build:auto
```

This writes a release bundle into `.site/`.

## Serve it locally

```sh
npm run docs:serve
```

Then open `http://localhost:4321`.

## Add your own docs

Create Markdown files under `docs/`, then register them in `site/content.json`.

Example:

```json
{
  "title": "My Page",
  "file": "../docs/guides/my-page.md"
}
```

## Common workflow

1. Add or edit Markdown in `docs/`
2. Update `site/content.json`
3. Rebuild the output bundle
4. Preview locally
