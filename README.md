# रेललाइव · RailLive — Indian Railways Live Train Location

A self-contained static web app (one HTML file, no build step, no backend) covering the
**whole Indian Railways network** — live running status and full timetables for any train,
plus station-to-station search, multi-train live map and PNR. Styled in a traditional Indian
idiom (parchment, maroon and marigold palette, lotus/rangoli medallion, Devanagari titling).

## What it covers

- **Find trains** — search **every** train by name or number, or list direct trains between
  two station codes (sorted fastest / earliest).
- **Live status** — enter any train number: current position, delay, speed, next halt, ETA,
  a route schematic, and the **full station-by-station timetable** with actual times and
  platforms where reported. Cancellations/diversions are surfaced when present.
- **Live map** — the selected train's route with its reported position, or plot several
  trains at once on an OpenStreetMap basemap.
- **PNR** — real booking / passenger / chart status.
- Light/dark theme, auto-refresh every 60 s, offline sample fallback.

## Data source

Live data comes from the free, keyless **[TrainTrack](https://traintrack.stupidlabs.lol/)**
API (unofficial NTES-derived JSON). It is browser-callable, so the page fetches directly from
the visitor's browser — no backend, no API key.

| Purpose | Endpoint |
|---------|----------|
| Search trains | `GET /api/trains/search?q=` |
| Train info | `GET /api/trains/{n}/info` |
| Timetable / schedule | `GET /api/trains/{n}/schedule` |
| Live running status | `GET /api/trains/{n}/live` |
| Cancellations / diversions | `GET /api/trains/{n}/exceptions` |
| Trains between stations | `GET /api/trains/between?from=&to=&sort=` |
| Multi-train live tracking | `GET /api/map/tracking?trains=` |
| PNR status | `GET /api/pnr/{pnr}` |
| Station search / coordinates | `GET /api/station/autocomplete`, `/api/station/{code}/coordinates` |

A small built-in sample set is used only as an offline fallback if the service can't be reached.

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
- Fonts (Tiro Devanagari Hindi, Mukta, JetBrains Mono) and Leaflet load from CDNs; the map
  basemap needs internet.
- To point at a different provider, change the `API` constant near the top of the script.
