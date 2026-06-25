---
title: "30x faster zonal stats with cloud-native COGs and exactextract"
date: 2026-06-25
author: Al Hotimski
layout: single
---

Most working GIS code runs about 30 times slower than it has to.

I know because I measured it on my own workflow last week.

I'm building a small open-source library called [cogsieve](https://github.com/ahotimski00/cogsieve) that filters polygons by fractional coverage of categorical rasters. Standard zonal-statistics work: given a set of parcels and a land-cover raster, tell me which parcels are mostly cropland, mostly forest, or mostly developed. The kind of question every working-GIS shop answers daily, every land trust uses for screening, every utility runs for siting analysis.

I wrote a fair benchmark against `rasterstats`, the standard pure-Python alternative, on 25,000 San Diego County parcels against the same USGS LCMAP raster hosted on Microsoft Planetary Computer. Same machine, back-to-back, single pass each:

| Tool | Wall clock | Throughput |
|---|---|---|
| cogsieve | 10.7 s | 2,330 parcels/sec |
| rasterstats | 320 s | 78 parcels/sec |

cogsieve is 30 times faster on the same data, against the same remote raster, doing more accurate per-pixel math.

The point of this post is not that cogsieve is clever. It isn't. cogsieve uses the right C++ library (`exactextract`) and the right IO pattern (Cloud-Optimized GeoTIFF range reads). Both have been publicly available and MIT-licensed for years. The 30x gap is what working GIS shops give up when they reach for the familiar tool first.

## Why the gap is so large

Three factors multiply.

**One: rasterstats answers 25,000 questions; exactextract answers all 25,000 in one sweep.**

rasterstats iterates per polygon. For each one it builds an in-memory rasterized mask of the polygon's shape, reads the raster window for that polygon's bounding box, applies the mask, and counts pixels. Separate read, separate GDAL `rasterize` call, separate numpy operation for each of the 25,000 polygons.

exactextract iterates per raster tile. For each tile it asks which polygons overlap it, then computes exact fractional pixel coverage for all of them in one C++ inner loop. The 200th polygon that intersects the same tile costs almost nothing extra.

Algorithmically: one pass through the data versus N passes. Worth roughly 3 to 5 times the speed.

**Two: the inner loop runs in C++, not Python.**

The per-pixel math runs millions of times. In rasterstats that loop is Python orchestrating numpy. Each iteration pays Python interpreter overhead, which adds up over millions of pixels. exactextract is C++ end to end. The same conceptual work runs roughly 50 times faster per inner-loop step. After amortization across the parts of the workflow that aren't inner-loop, you net out at maybe 5 to 10 times the speed.

**Three: COG range reads batch better than per-polygon reads.**

A Cloud-Optimized GeoTIFF supports HTTP range requests for sub-file reads. The speed advantage comes from batching: pull several adjacent tiles in one HTTP round trip when you know you'll need them.

rasterstats reads per polygon, which produces many small uncoordinated HTTP requests. exactextract's tile iterator knows what's coming next, and the GDAL HTTP layer batches and caches accordingly. Each HTTP request has about 50 to 100 milliseconds of round-trip latency regardless of payload size. Thousands of independent requests versus hundreds of batched ones is another 2 to 3x difference on remote rasters.

Multiplied together: 3-5 × 5-10 × 2-3 ≈ 30.

## When the gap shrinks

Honest caveats. The 30x is not universal.

- **Tiny rasters held in memory.** HTTP overhead disappears, factor three vanishes. The gap drops to roughly 10x.
- **A handful of huge polygons.** Per-polygon orchestration matters less when there are fewer iterations. The gap drops to 5-10x.
- **Local rather than remote rasters.** Range-read batching matters less. The gap drops to roughly 15x.
- **Polygons sparsely scattered across the raster.** Tile sharing doesn't help exactextract as much. Factor one weakens.

For the typical working-GIS shape (thousands of polygons over a remote categorical raster) 20-50x speedups are common in published exactextract benchmarks. The 30x I measured sits in the middle of that range, not at the edge.

## Why the gap exists at all

There is a real industry-level explanation, and it is not "GIS people are bad at code."

ArcGIS Pro is the dominant working environment. Most GIS analysts learn ArcPy first, not modern Python. Most enterprise GIS shops carry ArcGIS licenses through their employer. The standard zonal-stats workflow (`RasterToPolygon` then `Intersect` then `Statistics`) is the standard workflow because it is what the documentation shows, the YouTube tutorials demonstrate, and the textbook describes. Matt Forrest writes about this directly in [Stuck in Legacy GIS](https://forrest.nyc/stuck-in-legacy-gis-a-practical-roadmap-to-modern-gis-and-cloud-native-geospatial/): the technology has moved on, but the muscle memory and the training pipeline have not.

The Cloud-Native Geospatial movement is the institutional response. The [Cloud-Native Geospatial Forum](https://cloudnativegeo.org) is tracking the shift toward COG, STAC, GeoParquet, and the modern stack. It is a real movement with a real organization behind it, not one open-source maintainer's opinion.

But for most working GIS shops, the path of least resistance is still the legacy workflow. The 30x hasn't reached them yet because nothing forces them to measure it.

## What I'd actually recommend

If you are doing zonal statistics on more than a few thousand polygons, try `exactextract`. If you are reading raster data hosted as COGs, use rasterio's `/vsicurl/` driver and let GDAL batch the range requests. If you are publishing derived data, write to GeoParquet, not Shapefile.

Daniel Baston (the author of `exactextract`) gave [the canonical talk at FOSS4G NA 2024](https://talks.osgeo.org/foss4g-na-2024/talk/RLJJN7/). The library has Python bindings (`exactextract` on PyPI) that don't require any C++ tooling on your machine. It is a `pip install` and three lines of code.

If you want to see the whole pattern end to end (cloud-native raster reads, exactextract-based screens, content-addressed caching, and an interactive Streamlit demo) the [cogsieve repo](https://github.com/ahotimski00/cogsieve) is the demonstration. The benchmark script that produced the 30x number is committed and reproducible: `python scripts/bench_rasterstats.py` from a fresh clone, and you get your own measurement on your own hardware.

## What I am not saying

I am not saying ArcGIS is bad. I work in it every day. The visualization layer is excellent, the cartographic output is the industry standard, and the ecosystem of analysts who know how to use it is enormous. None of that goes away because exactextract is fast.

I am saying that for the specific workload of summarizing categorical raster coverage over a lot of polygons, the standard tools are leaving an order of magnitude on the table. If that workload is on your critical path (and for parcel-screening work like mine, it is), the fix is one Python package away.