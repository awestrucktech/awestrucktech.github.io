# Publishing this site to GitHub Pages

This repo is set up as a **user site**, which is the type GitHub Pages serves directly at
the root of `https://awestrucktech.github.io/` — required so `app-ads.txt` and the privacy
policy pages resolve at clean, permanent URLs you can paste into AdMob and Play Console.

## 1. Create the GitHub repository

1. Sign in to GitHub as the **`awestrucktech`** account (the one you gave as your GitHub
   username).
2. Go to [github.com/new](https://github.com/new).
3. Repository name must be **exactly**: `awestrucktech.github.io`
   (this exact name is what makes GitHub treat it as a user/org Pages site, served from
   the domain root instead of a `/reponame/` subpath).
4. Set visibility to **Public** (GitHub Pages user sites must be public on free plans).
5. Do **not** initialize with a README, .gitignore, or license — this local folder already
   has everything, and adding files on GitHub first will create conflicting history.
6. Click **Create repository**.

## 2. Push this local repo to GitHub

This folder is already a git repo with the site committed locally. From
`C:\suresh\apps\awestrucktech`, run:

```bash
git remote add origin https://github.com/awestrucktech/awestrucktech.github.io.git
git push -u origin main
```

You'll be prompted to authenticate — use a GitHub personal access token as the password
(GitHub no longer accepts account passwords over HTTPS), or push via SSH if you have an
SSH key set up on that account:

```bash
git remote set-url origin git@github.com:awestrucktech/awestrucktech.github.io.git
git push -u origin main
```

## 3. Enable GitHub Pages

1. On GitHub, open the `awestrucktech.github.io` repo → **Settings** → **Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Under **Branch**, choose `main` and folder `/ (root)`, then **Save**.
4. GitHub will show a banner "Your site is live at https://awestrucktech.github.io/" once
   the first deployment finishes (usually 1–2 minutes). You can watch progress under the
   repo's **Actions** tab.

## 4. Verify the deployed site

Once live, check each of these load correctly:

- `https://awestrucktech.github.io/` — homepage
- `https://awestrucktech.github.io/app-ads.txt` — must return the raw text (not HTML)
- `https://awestrucktech.github.io/privacy/podcast-player.html`
- `https://awestrucktech.github.io/privacy/malayalam-radio.html`
- `https://awestrucktech.github.io/privacy/hindi-radio.html`
- `https://awestrucktech.github.io/privacy/tamil-radio.html`
- `https://awestrucktech.github.io/privacy/australia-radio.html`
- `https://awestrucktech.github.io/privacy/finbud.html`
- `https://awestrucktech.github.io/terms/`

If a page 404s, double-check the file was actually pushed (`git log --stat`) and that
Pages is building from the `main` branch root, not a `docs/` folder.

## 5. Link the privacy policies from Play Console

For each app, in **Google Play Console → [App] → Policy → App content → Privacy policy**,
paste its corresponding URL from the list above, then save and (if prompted) resubmit for
review.

## 6. Confirm AdMob picks up app-ads.txt

1. In **AdMob → Apps → [App] → App settings**, make sure each app's **App URL / website**
   points to `https://awestrucktech.github.io/` (or the app's own page if you later add one)
   so Google's crawler checks the right domain for `app-ads.txt`.
2. In **AdMob → Blog / app-ads.txt status** (or the warning banner on the Apps list), it can
   take **Google up to ~24 hours** to re-crawl and clear an "Unauthorized sellers" warning
   after the file goes live — this is normal, no action needed once the file is reachable.
3. You can manually verify Google can see it with:
   ```bash
   curl -s https://awestrucktech.github.io/app-ads.txt
   ```
   It should print exactly: `google.com, pub-1302968271378900, DIRECT, f08c47fec0942fa0`

## 7. Future updates

Any time you edit files locally, publish changes with:

```bash
git add -A
git commit -m "describe the change"
git push
```

GitHub Pages redeploys automatically within a minute or two of each push to `main`.

## Optional: custom domain

If you later buy a domain (e.g. `awestrucktech.com`) and want the site there instead:

1. Add a `CNAME` file at the repo root containing just the domain, e.g. `awestrucktech.com`.
2. At your domain registrar, add a `CNAME` record pointing `www` (or an `A`/`ALIAS` record
   for the apex domain) to `awestrucktech.github.io` — see
   [GitHub's custom domain docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
   for the exact DNS records GitHub currently requires.
3. Re-check `https://<yourdomain>/app-ads.txt` and update the "App URL / website" in AdMob
   and the Play Console privacy policy links to the new domain.
