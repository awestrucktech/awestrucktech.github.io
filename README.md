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

See [PUBLISHING.md](PUBLISHING.md) for the full step-by-step: creating the repo, pushing,
enabling Pages, verifying the live URLs, and linking privacy policies from Play Console.

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
- FinBud's policy states it is fully offline with no data collection, no ads, and no sign-in —
  confirm the shipped app has no hidden SDK (analytics, crash reporting, ads) before publishing,
  since that claim needs to stay true for the policy to remain accurate.
