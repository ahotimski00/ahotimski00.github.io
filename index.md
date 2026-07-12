---
layout: home
author_profile: true
title: "Al Hotimski"
excerpt: "Geospatial Data Scientist"
---
Geospatial Data Scientist at **The Conservation Fund** with an MS in Remote Sensing and Geospatial Sciences (Environmental Data Science). I build data systems and analytical models that make sense of the landscape: land ownership, urban growth, fire risk, and conservation opportunity. The tools I have shipped at TCF have cut analysis time from 20+ hours to 10 minutes and reduced manual QA workloads by 93%.

---

## What I Do

<div class="feature__wrapper">

<div class="feature__item">
    <div class="archive__item">
      <div class="archive__item-body">
        <h2 class="archive__item-title">Geospatial Analysis</h2>
        <div class="archive__item-excerpt">
          <p>Land cover classification, change detection, and spatial data modeling. ArcGIS Pro, QGIS, Google Earth Engine, geopandas, rasterio. Recent: 17 years of Landsat across LA County's fire hazard zones.</p>
        </div>
      </div>
    </div>
  </div>

<div class="feature__item">
    <div class="archive__item">
      <div class="archive__item-body">
        <h2 class="archive__item-title">Machine Learning</h2>
        <div class="archive__item-excerpt">
          <p>Supervised classification, time-series change detection (CCDC), and fuzzy entity resolution applied to spatial and environmental data. scikit-learn, pandas, geopandas.</p>
        </div>
      </div>
    </div>
  </div>

<div class="feature__item">
    <div class="archive__item">
      <div class="archive__item-body">
        <h2 class="archive__item-title">Conservation Tech</h2>
        <div class="archive__item-excerpt">
          <p>End-to-end pipelines for land trusts and conservation orgs. USDA NRCS ACEP grant screening that replaces manual Web Soil Survey queries with one regional run. LLC-resolved parcel ownership and boundary change tracking across Southeast U.S. timberland.</p>
        </div>
      </div>
    </div>
  </div>

</div>

---

## Projects

### [cogsieve](/tools/#cogsieve)

An open-source Python library that filters polygons by fractional class coverage of categorical rasters, reading windowed pixels directly from remote Cloud-Optimized GeoTIFFs instead of downloading scenes. Three runnable demos on public data: solar siting, tree equity, wildfire risk.
**Open source (MIT), CI-tested, 30x faster than the standard pure-Python zonal-stats workflow.** [Live demo](https://cogsieve-vir5swvkd2a5fypnpyqlnn.streamlit.app/) · [GitHub](https://github.com/ahotimski00/cogsieve)
`Python` `rasterio` `geopandas` `exactextract` `COG` `Streamlit`

---

### [parcel-lineage](/tools/#parcel-lineage)

An open-source library that reconciles messy county parcel owner names into their true holdings and tracks ownership change between snapshots. Runs live against public ArcGIS parcel services.
**Open source (MIT), typed and tested. On real Adirondack data, it collapses 711 raw owner strings to surface the largest true timberland holders.** [GitHub](https://github.com/ahotimski00/parcel-lineage)
`Python` `rapidfuzz` `pandas` `ArcGIS REST` `Entity Resolution`

---

### [Land Ownership and Boundary Change Detection](/projects/#land-ownership)

An automated pipeline that resolves LLC ownership structures in county parcel records and detects ownership and boundary changes between time-stamped snapshots using spatial overlay analysis and symmetric difference.
**93% reduction in manual QA review. Longitudinal ownership intelligence across the Southeast U.S.**
`Python` `SQL` `Data Harmonization` `Relational DB` `Spatial Overlay` `ReGrid`
*Open-source, public-data version: [parcel-lineage](/tools/#parcel-lineage).*

---

### [ACEP Easement Eligibility Screening Tool](/projects/#farm-parcel)

Automated USDA NRCS ACEP easement grant screening by applying SSURGO and NLCD raster criteria via REST services.
**Analysis time: 20+ hours → 10 minutes. Projected $12,000/yr savings.**
`Python` `ArcGIS Pro` `REST APIs` `SSURGO` `NLCD`

---

### [Urban Growth in Fire Hazard Zones](/projects/#fire-hazard)

A 9-class Landsat change detection (2007-2024) paired with a full Olofsson accuracy assessment. New development expanded into LA County's very high fire hazard zones before the hazard designation caught up; the mapped extent corrects from ~16,600 ha to ~5,700 ha once bias-adjusted.
`GEE` `Random Forest` `Landsat` `Accuracy Assessment`

---

## Skills

| Domain | Tools |
| --- | --- |
| Languages | Python, R, SQL, JavaScript, Bash |
| ML & Analysis | scikit-learn, supervised classification, fuzzy matching, data harmonization, entity resolution, time-series, change detection (CCDC) |
| Data Engineering | pandas, NumPy, relational databases, ETL pipelines, Git |
| GIS & Remote Sensing | ArcGIS Pro, QGIS, Google Earth Engine (cloud-native), geopandas, shapely, rasterio, Landsat |
| Visualization | Power BI, ArcGIS Online, matplotlib |

---

## Get in touch

Open to geospatial data science, remote sensing, and spatial ML roles.

[Connect on LinkedIn](https://www.linkedin.com/in/al-hotimski/){: .btn .btn--primary}
