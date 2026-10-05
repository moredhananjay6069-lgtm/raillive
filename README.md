# RailLive — Indian Railways Live Train Location

A self-contained static website (single HTML file, no build step, no backend) that
shows a live-style train-location dashboard for Indian Railways services.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The entire site — HTML, CSS and JavaScript inline. Open it directly in a browser. |
| `.nojekyll`  | Tells GitHub Pages to serve files as-is (no Jekyll processing). |
| `README.md`  | This file. |

## Run it locally

Just double-click `index.html`, or serve the folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy it permanently (free options)

### Option A — GitHub Pages
1. Create a new **public** repository, e.g. `raillive`.
2. Upload `index.html` and `.nojekyll` to the repository root.
3. Repo → **Settings → Pages** → *Source*: `Deploy from a branch`,
   *Branch*: `main` / `/ (root)` → **Save**.
4. After ~1 minute the site is live at:
   `https://<your-username>.github.io/raillive/`

### Option B — Netlify Drop (no account setup needed to start)
1. Go to <https://app.netlify.com/drop>.
2. Drag this whole folder onto the page.
3. You get an instant URL like `https://<random-name>.netlify.app`; claim it to keep it.

### Option C — Cloudflare Pages / Vercel
Both accept a folder upload or a connected Git repo and give a permanent
`*.pages.dev` / `*.vercel.app` URL.

## Connecting real live data

The page currently renders **representative sample data** baked into `index.html`
(see the `TRAINS` object). To make it authoritative, serve it from a small backend
that proxies a licensed live-status API (NTES or a rail-data provider) and returns
JSON in this shape — the UI then needs no changes:

```json
{
  "number": "12951",
  "name": "Mumbai Central – New Delhi Rajdhani Express",
  "from": "Mumbai Central",
  "to": "New Delhi",
  "days": "Daily",
  "delay": 18,
  "stations": [
    { "code": "MMCT", "name": "Mumbai Central", "dist": 0, "sched": "17:00", "dep": "17:00", "plat": "5", "halt": "—" }
  ]
}
```

A backend proxy is required because browser pages cannot call most rail-data APIs
directly (CORS) and must never hold an API key in client-side code.

## Notes

- Fonts (Space Grotesk, JetBrains Mono) load from Google Fonts; the page degrades
  gracefully to system fonts offline.
- Positions and delays are illustrative, not official.
