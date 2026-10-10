# POTA Spotter

A single-page sign display for live [Parks on the Air](https://parksontheair.com) (POTA) activator spots in one US state (Michigan by default). Built for a 1080 x 1920 portrait screen: a large dark map on top, a table of callsigns below.

**Version 1.1.0**

## Features

- **Live spots:** polls the POTA activator feed every 3 minutes.
- **Map:** Leaflet with Esri World Dark Gray tiles, fitted to the selected state. Each spot is a tree icon with the activator callsign, park name and park reference (`US-xxxx`).
- **On Air / QRT:** a spot is On Air while it is in the POTA feed. When it drops out it becomes QRT (gray, no pulse) and stays on screen for 20 minutes.
- **Crowded areas:** spots that would overlap are collapsed into a small table joined to their trees by lines. Several callsigns at one park are handled the same way. When several parks share a table, each park gets its own color on its tree, line and table rows. A QRT spot that would overlap an On Air spot is removed from the map (it stays in the list).
- **Change Location:** pick any US state (plus DC) from a list or use the browser's location, and filter by operating mode: CW, DATA (DATA, FT4, FT8) or PHONE (PHONE, SSB). Choices are saved in the browser.
- **List:** every callsign with park, reference, frequency, mode and status.

## Quick start

There is no build step. Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8080
# then visit http://localhost:8080
```

### GitHub Pages

1. Push this repo to GitHub.
2. Go to **Settings > Pages**, choose the `main` branch and the root folder.
3. Open `https://<your-username>.github.io/<repo-name>/` on the sign's browser.

Pages serves over HTTPS, which the browser needs before it allows the **Use My Location** button.

## Configuration

Constants are at the top of the script in `index.html`:

| Name | Purpose | Default |
| --- | --- | --- |
| `POLL_MS` | Spot refresh interval | 3 minutes |
| `INACTIVE_MS` | How long QRT spots are kept | 20 minutes |
| `MAX_ROWS` | Rows shown in the list | 11 |
| `MODE_GROUPS` | Operating mode filter groups | CW, DATA, PHONE |
| `STATES` | State names and map bounds | 50 states + DC |
| `CLUSTER_COLORS` | Colors for parks that share a table | 8 colors |

## Notes and limits

- Modes outside the three filter groups (for example FM) are always shown.
- Overlap detection estimates label sizes rather than measuring text, so it may group slightly early or late.
- State map bounds are approximate.
- Status comes only from the spot being present in the feed. It does not read the spot's expiry or comments.
- The page needs internet access to `api.pota.app`, Esri, OpenStreetMap Nominatim and cdnjs.

## Data and credits

- Spots: [POTA API](https://docs.pota.app/)
- Map tiles: Esri, via [Leaflet](https://leafletjs.com)
- Location lookup: [OpenStreetMap Nominatim](https://nominatim.org) (light use only, per its usage policy)
- Fonts: Oswald and Source Sans Pro from Google Fonts

## Author

Jim Davis - N8JRD (vibe coded with Claude) 2026

## License

[MIT](LICENSE)
