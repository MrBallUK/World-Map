# World Map

<img width="2481" height="1228" alt="image" src="https://github.com/user-attachments/assets/2d318a0d-0a95-40d1-be8b-b409329d0e97" />


Realtime world map clock with day/night shading, ISS tracking, live flights, aurora, and earthquakes.

This project is a single-page HTML5 canvas app (`index.html`) with no build step.

## Features

- Day/night Earth rendering with dynamic solar position
- Timezone ruler and dateline display
- ISS position and orbit path (live with fallback)
- Live flights (ADS-B) with:
  - provider fallback logic
  - military-only mode
  - location-aware local mode
  - hover and click flight popup with raw API fields
- Live aurora overlay (NOAA SWPC)
- Live earthquake overlay (USGS)
- Optional city labels and user location marker

## Data Sources

- ISS: `https://api.wheretheiss.at/v1/satellites/25544`
- Aurora: `https://services.swpc.noaa.gov/json/ovation_aurora_latest.json`
- Earthquakes: `https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_day.geojson`
- Flights:
  - `https://opensky-network.org/api/states/all` (global snapshot, rate-limited)
  - `https://api.airplanes.live/v2/point/{lat}/{lon}/{radius}` (fallback/local)
  - `https://api.airplanes.live/v2/mil` (military mode)

## Quick Start

1. Clone or download this repo.
2. Run a local static server from the project folder:

```bash
python -m http.server 8080
```

3. Open:

`http://localhost:8080/index.html`

Notes:
- Geolocation usually requires `https` or `localhost`.
- Opening `index.html` directly from disk may break some browser APIs.

## Controls

- `LAYERS` menu (top-right):
  - Live Aurora
  - Live Flights
  - Military Only
  - Show Cities
  - Use My Location
  - Global Earthquakes
- Hover flights to inspect details.
- Click flights to pin popup at cursor.
- Hover earthquakes for popup details.
- Press `T` to toggle timezone bands.
- Press `Esc` to close timezone panel.

## Project Structure

- `index.html` - main app (HTML/CSS/JS)

## Known Limitations

- Public APIs can rate-limit or temporarily fail.
- OpenSky often returns `429` without authentication.
- Military mode depends on airplanes.live availability.
- No backend caching/proxy, so browser CORS and endpoint uptime matter.

## Development Notes

- No framework, no bundler, no package manager.
- Main render loop and all logic live in one file for fast iteration.
- If you add new overlays, keep draw order in `draw()` consistent.
