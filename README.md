# designops-pbi-embed

Static host for the Power BI **Design Ops Dashboard** embed used at
[`https://design.manulife.ca/dashboard`](https://design.manulife.ca/dashboard).

Single-file HTML with inline CSS + JS, no build step. Auto-deployed to
Azure Static Web Apps on every push to `main`.

## Files

- `index.html` — the embed player (mirror of
  `verasda/pbi-dashboard:dashboard/pbi-embed/index.html`).
- `staticwebapp.config.json` — SWA response headers. `Content-Security-Policy: frame-ancestors`
  explicitly permits `design.manulife.ca`, `*.manulife.ca`, and Figma origins to
  iframe this site.

## Update flow

1. Edit `dashboard/pbi-embed/index.html` in the source repo.
2. Copy the file into this repo (`cp .../index.html ./index.html`).
3. `git commit -am 'update' && git push` — GitHub Actions redeploys within ~1 minute.

## URLs

- Repo: <https://github.com/davidveramanulife/designops-pbi-embed>
- SWA URL: *(fill in after Azure Portal creates the resource)*

## Config knobs (in `index.html`)

- `CONFIG.reportId` — Power BI report ID
- `CONFIG.groupId` — workspace ID
- `CONFIG.tenantId` — AAD tenant (Manulife)
- `CONFIG.pages` — array of `{ name, label }` for the top tab bar

If a page is added/removed in Power BI, update `CONFIG.pages` and push.
