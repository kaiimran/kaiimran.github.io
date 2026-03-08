# 📱 WA Tanpa Save Nombor

**WhatsApp someone without saving their number.**  
A lightweight, mobile-first PWA built for Malaysian phone numbers.

🔗 **Live site:** `https://kaiimran.github.io/`

---

## What it does

Paste any messy Malaysian phone number — copied from your call list, WhatsApp profile, or a message — and it cleans it up instantly and opens WhatsApp directly.

No sign-up. No backend. No number is ever stored or sent anywhere. Everything runs in your browser.

---

## Supported formats

All of these resolve to the same clean number:

| Input | Cleaned |
|---|---|
| `016 333 1111` | `60163331111` |
| `+60 16-333 1111` | `60163331111` |
| `016-333 1111` | `60163331111` |
| `163331111` | `60163331111` |
| `011-12345678` | `601112345678` |
| `011 1234 5678` | `601112345678` |

The cleaning logic handles:
- Spaces, dashes, brackets, `+` signs — stripped automatically
- Missing country code `60` — prepended automatically
- Leading `0` — replaced with `60`
- Already clean numbers — passed through unchanged

---

## Features

- 🇲🇾 **Malaysian number cleaning** — handles all common formats including 10 and 11-digit numbers
- 📋 **Paste button** — one tap to paste from clipboard, swaps to ✕ clear when field has content
- 🌐 **BM / EN toggle** — full Bahasa Malaysia and English UI
- 📲 **PWA** — installable on Android ("Install App") and iOS ("Add to Home Screen")
- ⚡ **Offline support** — service worker caches the app shell
- 🔒 **Private** — zero tracking, zero server, runs 100% client-side
- 🔙 **No orphan tabs** — uses `location.href` so pressing Back restores the app cleanly

---

## Files

```
├── index.html      # Main app (single file, no dependencies)
├── manifest.json   # PWA manifest for Android install
├── sw.js           # Service worker for offline + caching
└── icon.svg        # App icon (browser tab, home screen, PWA)
```

---

## Deploy to GitHub Pages

1. Fork or clone this repo
2. Go to **Settings → Pages**
3. Set source to `main` branch, `/ (root)`
4. Your site will be live at `https://yourusername.github.io/reponame/`

> If deploying to a subfolder (not root), update `"start_url"` in `manifest.json` to match your path.

---

## Install as an app

**iPhone (Safari)**
1. Open the site in Safari
2. Tap the Share icon **⬆**
3. Tap **"Add to Home Screen"**
4. Tap **Add**

**Android (Chrome)**
1. Open the site in Chrome
2. Tap the **"Install App"** button at the bottom of the card
3. Tap **Install**

---

## How the number cleaning works

```js
function clean(raw) {
  // 1. Strip everything except digits
  var d = raw.replace(/\D/g, '');

  // 2. Normalise country code
  if (d.startsWith('60'))      { /* already correct */ }
  else if (d.startsWith('0')) { d = '60' + d.slice(1); }
  else                        { d = '60' + d; }

  // 3. Validate local part is 7–10 digits
  var local = d.slice(2);
  if (local.length < 7 || local.length > 10) return null;

  return d;
}
```

---

## Tech stack

| | |
|---|---|
| **Framework** | None — vanilla HTML, CSS, JS |
| **Dependencies** | None — zero npm, zero CDN |
| **Hosting** | GitHub Pages (free) |
| **Size** | ~23 KB total |
| **Font** | System font stack (no external load) |

---

## License

MIT — free to use, modify, and deploy.
