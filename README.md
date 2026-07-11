# Part3 — Berlin Hospital Density Map

This project generates a PMTiles vector tile package from Berlin neighborhood hospital count data and displays it in a browser with MapLibre GL JS.

## Files

- `create_pmtiles.sh`
  - Shell script that converts `neighborhoods_with_hospital_counts.geojson` into `hospital_with_counts.pmtiles` using Tippecanoe.
  - Includes standard TileJSON options for zoom range, feature limits, and layer naming.

- `hospital_with_counts.pmtiles`
  - Generated vector tile archive containing neighborhood hospital density geometry and properties.
  - Can be served directly over HTTP to MapLibre via the PMTiles protocol plugin.

- `index.html`
  - Browser map viewer that loads `hospital_with_counts.pmtiles` with MapLibre GL JS.
  - Visualizes hospital counts as a choropleth layer and provides popup interaction.

## Requirements

- `tippecanoe` installed and available on `PATH`
- A local HTTP server to serve `index.html` and `hospital_with_counts.pmtiles`
- Internet access for the MapLibre GL JS and PMTiles plugin CDN assets

## Usage

1. Ensure the GeoJSON source file exists in this folder.

2. Run the tile creation script:

   ```bash
   bash create_pmtiles.sh
   ```

3. Serve the folder locally and open the map:

   ```bash
   python3 -m http.server 8585
   ```

4. Open `http://localhost:8585/index.html` in a browser.

## Notes

- `index.html` is configured to load the PMTiles file from `http://localhost:8585/hospital_with_counts.pmtiles`.
- If you move the files, update the `pmtilesUrl` value in `index.html`.
- The map uses a free raster basemap and does not require an API key.

## Troubleshooting

- If `tippecanoe` is missing, install it from the official repository or use Docker.
- If `index.html` fails to load tiles, verify the local server is running and the PMTiles file is accessible.
