# awestrucktech.github.io

Source for the Awestruck Tech portfolio site — a static site (no build step) listing our
Android apps, their Google Play links, individual privacy policies, terms of use, and the
`app-ads.txt` file used by AdMob.

Live site (once deployed): https://awestrucktech.github.io/

## Structure

```
index.html                 Homepage — app portfolio, about, contact
privacy/index.html         List of all privacy policies
privacy/*.html             One privacy policy per app
terms/index.html           Shared terms of use for all apps
app-ads.txt                AdMob app-ads.txt (served at site root)
robots.txt, sitemap.xml    Basic SEO
404.html                   Custom not-found page
assets/                    css/js/img shared by every page
```

## Deploying to GitHub Pages

1. Create a repo named exactly `awestrucktech.github.io` under the `awestrucktech` GitHub account
   (a user/org site repo — this is what makes the site serve from the domain root, which AdMob
   requires for `app-ads.txt`).
2. Push this folder's contents to the `main` branch.
3. In the repo Settings → Pages, set Source to "Deploy from a branch" → `main` / `root`
   (GitHub usually auto-detects this for a `<username>.github.io` repo).
4. Wait a few minutes, then confirm:
   - https://awestrucktech.github.io/ loads the homepage
   - https://awestrucktech.github.io/app-ads.txt returns the raw text file
5. In each app's Play Console listing, set the **Privacy Policy URL** to its page under `/privacy/`.
6. In AdMob, make sure each app's linked website matches `https://awestrucktech.github.io/`
   so Google can crawl `app-ads.txt` at the root.

## Adding a new app

1. Add a card to the `.app-grid` section in `index.html` (copy an existing `<article class="app-card">` block).
2. Copy `privacy/finbud.html` (or the closest existing app) as a starting point for the new
   app's `privacy/<app-slug>.html`, and update the package name, Play Store link, and any
   data-collection specifics that differ (permissions, accounts, ads).
3. Add the new policy to `privacy/index.html` and to `sitemap.xml`.
4. Link the new privacy policy page from the app's Play Console listing.

## Before publishing — please verify

The privacy policies were drafted from what's publicly knowable about each app (Play Store
descriptions, the `app-ads.txt` entry confirming AdMob, and typical permissions for this kind
of app). Before linking them from Play Console, double-check against your actual app builds:

- The permissions table in each policy matches what's declared in each app's `AndroidManifest.xml`.
- Whether any app uses analytics/crash tools beyond AdMob (e.g. Firebase Analytics, Crashlytics) —
  if so, add a line under "Advertising" / a new "Analytics" section naming them.
- FinBud's account/sync description matches how Google Sign-In and cloud sync actually work in the app.
