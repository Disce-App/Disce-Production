# Disce-Stage — public website

Public, publishable source of the DISCE website (deployed at
`stage.weltvorstellung.de` today, `weltvorstellung.de` after the cutover).

> **This repository must contain publishable site files only.**
> All internal planning, strategy, audit, decision and design documents live in
> the private repository `Disce-App/disce-internal` and must never be added
> here. GitHub Pages serves the tracked tree as-is, and this repository is
> public — anything committed is public.

## Contents

- HTML pages at the repository root (`index.html`, `philosophy.html`,
  `kernel.html`, `team.html`, `status.html`, `waitlist.html`, `impressum.html`,
  `datenschutz.html`, `beta.html`, `404.html`)
- `css/` — shared stylesheet (`experimental.css` plus the generated
  `experimental.min.css` referenced by the pages)
- `js/` — `site.js` and the generative modules under `js/generative/`
- `fonts/` — self-hosted subsets and OFL licences
- `images/` — masters and committed responsive derivatives in `images/derived/`
- `robots.txt`, `sitemap.xml`, `site.webmanifest`, `favicon.ico`,
  `apple-touch-icon.png`, `CNAME`, `.nojekyll`

## Local preview

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000/>. Serve from the repository root; there is no
build step.

See `AGENTS.md` for the working rules.
