# AGENTS.md — Disce-Stage (public website)

Repository-specific instructions for coding agents working in this repo.

## What this repo is

The **public, publishable** source of the DISCE website. GitHub Pages serves the
tracked tree as-is and this repository is public, so **everything committed here
is public**.

## Hard guardrail — no internal documents

- All internal planning, strategy, audit, decision and design documents live in
  the **private** repository `Disce-App/disce-internal` (locally checked out as
  `../disce-internal`).
- **Never** commit internal documents, drafts, notes, planning files, scripts,
  sources or working material here.
- The only files that belong in this repo are publishable site files: the HTML
  pages, `css/`, `js/`, `fonts/`, `images/`, `robots.txt`, `sitemap.xml`,
  `site.webmanifest`, `favicon.ico`, `apple-touch-icon.png`, `CNAME`,
  `.nojekyll`, `.gitignore`, `README.md`, `AGENTS.md`.
- Before any design or content task, read
  `../disce-internal/DESIGN-BRIEF.md` (binding visual/design reference).

## Stack

- Static HTML5 pages at the repository root (`index.html`, `philosophy.html`,
  `team.html`, `status.html`, `beta.html`, `waitlist.html`, `impressum.html`,
  `datenschutz.html`, plus `kernel.html` and `404.html`).
- `beta.html` is a minimal closed-beta placeholder. It is **not linked from the
  navigation yet**; do not add links to it without explicit approval.
- One shared stylesheet: `css/experimental.css`, minified to the committed
  `css/experimental.min.css` that the pages reference. `waitlist.html` carries
  its own inline styles.
- Vanilla JavaScript: `js/site.js`, the `js/generative/` modules, plus inline
  scripts in `waitlist.html`.
- No build system, package manager, framework, test runner, or CI. There is
  nothing to install or compile.

## Local preview

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000/>. Serve from the repository root; there is no
build step.

## Scope guardrail

Do not change product copy, headlines, CTAs, claims, translations, legal copy,
or content unless explicitly instructed.

## Dependency guardrail

Do not add dependencies, package managers, build tooling, CDNs, analytics, or
third-party services without explicit approval. Assets and fonts stay
self-hosted.

## Git guardrail

- One bounded task per commit.
- Never force-push.
- Do not commit generated files, local server artifacts, or secrets.
- Stage only files you can clearly identify as belonging to the current task.

## Image guardrail

Use only assets already committed to the repository. Do not generate, download,
or substitute images without explicit approval.

## Image pipeline

`scripts/optimize_images.py` in the private repo (`../disce-internal/scripts/`)
is the single image pipeline. It reads a master from this repo's `images/` and
writes responsive derivatives into `images/derived/`.

- **Masters are read-only.** Never edit or overwrite files in `images/`; crops
  and resizes live only in the generated derivatives.
- Run it with Pillow + `pillow-avif-plugin` installed *outside* the tree (not
  vendored, no project dependency).
- Outputs AVIF (primary) + WebP (fallback) at the requested widths, plus a
  ~24 px WebP LQIP placeholder. Never upscales past the master width.
- Budgets and asset classes follow `DESIGN-BRIEF.md` §9 (in the private repo).
- **Derivatives are committed.** GitHub Pages serves the tracked tree as-is, so
  `images/derived/` must be staged alongside the HTML/CSS that references it.

## Preview screenshots

`_screenshots/` is a local, ignored preview directory for rendered screenshots
and visual checks. It must never be committed; keep the tracked tree clean.

## Accessibility guardrail

Preserve keyboard access, visible focus states, and WCAG AA contrast.

## Ask first

Ask before making assumptions that affect product behavior, content, legal or
privacy matters, or deployment.

## Generative web visuals

Before planning, implementing, refactoring, or reviewing any Canvas, SVG motion,
CSS animation, WebGL, shader, particle, procedural, or scroll-linked visual, read
`../disce-internal/GENERATIVE_WEB_VISUALS_COMPETENCY.md` and
`../disce-internal/docs/generative-visuals/implementation-plan.md`.

A generative visual is an optional enhancement. It must be deletable without the
page losing meaning, its static/no-JS fallback is the current look of the
section, and it uses only existing CSS design tokens. State its user/product
purpose first; if none exists, propose a static or CSS/SVG alternative. Do not
add dependencies or a build step.
