# Clever Humanizer — Floating Panel (Chrome extension v2.0.0)

A floating **"✦ Humanize"** button on every web page. Click it (or press
`Ctrl+Shift+H`) and a draggable panel opens *inside the page* with the
Clever Humanizer ready to use. Drag it by its blue header, resize it from
the bottom-right corner.

## How it works — please read this first

The panel is an iframe. Clever only lets its widget run on **websites you
register as allowed** in your widget settings, so the panel does NOT load
Clever directly. It loads a tiny **wrapper page that you host**, and that
wrapper page contains your official Clever widget. Chain:

`any web page → floating panel → YOUR wrapper page (allowed domain) → Clever widget`

There is a fallback in the panel header (**↗ Popup**) that opens the main
site in a popup window (that is v1's method) if anything in the chain fails.

## Setup — 3 steps

### Step 1 — Install the extension

1. Unzip this package and keep the folder somewhere permanent.
2. Chrome → `chrome://extensions` → turn on **Developer mode**.
3. **Load unpacked** → select the `clever-humanizer-panel` folder
   (the one containing `manifest.json`).
4. Open any normal web page — you should see the blue **✦ Humanize**
   button at the bottom-right. Clicking it now will try the main site
   directly and will probably show a blank frame — that is expected
   until Step 2 is done.

### Step 2 — Create your widget + host the wrapper (one time, ~10 min)

1. Sign up free at https://cleverhumanizer.ai/ and sign in.
2. In your profile, open the **API** page and create a **Humanizer widget**.
3. Host the wrapper: take `wrapper-hosting/index.html` from this package.
   Easiest free host: **GitHub Pages** — create a GitHub account/repo,
   upload the file as `index.html`, Settings → Pages → enable.
   (Netlify Drop also works: drag the folder onto netlify.com/drop.)
   Your wrapper address will look like `https://yourname.github.io/humanizer/`
4. Back in your Clever widget settings, add that host's domain
   (e.g. `yourname.github.io`) as an **allowed website**, and copy the
   widget **snippet** Clever gives you.
5. Edit your hosted `index.html`: paste the snippet exactly where the file
   says `PASTE YOUR CLEVER HUMANIZER WIDGET SNIPPET`, re-upload it, and
   open the wrapper address in a tab to check the widget appears there.
   If it does not appear on its own page, the panel will not fix it —
   the problem is the widget/allowed-domain setup.

### Step 3 — Point the panel at your wrapper

1. Right-click the extension icon → **Options** (or puzzle-piece → ⋯ → Options).
2. Paste your wrapper page's full public URL → **Save**.
3. Refresh any page, click **✦ Humanize** — your widget loads in the panel.
   Select text on a page → right-click → **"Humanize selected text
   (floating panel)"** copies it and opens the panel; press `Ctrl+V`
   inside the widget to paste. (No extension is allowed to type into
   another site's iframe, so paste is the one manual step.)

## Limits to know upfront

- Content scripts cannot run on `chrome://` pages, the Chrome Web Store,
  or a blank new tab — the button simply will not appear there.
  Use the toolbar icon / popup fallback on those.
- Some strict sites (banking, some corporate tools) block injected content;
  the popup fallback covers those.
- Keep the "Powered by Clever" line visible — it is part of the widget and
  Clever's terms for free use.

## Files

- `manifest.json`, `background.js` — Manifest V3 plumbing
- `content.js` — the floating button + draggable Shadow-DOM panel
- `options.html` / `options.js` — where the wrapper URL is saved
- `wrapper-hosting/index.html` — the page you host (Step 2)
- `icons/`

Version 2.0.0 — built 22 Nov 2026. Supersedes the v1 popup-window extension;
you can keep both installed, but they share the Ctrl+Shift+H shortcut, so
remove or disable one of them.
