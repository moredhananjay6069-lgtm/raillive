# रेललाइव · RailLive — Indian Railways Live Train Location

A self-contained static web app (one HTML file, no build step, no backend) that shows
**real live running status** for Indian Railways trains, styled in a traditional Indian
idiom — a warm parchment, maroon and marigold palette, a lotus/rangoli medallion, a
textile-trim border, and Devanagari titling.

## Real live data, no key

Live data comes from the free, keyless **[TrainTrack](https://traintrack.stupidlabs.lol/)**
API (an unofficial NTES-derived JSON service). Because it is browser-callable, the page
fetches directly from the visitor's browser — there is no backend and no API key to manage.

- `GET /api/trains/{number}/schedule` — stops, times, distances, coordinates
- `GET /api/trains/{number}/live` — current position, delay, platforms
- `GET /api/trains/search?q=` — search by name or number
- `GET /api/pnr/{pnr}` — PNR status

Enter **any** train number and the dashboard, route schematic, map and timetable are built
from the real schedule and the latest reported position. A small built-in sample set is used
only as an offline fallback if the service cannot be reached.

## Features

- **Live status dashboard** — speed, last reported station, next halt, ETA, progress bar.
- **Route schematic** — vertical track map with the train's reported position.
- **Interactive map** — route on a Leaflet / OpenStreetMap basemap with a moving marker.
- **Station timetable** — actual times, delays, platforms and status where reported.
- **Train directory** — popular services, one click to load live.
- **Search modes** — Train (number or name), Station, and PNR.
- **Light/dark theme**, pause/scrub controls for the offline sample, auto-refresh every 60s.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The entire site — HTML, CSS and JavaScript inline. |
| `.nojekyll`  | Tells GitHub Pages to serve files as-is. |
| `README.md`  | This file. |

## Run locally

Open `index.html`, or serve the folder: `python3 -m http.server 8000`.

## Deploy (GitHub Pages)

Upload `index.html` and `.nojekyll` to a public repo → **Settings → Pages** → Source:
*Deploy from a branch*, `main` / `/ (root)`.

## Notes

- Live data is **unofficial** and may be delayed, incomplete or briefly unavailable. Always
  confirm travel-critical details via the official NTES / enquiry.indianrail.gov.in.
- Fonts (Tiro Devanagari Hindi, Mukta, JetBrains Mono) and Leaflet load from CDNs; the page
  degrades gracefully offline (the map basemap needs internet).
- To point at a different provider, change the `API` constant near the top of the script.
