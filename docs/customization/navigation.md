# Navigation

The sidebar and landing cards are driven entirely by `site/content.json`.

## Section shape

Each section contains:

- `title`
- `icon`
- `desc`
- `pages`

Example:

```json
{
  "title": "Getting Started",
  "icon": "rocket",
  "desc": "First steps for new users.",
  "pages": [
    {
      "title": "Quickstart",
      "file": "../docs/getting-started/quickstart.md"
    }
  ]
}
```

## File paths

Page file paths in `content.json` are resolved relative to `site/`, not the repository root.

That is why the paths typically begin with `../docs/`.

## Choosing icons

Section icons use [Lucide](https://lucide.dev/) icon names in kebab-case.

Examples:

- `rocket`
- `book-open`
- `braces`
- `settings-2`
