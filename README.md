# WaSticker Website

Front-end prototype of the WaSticker web app. Everything lives in **one file, `index.html`** (inline CSS, inline JS, base64 images). No build step, no framework, no server.

- Live: https://uiuxdesignteam1-create.github.io/Wasticker-Website/
- Design: Figma "WA Sticker Website" (file `Cb50iRtT3EusV7pDZyynV1`)
  - Page **"WaSticker Web · Live v1"** = the full design of the live site: components, colour variables, text styles, desktop (1440) + mobile (390) screens
- Full handover notes: see the "WaSticker Website — Developer Handover" doc

## Run locally

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

## Check before pushing

```sh
node -e "const s=require('fs').readFileSync('index.html','utf8');for(const m of s.matchAll(/<script>([\s\S]*?)<\/script>/g))new Function(m[1]);console.log('ok')"
```

Push to `main` → GitHub Pages redeploys in about a minute. Phones cache hard: open with `?v=<anything>` to see a new deploy.

## How the code is organised

| Part | Where to look in `index.html` |
| --- | --- |
| Router | `render()` switches on `location.hash` |
| Pages | `pageSticker` / `wireSticker` (‹ › on the card edges = `.stp-edge`, swipe, ←/→ keys), `stPack(id)`, manager + `mypack-<id>` |
| State | global `S`, persisted by `save()` to `localStorage` keys `was_user`, `was_credits`, `was_mine`, `was_lib`, `was_blocked` (+ `sessionStorage` `was_appbar`) |
| Data | `PACKS` array; demo own pack MILO is `m0` |
| Menus | `menuSheet`, `shareSheet`, `reportModal`, `blockAsk`, `blockListModal`, `passModal`, `orderSheet` |
| Share + QR | `shareCore({qr})`, embedded `QRGEN` (MIT, Kazuhiko Arase) |
| Open in app | `getApp`, `openPlay`, `PLAY_URL`, `APP_SCHEME`, `appUrl`, desktop QR popup (`QR_APP`, `QR_PLAY`) |
| Icons | `I` (UI icons), `API` (popup icons from the app) |

## Routes

`home`, `home-faq`, `stickers`, `stickers-animated`, `stickers-static`, `categories`, `category-<slug>`, `popular`, `pack-<id>`, `sticker-<packId>-<n>`, `create`, `manager`, `saved` (Saved Packs), `mypack-<id>`, `search`, `pricing`, `tutorials`, `article-<slug>`, `signin`, `signup`, `contact`, `privacy`, `terms`.

## Demo only (needs a backend)

Sign in/up, credits, create/edit/delete packs, followers and sticker stats, report, block filtering, change password, order stickers. All of it is stored in the browser only.

## To finish

- [ ] Set `APP_SCHEME` / universal link so "Open in WaSticker" opens the app (empty now)
- [ ] Serve the site at `wasticker.io` — share links and QR codes already point there
- [ ] Confirm Play package `com.braincraftapps.droid.stickermaker`, then remove the "Soon" tags
- [ ] Move the 43 base64 images (≈5.8 MB file) out to real asset files / CDN
