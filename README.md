# crew83.github.io

Website for Ruchi Crew Limited t/a CREW83 (https://crew83.com), built with [Hugo](https://gohugo.io/) — no theme, no JavaScript, one stylesheet.

- `content/_index.md` — all homepage copy (hero, "What we do") lives in the front matter.
- `hugo.toml` — site title, base URL, contact email and the legal footer line.
- `layouts/` — templates; `assets/css/main.css` — styles.

Run locally with `hugo server`.

## Deployment

Every push to `main` runs `.github/workflows/hugo.yaml`, which builds the site and uploads it over FTPS into `public_html` on the cPanel host. Configure it once in the GitHub repo under *Settings → Secrets and variables → Actions*:

| Kind     | Name             | Value                                                                   |
|----------|------------------|-------------------------------------------------------------------------|
| Secret   | `FTP_SERVER`     | FTP host from cPanel → *FTP Accounts* (e.g. `server211.web-hosting.com`) |
| Secret   | `FTP_USERNAME`   | The FTP account username                                                |
| Secret   | `FTP_PASSWORD`   | That account's password                                                 |
| Variable | `FTP_SERVER_DIR` | Optional. Defaults to `public_html/`; use `./` if the FTP account's home is already `public_html` |

Tip: create a dedicated FTP account in cPanel whose directory is `public_html`, so the deploy credentials can reach nothing else. The action uploads only changed files and never deletes anything it didn't upload.
