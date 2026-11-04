# NYC Charter Schools Map

An interactive map of charter school locations across New York City's five boroughs. Nearby locations are grouped into clusters; zoom in or click a cluster to reveal individual markers, then click a marker to view the school's name and address.

## View the map

Open `index.html` in a browser with an internet connection. The site can also be hosted as a static page using **GitHub Pages** (repository **Settings → Pages → Deploy from a branch → main / root**).

## Data sources and dependencies

| Resource | Role | Why it was used |
| --- | --- | --- |
| [New York State GIS school locations — NYS Schools, layer 3](https://nysgeohub.ny.gov/arcgis/rest/services/Education/NYS_Schools/FeatureServer/3) | School names, physical addresses, county labels, and coordinates | A public state geospatial data service provides structured school-location records, avoiding manual address collection and geocoding. The map requests its ArcGIS REST `query` endpoint as GeoJSON when the page loads. |
| [Esri World Street Map](https://www.arcgis.com/home/item.html?id=3b93337983e9436f8db950e38a8629af) | Background map tiles | Supplies recognizable roads, neighborhoods, and geographic context so users can understand where schools are located. |
| [Leaflet 1.9.4](https://leafletjs.com/) | Interactive map, zooming, markers, and popups | Lightweight, open-source mapping library that works in a single HTML file without a frontend build process. |
| [Leaflet.markercluster 1.5.3](https://github.com/Leaflet/Leaflet.markercluster) | Groups nearby markers | Keeps dense areas readable while preserving access to individual schools as users zoom in. |
| [unpkg](https://unpkg.com/) | Delivers Leaflet and markercluster JavaScript/CSS | Loads the libraries from a CDN, keeping the repository small and setup simple. |

The map also includes the standard **OpenStreetMap contributors** attribution shown with the map, where applicable; school locations are supplied by New York State, not OpenStreetMap.

## How it works

1. On page load, the browser requests GeoJSON school records from the New York State ArcGIS REST service.
2. The application keeps records whose county is **Bronx, Kings, New York, Queens, or Richmond**, and whose coordinates fall within a broad NYC geographic range.
3. Each matching record becomes a map marker with the school name and physical address in a popup.
4. Leaflet.markercluster groups nearby markers at lower zoom levels. The displayed location count reflects the matching records returned by the live service.

## Implementation choices

- **Simple static HTML:** No framework, server, account, or build step is needed for this small mapping task.
- **Live public data:** The map reads directly from the state service instead of maintaining a manually copied list. As a result, the number of displayed locations may change when the service's records change.
- **Existing mapping tools:** Leaflet, the clustering plugin, and Esri tiles cover the core mapping needs without building custom geographic functionality.
- **Minimal scope:** The interface focuses on viewing school locations rather than adding search, filters, or AI features that are not necessary for the requested map.

## Requirements and limitations

An internet connection is required to load the school data, map tiles, and CDN-hosted libraries. Availability and completeness depend on the state service and the fields it returns. The map does not independently audit the statewide dataset or guarantee that every currently operating charter-school site is represented.

No project API key is configured for the map tile endpoint used in `index.html`.
