# PWA Implementation Instructions

This document contains step-by-step instructions for converting the CW Morse Trainer into a Progressive Web App (PWA).

## Estimated Time: 1-2 hours

## Prerequisites

- The app needs to be served over HTTPS (localhost works for testing)
- You'll need app icons in various sizes

---

## Step 1: Create Manifest File

Create `manifest.json` in the same directory as `index.html`:

```json
{
  "name": "CW Morse Trainer",
  "short_name": "CW Trainer",
  "description": "Passive Morse code listening practice tool",
  "start_url": "./index.html",
  "display": "standalone",
  "orientation": "portrait",
  "background_color": "#0a0a0a",
  "theme_color": "#FFBF00",
  "icons": [
    {
      "src": "icons/icon-72.png",
      "sizes": "72x72",
      "type": "image/png"
    },
    {
      "src": "icons/icon-96.png",
      "sizes": "96x96",
      "type": "image/png"
    },
    {
      "src": "icons/icon-128.png",
      "sizes": "128x128",
      "type": "image/png"
    },
    {
      "src": "icons/icon-144.png",
      "sizes": "144x144",
      "type": "image/png"
    },
    {
      "src": "icons/icon-152.png",
      "sizes": "152x152",
      "type": "image/png"
    },
    {
      "src": "icons/icon-192.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "any maskable"
    },
    {
      "src": "icons/icon-384.png",
      "sizes": "384x384",
      "type": "image/png"
    },
    {
      "src": "icons/icon-512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "any maskable"
    }
  ]
}
```

---

## Step 2: Create Service Worker

Create `sw.js` in the same directory:

```javascript
const CACHE_NAME = 'cw-trainer-v1';
const urlsToCache = [
  './index.html',
  './manifest.json'
];

// Install event - cache files
self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then((cache) => {
        console.log('Opened cache');
        return cache.addAll(urlsToCache);
      })
  );
  self.skipWaiting();
});

// Fetch event - serve from cache, fallback to network
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request)
      .then((response) => {
        // Cache hit - return response
        if (response) {
          return response;
        }
        return fetch(event.request);
      })
  );
});

// Activate event - clean up old caches
self.addEventListener('activate', (event) => {
  const cacheWhitelist = [CACHE_NAME];
  event.waitUntil(
    caches.keys().then((cacheNames) => {
      return Promise.all(
        cacheNames.map((cacheName) => {
          if (cacheWhitelist.indexOf(cacheName) === -1) {
            return caches.delete(cacheName);
          }
        })
      );
    })
  );
  self.clients.claim();
});
```

---

## Step 3: Update index.html

Add these changes to `index.html`:

### A. Add manifest link in `<head>` section (around line 5):

```html
<link rel="manifest" href="manifest.json">
<meta name="theme-color" content="#FFBF00">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="CW Trainer">
```

### B. Register service worker at the end of the `<script>` section (before closing `</script>` tag):

```javascript
// ============================================
// PWA SERVICE WORKER REGISTRATION
// ============================================

if ('serviceWorker' in navigator) {
    window.addEventListener('load', () => {
        navigator.serviceWorker.register('./sw.js')
            .then((registration) => {
                console.log('ServiceWorker registered:', registration.scope);
            })
            .catch((error) => {
                console.log('ServiceWorker registration failed:', error);
            });
    });
}
```

---

## Step 4: Create App Icons

Create an `icons/` directory and add PNG icons in these sizes:
- 72x72
- 96x96
- 128x128
- 144x144
- 152x152
- 192x192 (required)
- 384x384
- 512x512 (required)

**Icon Design Suggestion:**
- Terminal-style amber background (#FFBF00 or #0a0a0a)
- Morse code pattern (dots and dashes)
- Or stylized "CW" letters in monospace font

**Quick Icon Generation Options:**
1. Use online PWA icon generator (search "PWA icon generator")
2. Design in GIMP/Photoshop and export at different sizes
3. Use ImageMagick to batch resize: `convert icon.png -resize 192x192 icon-192.png`

---

## Step 5: Testing the PWA

### Local Testing:
1. Serve the app over HTTPS or use localhost
   - Python: `python -m http.server 8000`
   - Node.js: `npx http-server`
   - VSCode: Use Live Server extension

2. Open Chrome DevTools → Application tab
   - Check "Manifest" section
   - Check "Service Workers" section
   - Look for install prompt in address bar

3. Test on mobile device:
   - Chrome Android: Should show "Add to Home Screen" prompt
   - iOS Safari: Share → Add to Home Screen

### Features to Test:
- ✅ Offline functionality (disconnect network, app still works)
- ✅ Install to home screen
- ✅ Standalone mode (no browser UI)
- ✅ Audio playback in standalone mode
- ⚠️ Background audio (may not work on iOS)

---

## Step 6: Deployment

### Option A: GitHub Pages (Recommended - Free)
1. Create GitHub repository
2. Push files to repository
3. Enable GitHub Pages in Settings
4. Access via `https://username.github.io/repo-name/index.html`

### Option B: Other Free Hosts
- Netlify
- Vercel
- Cloudflare Pages

**Important:** All require HTTPS (which they provide automatically)

---

## Optional Enhancements

### Screen Wake Lock
Prevent screen from sleeping during practice:

```javascript
// Add this function
let wakeLock = null;

async function requestWakeLock() {
    if ('wakeLock' in navigator) {
        try {
            wakeLock = await navigator.wakeLock.request('screen');
            console.log('Wake Lock active');
        } catch (err) {
            console.log('Wake Lock error:', err);
        }
    }
}

// Call when starting playback
// requestWakeLock();
```

### Install Prompt
Show custom install button:

```javascript
let deferredPrompt;

window.addEventListener('beforeinstallprompt', (e) => {
    e.preventDefault();
    deferredPrompt = e;
    // Show custom install button
});

// On button click:
// deferredPrompt.prompt();
// const { outcome } = await deferredPrompt.userChoice;
```

---

## Troubleshooting

**"Service Worker registration failed"**
- Check that you're using HTTPS or localhost
- Check browser console for specific errors
- Verify sw.js path is correct

**"Add to Home Screen" not appearing**
- Manifest must be valid (check DevTools → Application → Manifest)
- All required icons must exist
- Must be served over HTTPS
- User must visit site at least twice (some browsers)

**Icons not showing**
- Verify icon paths in manifest.json
- Check that icon files exist in icons/ directory
- Clear browser cache and re-register service worker

**App not working offline**
- Check Service Worker is active in DevTools
- Verify files are cached (DevTools → Application → Cache Storage)
- Try unregistering and re-registering service worker

---

## Claude Implementation Prompt

If you want Claude to implement this, use this prompt:

```
Please convert the CW Morse Trainer into a Progressive Web App (PWA) by:

1. Creating manifest.json with app metadata and icon definitions
2. Creating sw.js service worker for offline caching
3. Adding manifest link and service worker registration to index.html
4. Creating placeholder icon files (or noting that I need to add them)

Use the specifications in pwa-instructions.md as reference.
Keep the OK1TRL amber terminal theme (#FFBF00 on #0a0a0a) for the PWA metadata.
```

---

## Version Updates

When updating the app after PWA deployment:

1. Increment `CACHE_NAME` in sw.js (e.g., 'cw-trainer-v2')
2. Service worker will auto-update on next visit
3. Users will get new version automatically

---

**Estimated Total Time:**
- Manifest & Service Worker: 30 minutes
- Icon creation: 30-60 minutes
- Testing & debugging: 30 minutes
- Deployment: 15 minutes

**Total: 1.5-2.5 hours**
