# crew83/website

Website for CREW83 (crew83.com), built with [Hugo](https://gohugo.io/) — no theme, no JavaScript, one stylesheet.

## Pages

| URL          | Source                | Notes |
|--------------|-----------------------|-------|
| `/`          | `content/_index.md`   | Homepage. All copy (hero, "What we do" cards) lives in the front matter; rendered by `layouts/home.html`. |
| `/services/` | `content/services.md` | "What we do" in full: the three stages (Find the problem, Build the solution, Create the product), what runs across every stage, and how an engagement works. |
| `/about/`    | `content/about.md`    | What we do, who for, and how we're different. |
| `/404.html`  | `layouts/404.html`    | Not-found page. |

`/services/` and `/about/` are plain Markdown (with a little inline HTML for the two-column "pairs" and the closing call to action) rendered by `layouts/page.html`. Any new `content/<name>.md` gets the same treatment at `/<name>/`.

The three homepage cards link to the matching section on `/services/` (`#find-the-problem`, `#build-the-solution`, `#create-the-product`). The anchor is derived from the card title, so if you rename a stage in `_index.md`, rename the matching `<h2 id="…">` in `services.md` too.

## Navigation

Header: **Home · What we do · About · Contact** (Contact is a `mailto:` link). Footer: **Home · What we do · About**, with the contact email underneath, then the legal line and copyright. Both menus are hard-coded in `layouts/_partials/header.html` and `footer.html`.

## Where things are set

- `hugo.toml` — site title, base URL, meta description, contact email (`params.email`, used by every Contact / Get in touch link) and the legal footer line (`params.legal`).
- `layouts/` — `baseof.html` (page shell), `home.html`, `page.html`, `404.html`, and the header/footer partials.
- `assets/css/main.css` — all styling; minified and fingerprinted by Hugo at build time.
- `assets/favicon.ico` — site icon.

## Working locally

Requires Hugo (extended not needed). Run `hugo server` and open http://localhost:1313/. A production build is `hugo --gc --minify`, output in `public/` (git-ignored).

## Deployment

Every push to `main` runs `.github/workflows/hugo.yaml`, which builds the site and uploads it over FTPS into `public_html` on the cPanel host. Configure it once in the GitHub repo under *Settings → Secrets and variables → Actions*:

| Kind     | Name             | Value                                                                   |
|----------|------------------|-------------------------------------------------------------------------|
| Secret   | `FTP_SERVER`     | FTP host from cPanel → *FTP Accounts*                                   |
| Secret   | `FTP_USERNAME`   | The FTP account username, in the full form cPanel shows                 |
| Secret   | `FTP_PASSWORD`   | That account's password                                                 |
| Variable | `FTP_SERVER_DIR` | Optional. Defaults to `public_html/`; use `./` if the FTP account's home is already `public_html` |

Tip: create a dedicated FTP account in cPanel whose directory is `public_html`, so the deploy credentials can reach nothing else. The action uploads only changed files and never deletes anything it didn't upload. A failed run can be retried from the Actions tab with *Re-run failed jobs* — no new commit needed.
