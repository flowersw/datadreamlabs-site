# datadreamlabs.com

Static one-page site for Will Flowers / DataDream Labs, served by GitHub Pages: `index.html` + `logo/`.

## Preview locally
```bash
cd ~/src/personal/datadreamlabs-site && python3 -m http.server 8000
```
Open http://127.0.0.1:8000. Edit, save, refresh. (Double-clicking `index.html` also works.)

## Writing
The blog stays on Medium (https://medium.com/@will-flwrs). The "Writing" section lists posts by hand: to add one, copy an `<li>` in `.posts` in `index.html`. Medium's RSS feed (`https://medium.com/feed/@will-flwrs`) can't be fetched from the browser on a static site, because Medium blocks cross-origin requests, so the list stays static.

## How this site is built
- `index.html` is generated. Don't hand-edit it. Edit `_variants/content.py` (every claim, role, skill, and tool link) and run `python3 _variants/build.py`.
- `_variants/` (git-ignored, never published) holds the content source, builder, prototypes, logo drafts, and `tower_logo.py`.
- Skills section: collapsed by default; searchable and sortable; tool links in each role open it pre-searched (`?q=Terraform#skills-fold`).

## Logo files (`logo/`)
- `mark-final-periwinkle.svg`: the site logo (night sky, sage masonry frame, ivory crescent moon, and a moon-side nested-spiral math constellation).
- `mark-original-periwinkle.svg`: the favicon (simple window, reads at 16–32px).
- `original-full-lockup.svg`: untouched original from the Wix logo kit.

## Deploy on GitHub Pages (personal account)
1. Create a public repo, e.g. `datadreamlabs-site`, on your **personal** GitHub account (not `will-flowers-pangia`).
2. Push this folder, then: repo **Settings → Pages → Source: Deploy from a branch → `main` / root**.
3. **Custom domain:** `datadreamlabs.com` (the `CNAME` file already says this). Tick **Enforce HTTPS** once the certificate issues (it can take up to an hour).

## Namecheap DNS (Domain List → datadreamlabs.com → Advanced DNS)
**Don't touch the MX records or any TXT records.** Your Google Workspace email depends on them.

Remove:
- the **URL Redirect** record for `@` (the Namecheap URL forward)
- the `www` CNAME pointing to `parkingpage.namecheap.com`

Add:
| Type | Host | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | `<your-github-username>.github.io.` |

Check: `dig +short datadreamlabs.com` should list the four 185.199.x.153 addresses, and `dig +short MX datadreamlabs.com` should still show `smtp.google.com`.
