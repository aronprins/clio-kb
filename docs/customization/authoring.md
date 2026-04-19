# Authoring Pages

Pages are plain Markdown files, so the easiest way to extend the site is to keep writing docs the way you already do.

## Internal links

Use relative Markdown links between pages:

- [Overview](../getting-started/overview.md)
- [GitHub Pages Deployment](../deployment/github-pages.md)

The app rewrites these into in-app navigation automatically.

## Headings

Headings become deep-link targets. The app generates anchor links for each heading so readers can copy direct URLs.

## Code blocks

Fenced code blocks get a copy button in the rendered UI.

```sh
npm run docs:build:auto
```

## Tables and images

Standard Markdown tables and images are supported. Keep image paths relative to the Markdown file location.
