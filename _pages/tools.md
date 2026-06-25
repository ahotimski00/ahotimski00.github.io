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

**Live demo:** [cogsieve-vir5swvkd2a5fypnpyqlnn.streamlit.app](https://cogsieve-vir5swvkd2a5fypnpyqlnn.streamlit.app/) - three tabs (solar siting, tree equity, wildfire WUI), each with threshold sliders that re-filter cached coverage fractions in milliseconds.

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

**Approach: decisions I made building this**

*Use exact fractional pixel coverage instead of rasterize-then-intersect.* The textbook zonal-stats workflow vectorizes the raster, intersects with input polygons, then sums area per fragment. It introduces edge artifacts at polygon boundaries (a pixel half-inside the polygon either gets counted entirely or discarded) and produces large intermediate vector tables. `exactextract` computes each pixel's exact fractional intersection analytically in C++. Cleaner numbers, less code, and faster.

*Read remote rasters as Cloud-Optimized GeoTIFFs, do not download scenes.* The LCMAP and MTBS rasters used here are tens of gigabytes each, CONUS-wide. Naive workflows download the scene, clip locally, then analyze. cogsieve uses GDAL's `/vsicurl/` driver to issue HTTP range requests for only the tiles that intersect each polygon's bounding box. A state-wide screen pulls tens of megabytes over the wire, not gigabytes.

*Treat the screen as a config object, not a function.* One frozen `CoverageScreen` dataclass holds the raster URL, pass classes, track classes, threshold, and an `invert` flag. The same primitive serves "find parcels with high cropland coverage" (solar) and "find blocks with low canopy coverage" (tree equity) just by changing the class codes and the flag. Made adding the wildfire and tree-equity demos take a few hundred lines each instead of redoing the engine.

*Cache aggressively at stage boundaries.* The pipeline writes each screen's per-polygon coverage fractions to a content-addressed GeoParquet keyed by (polygon hash, screen name, classes, threshold). Re-runs with the same inputs replay from cache. The Streamlit demo above demonstrates the payoff: changing thresholds re-uses the cached fractions and only recomputes a boolean, which is why slider moves feel instant.

*Engineering bar: typed Python (mypy), ruff-linted, hermetic pytest fixtures (no network in tests), GitHub Actions CI on Python 3.11 and 3.12, MIT-licensed, no proprietary dependencies.* This is the floor, not the headline. The non-obvious choice was making the tests hermetic against a synthetic 4-quadrant raster fixture instead of pulling real data: it means CI runs in under a second and contributors don't need network access or USDA accounts to verify a change.
