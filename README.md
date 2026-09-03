# crew83.github.io

Website for Ruchi Crew Limited t/a CREW83, built with [Hugo](https://gohugo.io/) — no theme, no JavaScript, one stylesheet.

- `content/_index.md` — all homepage copy (hero, "What we do") lives in the front matter.
- `hugo.toml` — site title, contact email and the legal footer line.
- `layouts/` — templates; `assets/css/main.css` — styles.

Run locally with `hugo server`.

## Deployment

Every push to `main` runs `.github/workflows/hugo.yaml`, which builds the site once and deploys it to two places.

**GitHub Pages** — works out of the box once *Settings → Pages → Source* is set to **GitHub Actions**. Live at https://crew83.github.io/.

**cPanel hosting** — the built files are uploaded over FTPS into `public_html`, replacing a manual File Manager upload. To switch it on, in the GitHub repo go to *Settings → Secrets and variables → Actions* and add:

| Kind     | Name              | Value                                                        |
|----------|-------------------|--------------------------------------------------------------|
| Secret   | `FTP_SERVER`      | FTP host from cPanel → *FTP Accounts*                        |
| Secret   | `FTP_USERNAME`    | The FTP account username                                     |
| Secret   | `FTP_PASSWORD`    | That account's password                                      |
| Variable | `CPANEL_DEPLOY`   | `true` (set to anything else to pause cPanel deploys)        |
| Variable | `SITE_URL`        | Optional. Public URL of the hosted site; defaults to `https://crew83.com/` |
| Variable | `FTP_SERVER_DIR`  | Optional. Defaults to `public_html/`; set if the FTP account's root is already `public_html`, e.g. `./` |

Tip: create a dedicated FTP account in cPanel whose home directory is `public_html` so the deploy key can touch nothing else. The action only uploads changed files and never deletes anything it didn't put there.
