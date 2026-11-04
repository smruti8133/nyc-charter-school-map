# NYC Charter Schools Map

An interactive map of charter-school locations across New York City's five boroughs. Click a numbered cluster to zoom in, then click a school marker to see its name and address.

**Live map:** https://smruti8133.github.io/nyc-charter-school-map/

## Data sources and tools

| Source / tool | How it's used | Why |
| --- | --- | --- |
| [New York State GIS — Charter K–12 (layer 3)](https://nysgeohub.ny.gov/arcgis/rest/services/Education/NYS_Schools/FeatureServer/3) | Supplies school names, physical addresses, counties, and coordinates | Official, charter-specific geographic data; no separate geocoding needed |
| [NYSED Charter Schools Directory](https://www.nysed.gov/charter-schools/charter-schools-directory) | Reference for school information (not queried by the map) | Independent official roster for context |
| [Leaflet](https://leafletjs.com/) | Displays the interactive map and school popups | Lightweight and suitable for a single HTML page |
| [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster) | Groups nearby markers | Makes dense areas easier to explore |
| [Esri World Street Map](https://server.arcgisonline.com/ArcGIS/rest/services/World_Street_Map/MapServer) | Supplies the street basemap | Adds geographic context |
| [unpkg](https://unpkg.com/) | Delivers the Leaflet libraries | No build step required |

## How it works

1. JavaScript requests GeoJSON school-location records from the NYS GIS Charter K–12 layer, filtered to NYC's five counties: Bronx, Kings, New York, Queens, and Richmond.
2. The browser checks that each record has a school name, a matching NYC county, and valid coordinates within a broad NYC-area range. It also checks for API errors and unexpected responses.
3. Valid locations are shown as clickable markers. Nearby markers are clustered to reduce overlap.

## Data coverage

The map includes charter-school networks throughout NYC, not only Success Academy. **School locations are not necessarily the same as distinct schools:** one school may operate at multiple sites. The displayed count represents valid location records returned by the GIS service, not a count of unique charter schools.

The state GIS layer is the live data source. The NYSED directory is listed as a reference, but this project does not automatically compare individual records against it. Data coverage and updates depend on the state service.
