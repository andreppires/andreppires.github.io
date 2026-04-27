# andreppires.github.io

Personal site for André Pires — a single-page static CV/landing page.

Live at <https://www.andreppires.xyz/> (custom domain set via `CNAME`).

## Local preview

No build step. Either open `index.html` directly in a browser, or:

```sh
python3 -m http.server
```

## Deployment

Pushes to `master` are deployed by `.github/workflows/deploy.yml`, which uploads
the repository as-is to GitHub Pages.

When editing `css/style.css`, bump the `?v=N` query string in `index.html` so
visitors don't keep a stale cached copy.
