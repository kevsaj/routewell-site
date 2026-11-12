# routewell.ca

Static marketing site for Routewell. Plain HTML and one CSS file, no build step. Hosted free on GitHub Pages.

## Pages

| URL | File | Purpose |
|---|---|---|
| `/` | `index.html` | Home: pitch, three packages, Process Check, care plan, how it works, about, FAQ |
| `/demo/` | `demo/index.html` | One demo video per package. Linked from every cold email. |
| `/process-check/` | `process-check/index.html` | The $250 paid entry offer (email 2 of the sequence) |
| `/industries/accounting-law/` | `industries/accounting-law/index.html` | Landing page for accounting, bookkeeping and law firms (link from cold emails to that list) |
| `/industries/construction-trades/` | `industries/construction-trades/index.html` | Landing page for construction, engineering and trades |
| `/partners/` | `partners/index.html` | White-label pitch for MSPs |
| `/book/` | `book/index.html` | Booking page. Every "Book a call" button points here. |
| `/privacy/` | `privacy/index.html` | Short privacy notice |
| 404 | `404.html` | Not-found page |

Shared styles: `assets/site.css`. Phone menu toggle: `assets/site.js`. Link-preview image: `assets/og.png` (1200×630). Search markup (JSON-LD) is in the `<head>` of the home and industry pages; if you change prices or FAQ answers, update it there too. Header and footer are repeated in each page; if you change the nav, change it in every `index.html`.

## Placeholders to fill (search for these comments)

- `BOOKING LINK` in `book/index.html`: replace the `mailto:` with the Microsoft Bookings URL.
- `DEMO VIDEO` in `index.html` and `demo/index.html`: swap each placeholder for
  `<div class="video-frame"><video src="/assets/approval-flow.mp4" controls playsinline preload="metadata"></video></div>`
  or a YouTube (unlisted) embed. Keep files under ~20 MB; GitHub rejects files over 100 MB.
- `PHOTO` in `index.html`: add `assets/kevin.jpg` (square, ~400 px) and use `<img class="avatar" src="/assets/kevin.jpg" alt="Kevin, founder of Routewell">`.

## Run locally

```
python3 -m http.server 8000
```

Then open http://localhost:8000. Links are root-relative (`/demo/`), so open through the server, not as a file.

## Deploy (GitHub Pages)

1. Repo Settings → Pages → Source: "Deploy from a branch", branch `main`, folder `/ (root)`.
2. Custom domain: `routewell.ca` (the `CNAME` file already says this). Tick "Enforce HTTPS" once the certificate is issued (can take up to an hour).
3. GoDaddy → routewell.ca → DNS. Delete any existing `A` record for `@` (GoDaddy's parked page) and add:

| Type | Name | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | kevsaj.github.io |

Leave MX, SPF (TXT), autodiscover and DKIM records for Microsoft 365 email alone; they do not conflict with these.
