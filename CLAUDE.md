# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page static personal site (André Pires' CV/landing page) served from GitHub Pages at the custom domain `www.andreppires.xyz` (set via `CNAME`).

There is **no build step**. `index.html` is the site; `css/style.css` is loaded directly. To preview locally, open `index.html` in a browser, or run `python3 -m http.server` from the repo root.

## Deployment

Push to `master` triggers `.github/workflows/deploy.yml`, which uploads the repository as-is (`path: .`) and deploys it to GitHub Pages. There is no Jekyll build executed by the workflow — it uses `actions/upload-pages-artifact` directly, not `actions/jekyll-build-pages`. Do not add Jekyll-specific files (`_config.yml`, layouts, includes, front matter) expecting them to render — `index.html` is a complete document and is shipped verbatim.

## Cache-busting CSS

`index.html` references the stylesheet as `css/style.css?v=N`. **When you edit `css/style.css`, bump the `?v=N` query string in `index.html`** so visitors don't keep a stale cached copy. (GitHub Pages doesn't fingerprint assets for us.)

## Visual system (when editing CSS)

The design is built around three brand colors defined as CSS custom properties in `:root`: `--green` / `--green-text`, `--orange`, `--blue`. Two patterns rely on these and are easy to break:

- **Card accent rotation.** `.role` cards in `.timeline` rotate their left-border color via `nth-child(3n+1|3n+2|3n)` rules that set `--card-accent`. Adding/removing/reordering `<div class="role">` elements changes which color each card gets — that's intentional, not a bug.
- **Section padding specificity.** `<section>` elements also carry `class="container"`. The `section.container` selector exists specifically to override `.container`'s padding shorthand. Keep that selector form when adjusting section spacing.

The hero `.avatar` is rendered as a circle purely via CSS (`border-radius: 50%`) over a square JPG. The favicon (`img/favicon.png`) is a pre-masked circular PNG generated from `profile.jpg` — regenerate it (not just swap the link) if `profile.jpg` ever changes.
