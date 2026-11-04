# NYC Charter Schools Map

An interactive map of charter-school locations across New York City's five boroughs. Click a numbered cluster to zoom in, then click a school marker to see its name and address.

**Live map:** https://smruti8133.github.io/nyc-charter-school-map/

## Problem Statement

**Target users:** Parents and guardians exploring charter-school options for their children in NYC.

With hundreds of charter-school locations across NYC's five boroughs, understanding where schools are located and exploring available options can be challenging without a centralized geographic view.

**Goal:** Create an interactive map that helps users visualize school locations, explore schools across boroughs, and access basic information such as school names and addresses.

## MVP Priorities

Given the one-hour time constraint, I focused on three priorities:

1. **Coverage:** Display charter-school locations across all five boroughs using New York State GIS data.
2. **Reliability:** Validate school names, counties, and coordinates before displaying locations.
3. **Usability:** Use interactive markers and clustering to make hundreds of locations easy to explore.

These features directly address the core goal of making school locations accessible without adding unnecessary complexity.

## Data sources and tools

| Source / tool | How it's used | Why |
| --- | --- | --- |
| [New York State GIS — Charter K–12 (layer 3)](https://nysgeohub.ny.gov/arcgis/rest/services/Education/NYS_Schools/FeatureServer/3) | Supplies school names, physical addresses, counties, and coordinates | Official charter-specific geographic data; no separate geocoding needed |
| [Leaflet](https://leafletjs.com/) | Displays the interactive map and school popups | Lightweight and suitable for a single HTML page |
| [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster) | Groups nearby markers | Makes dense areas easier to explore |
| [Esri World Street Map](https://server.arcgisonline.com/ArcGIS/rest/services/World_Street_Map/MapServer) | Supplies the street basemap | Adds geographic context |
| [unpkg](https://unpkg.com/) | Delivers the Leaflet libraries | No build step required |

## How it works

1. On page load, the browser requests GeoJSON school records from the New York State ArcGIS REST service, filtered to NYC's five counties.
2. The application validates school names, geographic coordinates, and county information to ensure records fall within NYC's five boroughs: Manhattan (New York County), Brooklyn (Kings County), Queens, the Bronx, and Staten Island (Richmond County).
3. Each valid record becomes a map marker with the school name and physical address in a popup.
4. Leaflet.markercluster groups nearby markers at lower zoom levels. The displayed location count reflects valid records returned by the live service.

## Data coverage

The map covers charter-school locations across NYC, not only Success Academy. **School locations and distinct schools are not necessarily the same:** a school may operate at more than one physical site. The marker count represents location records, not a verified count of unique schools.

## Implementation choices

- **Simple static HTML:** No framework, server, account, or build step is needed for this small mapping task.
- **Live public data:** The map reads directly from the state service instead of maintaining a manually copied list. The displayed count may change as the service's records change.
- **Existing mapping tools:** Leaflet, the clustering plugin, and Esri tiles cover the core mapping needs without building custom geographic functionality.

## Requirements and limitations

An internet connection is required to load the school data, map tiles, and external libraries. School locations are retrieved directly from New York State's GIS service, so the map reflects the information available from that source.


## Future Enhancements

Depending on the intended user journey, potential enhancements include:

- **Borough and ZIP-code navigation:** Explore schools within a selected borough or near a specific location.
- **Grade-level filters:** Find schools by elementary, middle, or high school level.
- **School and campus grouping:** Group multiple campuses belonging to the same school or charter network.
- **School contact information:** Include phone numbers, email addresses, or websites to help families connect with schools.

These enhancements would extend the MVP from geographic discovery toward helping families identify, compare, and connect with relevant schools.
