# SEO Giveaway Landing Page — Deployment Guide

## Files to Deploy
Upload **only these two files** to your hosting root:

```
index.html
logo.png
```

Everything else lives in `_dev/` (source files, old versions) and `uploads/` (reference assets) — do NOT deploy those.

---

## Before You Go Live — Checklist

### 1. Set Your GoHighLevel Webhook URL
Open `index.html` and search for:
```
var GHL_WEBHOOK_URL = 'YOUR_GOHIGHLEVEL_WEBHOOK_URL_HERE';
```
Replace with your actual GHL webhook URL:
- In GoHighLevel: **Automations → New Workflow → Trigger: Webhook**
- Copy the webhook URL and paste it in place of the placeholder

### 2. Update the Canonical & OG URLs
Search for `oneclickdigital.net.au/seo-giveaway/` in `index.html` and replace with your actual page URL (appears in 4 places: `og:url`, `og:image`, `twitter:image`, `canonical`).

### 3. Create an OG Social Image
Create a `1200×630px` image (JPG) and upload it to your server at the path you set above (default: `/seo-giveaway/og-image.jpg`). This appears when the page is shared on Facebook, LinkedIn, etc.

### 4. Add a Favicon
`logo.png` is referenced as the favicon. Replace with a proper `favicon.ico` or a square PNG if needed.

### 5. Update the Webinar Date (if it changes)
Open `index.html` and find:
```javascript
var WEBINAR_DATE = new Date('2026-05-21T19:00:00+10:00');
```
Update the date/time/timezone if the webinar is rescheduled. Format: `YYYY-MM-DDTHH:MM:SS+HH:MM` (AEST = +10:00, AEDT = +11:00).

### 6. Add T&Cs and Privacy Policy Links
In the `Footer` section, find:
```javascript
h('a', {href: '#'}, 'Giveaway T&Cs'),
h('a', {href: '#'}, 'Privacy'),
```
Replace `'#'` with the actual URLs to your Terms & Conditions and Privacy Policy pages.

---

## Deployment Options

### Option A — Static Host (Recommended)
Works on any static host: **Netlify, Vercel, Cloudflare Pages, Kinsta Static Sites**

1. Drag and drop the two files (`index.html`, `logo.png`) into the host's dashboard, or
2. Push to a Git repo and connect it to the host

### Option B — WordPress (via cPanel / File Manager)
1. Upload `index.html` and `logo.png` to a subfolder, e.g. `/public_html/seo-giveaway/`
2. Access the page at `yourdomain.com/seo-giveaway/`

### Option C — Custom Domain via Netlify Drop
1. Go to [netlify.com/drop](https://app.netlify.com/drop)
2. Drag the two files — page is live in seconds with a Netlify URL
3. Set a custom domain in Netlify settings

---

## Performance Notes
- **No build step required.** `index.html` is fully self-contained.
- React and ReactDOM load from the unpkg CDN (production builds, ~44KB + 130KB gzipped). They are heavily cached by browsers after the first visit.
- Google Fonts load via a preconnected CDN link — cached after first visit.
- Total first-load payload (gzipped): ~250KB. Subsequent visits: ~20KB.

---

## Source Files (in `_dev/`)
| File | Purpose |
|------|---------|
| `app.jsx` | Original React source (JSX, development version) |
| `tweaks-panel.jsx` | Dev-only live-editing panel |
| `landing.html` | Original dev HTML shell (loads Babel + dev React) |
| `landing-bundle-src.html` | Previous bundled version |
| `landing-print.html` | Print/preview variant |
| `One Click Digital - SEO Giveaway Landing Page.html` | Bundler output (portable, offline) |
| `screenshots/` | Reference screenshots from design phase |
