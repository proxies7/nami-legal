# Nami Accounting — legal pages for Google OAuth publishing

Three static pages, no build step, no external assets. Upload the folder as-is.

## Field-by-field: OAuth consent screen → App domain

| Console field | Value (after hosting — see below) |
|---|---|
| Application home page | `https://<your-host>/` |
| Application privacy policy link | `https://<your-host>/privacy.html` |
| Application terms of service link | `https://<your-host>/terms.html` |
| Authorized domains | `<your-host>` only — no `https://`, no path |

Example with GitHub Pages user `proxies7` and repo `nami-legal`:

```
Application home page           https://proxies7.github.io/nami-legal/
Application privacy policy link https://proxies7.github.io/nami-legal/privacy.html
Application terms of service    https://proxies7.github.io/nami-legal/terms.html
Authorized domains              proxies7.github.io
```

`proxies7.github.io` is acceptable as an authorized domain because `github.io` is on the
Public Suffix List, so the *subdomain* is the registrable domain. Same rule for
`*.netlify.app`, `*.pages.dev`, `*.web.app`.

## Hosting route A — GitHub Pages (5 min, no terminal)

1. github.com → **New repository** → name `nami-legal` → **Public** → Create.
2. **Add file → Upload files** → drag `index.html`, `privacy.html`, `terms.html` → Commit.
3. **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main`, folder `/ (root)` → Save.
4. Wait ~1 min, reload Settings → Pages; the URL appears. Open all three links in a private window
   to confirm they load without login.

## Hosting route B — Netlify Drop (fastest, no repo)

1. app.netlify.com/drop → drag this whole folder.
2. Claim the site with your account so the URL is permanent (`https://<name>.netlify.app`).
3. Authorized domain: `<name>.netlify.app`.

## Hosting route C — your own domain

If a domain you own already has a website (mila-grand / roof-rawai / etc.), put the three files in a
subfolder such as `/legal/` and use that domain as the authorized domain. This is the cleanest for
verification later, since Google verifies domain ownership by DNS or Search Console.

## After the fields are saved

- Click **Publish app** on the OAuth consent screen / Audience page.
- Status becomes *In production* → refresh tokens stop expiring after 7 days.
- With Drive/Sheets/Docs scopes the app stays **unverified**: the consent screen shows
  "Google hasn't verified this app" → *Advanced* → *Go to Nami Accounting (unsafe)*. For a
  single-user tool that is expected. Submitting for verification removes the warning and lifts
  the 100-user cap, but it is not required to run this pipeline.
- Do not remove the redirect URI `http://localhost:1` — the setup script depends on it.
