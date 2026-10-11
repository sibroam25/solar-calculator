# Solar Calculator: launch guide

This folder is the whole product. It is both a **website** and an **installable app** (a PWA).

| File | What it does |
|---|---|
| `index.html` | The calculator itself |
| `manifest.webmanifest` | Gives it a name, icon and colours when installed |
| `sw.js` | Saves the app on the phone so it works with no internet |
| `icons/` | App icons (normal, maskable for Android, Apple) |
| `_headers` | Hosting settings for Netlify and Cloudflare Pages |

Keep all of these together in one folder. Do not rename `index.html`.

## 1. Test it on your computer first (2 minutes)

Offline mode only works over a web address, not by double-clicking the file. In this folder run:

    python3 -m http.server 8000

Open http://localhost:8000 in Chrome. In the address bar you should see an install icon. In DevTools (F12), Application tab, you can confirm the manifest and service worker.
(Double-clicking `index.html` still works as a plain calculator, just without install and offline.)

## 2. Put the website online (free)

Pick one. Each gives you a secure `https://` link, which installing needs.

**Netlify (easiest).** Go to app.netlify.com/drop, sign up, and drag this whole folder onto the page. You get a link like `random-name.netlify.app`. Rename it under Site settings, Change site name.

**Cloudflare Pages.** Workers and Pages, Create, Pages, Upload assets, upload this folder.

**GitHub Pages.** Create a repository, upload these files, then Settings, Pages, deploy from the main branch. Your link will look like `yourname.github.io/solar-calculator/`. Every path in this package is relative, so the subfolder link works.

Optional: buy a domain (a `.ng` or `.com`) and connect it in the host's Domains section.

## 3. How people install it as an app

- **Android (Chrome):** open your link, tap **Install app** at the top of the page (or the browser menu, then Install app).
- **iPhone (Safari):** open the link, tap Share, then **Add to Home Screen**. The page shows this hint once.
- **Laptop (Chrome or Edge):** click the install icon in the address bar.

After installing, it has a home-screen icon, opens full screen and works offline.

## 4. Updating the app later

Edit `index.html`, upload the folder again to the same site. Users get the new version the next time they open the app online (it refreshes in the background, so it may show on the second open). To push a change to everyone immediately, change `solar-calc-v1` to `solar-calc-v2` in `sw.js`.

## 5. Putting it in the Google Play Store (optional)

1. Put the website online first (step 2). Note your final `https://` link.
2. Go to **pwabuilder.com**, paste your link and let it check the app.
3. Choose **Package for stores, Android**. Pick a package ID such as `com.yourname.solarcalc`. PWABuilder produces the Android package and a signing key. **Back up the signing key. If you lose it you cannot update the app.**
4. PWABuilder also gives you a `assetlinks.json` file. Upload it to your site at `/.well-known/assetlinks.json`. This links the app to your website and hides the browser address bar.
5. Create a Google Play Console account (one-time $25 fee). Upload the `.aab` file and complete the store listing: icon, screenshots, description and a short privacy policy. A one-page policy saying "this app stores your appliance list on your phone only and sends nothing anywhere" is accurate for this app.
6. A new personal account must run a closed test with 12 testers for 14 days before it can go to production. An organization account does not have this step.

PWABuilder's screens change over time, so follow what it shows you if it differs from the steps above.

**Sharing a file directly (no store):** PWABuilder's Android package for testing is an `.apk` you can send on WhatsApp. People must allow "install from unknown sources" to open it.

## 6. iPhone App Store

It costs $99 a year and needs a Mac. Apple may also reject apps that are only a website in a wrapper. The installable website already works on iPhone, so leave this for later.
