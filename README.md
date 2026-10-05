# रेललाइव · RailLive — Indian Railways Live Train Location

A self-contained static web app (one HTML file, no build step, no backend) that shows a
live train-location dashboard for Indian Railways services, styled in a traditional
Indian visual idiom — a warm parchment/maroon-and-marigold palette, a lotus/rangoli
medallion, a textile-trim border, and Devanagari titling.

## Features

- **Live status dashboard** — current speed, last reported station, next halt, ETA,
  a journey progress bar and a simulated IST clock.
- **Route schematic** — a vertical track map with the train marker moving between stations.
- **Interactive map** — the route drawn on a Leaflet / OpenStreetMap basemap with station
  markers and a moving train marker.
- **Station timetable** — arr/dep, platform, halt, distance and status pills, with delay
  propagated to downstream stops.
- **Train directory** — browse all services in the dataset and load any one.
- **Search modes** — Train (number or name), Station (name or code → trains passing through),
  and PNR (10-digit lookup).
- **Live data option** — paste a RapidAPI key to pull real running status directly from the
  browser (see below). Falls back to the demo feed automatically.
- **Controls** — pause/play, 1×–30× speed, scrub slider, and a light/dark theme toggle.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The entire site — HTML, CSS and JavaScript inline. |
| `.nojekyll`  | Tells GitHub Pages to serve files as-is. |
| `README.md`  | This file. |

## Run locally

Open `index.html` directly, or serve the folder:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## Deploy (GitHub Pages)

1. Upload `index.html` and `.nojekyll` to a public repository.
2. Repo → **Settings → Pages** → Source: *Deploy from a branch*, Branch: `main` / `/ (root)`.
3. The site goes live at `https://<username>.github.io/<repo>/`.

## Using real live data

The page ships with a **demo feed** (representative timetables — positions and delays are
illustrative, not official). To use real data:

1. Get a key for an Indian Railways live-status API on RapidAPI — the build targets the
   *Indian Railway IRCTC* API (`indian-railway-irctc.p.rapidapi.com`,
   `GET /api/trains/v1/train/status`).
2. Click the gear icon (**Live data settings**) in the site header.
3. Paste the RapidAPI key (and host/path if you use a different provider) and save.

The key is stored only in your browser's `localStorage` — it is never written into the
page source or committed to the repository. Because RapidAPI endpoints send CORS headers,
the request is made directly from the browser; there is no backend.

**Note:** the default `applyLive()` handler prints the provider's raw response fields so you
can map your exact provider shape. Adjust `applyLive()` in `index.html` to bind the response
to the UI once you know the field names your provider returns.

## Notes

- Fonts (Tiro Devanagari Hindi, Mukta, JetBrains Mono) and Leaflet load from CDNs; the page
  degrades gracefully offline (the map basemap will not load without internet).
- Always cross-check against the official NTES / enquiry.indianrail.gov.in before travel.
