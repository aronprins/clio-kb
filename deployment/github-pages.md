# GitHub Pages Deployment

The included publish script builds the site and pushes the output to `gh-pages`.

## Default base path

This repository is configured for:

`/clio-kb/`

That matches GitHub Pages for `aronprins/clio-kb`.

## Publish flow

```sh
npm run docs:publish
```

The script will:

1. build the release bundle
2. clone the current repository
3. switch to `gh-pages`
4. replace the published files
5. commit and push the update

## Using a different repository name

If you publish from a different repo slug or under a custom domain, update the base path in:

- `package.json`
- `scripts/publish-gh-pages.sh`

You can also build manually:

```sh
node site/build-release.mjs --base-path /your-base-path/ --out-dir .site
```
