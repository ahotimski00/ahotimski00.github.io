---
layout: single
title: "Tools"
permalink: /tools/
author_profile: true
toc: true
toc_label: "Tools"
toc_icon: "wrench"
---

Open-source libraries and interactive demos that stand on their own outside the longer case studies on the [Projects](/projects/) page.

---

## cogsieve {#cogsieve}

**A Python library that filters polygons by fractional class coverage of categorical rasters, reading windowed pixels directly from remote Cloud-Optimized GeoTIFFs instead of downloading scenes.** Three concrete use cases (solar siting, tree equity, wildfire risk) demonstrated on public data.

**Live demo:** [cogsieve-vir5swvkd2a5fypnpyqlnn.streamlit.app](https://cogsieve-vir5swvkd2a5fypnpyqlnn.streamlit.app/) - move two sliders, watch 25,000 San Diego County parcels re-filter in milliseconds.

[![cogsieve interactive solar-siting demo, San Diego County: threshold sliders, funnel stats, suitable parcels on a map](/assets/img/cogsieve_streamlit.png)](https://cogsieve-vir5swvkd2a5fypnpyqlnn.streamlit.app/)

**Repository:** [github.com/ahotimski00/cogsieve](https://github.com/ahotimski00/cogsieve)

**Stack:** Python · rasterio · geopandas · exactextract · pystac-client · Planetary Computer · Streamlit · pytest · GitHub Actions

**What it does:** Given a GeoDataFrame of polygons and a categorical raster (NLCD-style land cover, slope class, burn severity, etc.), compute the exact fractional pixel coverage per class per polygon, then filter polygons by a per-class threshold. Chain multiple screens to build a funnel. One declarative `CoverageScreen` dataclass carries the configuration for a stage, and the same primitive serves different domain questions just by changing the class codes and thresholds.

**Why it is fast:** Three design choices stack:
- **Exact fractional coverage** via `exactextract` (C++), instead of the standard rasterize-then-intersect workflow that produces edge artifacts and intermediate vector data.
- **COG windowed reads over HTTP** via rasterio's `/vsicurl/` driver: screens against a 30 GB CONUS LCMAP raster fetch only the tiles intersecting each parcel's bounding box, no scene download.
- **Funnel pipeline with content-addressed caching:** the second screen only sees parcels that survived the first, and per-stage GeoParquet caches make re-runs essentially free.

A two-screen funnel against 25,000 San Diego County parcels (USGS LCMAP buildable + 3DEP-derived slope) runs end-to-end in 12 seconds.

**Three demo domains, all on public data:**
- **Solar siting** (San Diego County): buildable land cover + low slope → 113 utility-scale candidates from 25,000 parcels.
- **Tree equity** (LA County): low canopy + urban context → 6,213 priority planting block groups from 6,591.
- **Wildfire WUI** (San Diego County): MTBS burn-severity touch → 45 parcels in the 2007 Witch Fire perimeter.

**Engineering practices:** typed Python (mypy clean), ruff-linted, hermetic pytest fixtures (no network in tests), GitHub Actions CI on Python 3.11 and 3.12, MIT-licensed, no proprietary dependencies.
