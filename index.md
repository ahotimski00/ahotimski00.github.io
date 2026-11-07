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
          <p>Land cover classification, change detection, and spatial data modeling. ArcGIS Pro and arcpy (custom Python toolboxes), ArcGIS Online, QGIS, Google Earth Engine, geopandas, rasterio. Recent: 17 years of Landsat across LA County's fire hazard zones.</p>
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

Screening which parcels are mostly forested, buildable, or high-risk usually means downloading whole raster scenes and waiting through slow, artifact-prone zonal stats. cogsieve reads exact fractional class coverage straight from remote Cloud-Optimized GeoTIFFs, so an analyst can funnel a county's parcels through several suitability screens in seconds and hand planners a defensible shortlist the same day. Three runnable demos on public data: solar siting, tree equity, wildfire risk.
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

---

### [ACEP Easement Eligibility Screening Tool](/projects/#farm-parcel)

Conservation staff were spending 20+ hours manually checking each farm parcel's ACEP easement eligibility, county by county in Web Soil Survey, a bottleneck on every grant cycle. I built an ArcGIS Pro Python toolbox (arcpy) that screens whole regions against live USDA SSURGO and NLCD services and returns a ranked, field-ready shortlist.
**Analysis time: 20+ hours to 10 minutes. Projected $12,000/yr savings.**
`Python` `arcpy` `ArcGIS Pro` `REST APIs` `SSURGO` `NLCD`

---

### [Urban Growth in Fire Hazard Zones](/projects/#fire-hazard)

In California, a Very High fire hazard designation triggers stricter wildfire building codes, so the map decides which new homes are built to that standard. Development expanded into LA County's very high zones during the years the maps went unrevised, much of it before the designation applied. The classification maps ~16,600 ha of it; a full Olofsson accuracy assessment corrects that to ~5,700 ha.
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

Open to geospatial data science, remote sensing, spatial ML, and solutions engineering roles.

[Connect on LinkedIn](https://www.linkedin.com/in/al-hotimski/){: .btn .btn--primary}
