# crew83.github.io

Website for Ruchi Crew Limited t/a CREW83, built with [Hugo](https://gohugo.io/) — no theme, no JavaScript, one stylesheet.

- `content/_index.md` — all homepage copy (hero, "What we do") lives in the front matter.
- `hugo.toml` — site title, contact email and the legal footer line.
- `layouts/` — templates; `assets/css/main.css` — styles.

Run locally with `hugo server`. Pushing to `main` deploys to GitHub Pages via `.github/workflows/hugo.yaml`.
