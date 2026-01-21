# Al Hotimski — Applied Data Scientist & Geospatial Analyst

### Education:
Remote Sensing and Geospatial Sciences, MS

### Work Experience:
Geospatial Analyst @ The Conservation Fund
- Automating Land Ownership and Boundary Change Detection

Research Assistant @ PLACES lab
- Land cover classification, Colombian Andes

### About Me:
I am an applied data scientist with a background in geospatial analytics, land-use modeling, and environmental data systems. My work focuses on using data science and applied machine learning to solve real-world problems involving complex ownership structures, spatial change over time, and climate-related risk.

This portfolio highlights end-to-end projects where I designed data pipelines, built analytical models, and delivered outputs that directly supported decision-making in land management, conservation, and resource planning.

---

## Core Skills

**Data Science & Analytics**
- Applied machine learning (Random Forest, classification, regression)
- Feature engineering and model evaluation
- Time-series and longitudinal analysis
- Data cleaning, normalization, and record linkage

**Geospatial & Environmental Analysis**
- Spatial joins, overlays, and change detection
- Land cover and land use classification
- Habitat fragmentation and landscape analysis
- Satellite and remote sensing workflows

**Engineering & Tooling**
- Python (pandas, NumPy, scikit-learn)
- Fuzzy string matching and distance metrics
- Automated data pipelines
- Relational databases and structured data models
- Google Earth Engine

---

## Selected Projects

### Owner Identification & Tracking System
**Goal:** Identify true timberland ownership and track changes over time to support acquisition strategy, competitor monitoring, and habitat fragmentation analysis.

**What I Built:**
- A relational database linking child LLCs to parent holding companies
- A fuzzy-matching system using Euclidean distance to resolve inconsistent owner names
- A scalable Python pipeline to flag ownership and boundary changes across parcel datasets

**Impact:**
- Reduced manual ownership review by ~93%
- Enabled direct outreach to parent companies instead of cold outreach to shell LLCs
- Created a time series of land ownership for longitudinal analysis

<div class="carousel-wrapper">
  <button class="carousel-btn left" onclick="scrollCarousel(-1)">&#10094;</button>

  <div class="carousel" id="carousel">
    <figure>
      <img src="/assets/img/TCF7.jpg" alt="TCF7 project image">
      <figcaption>TCF7 visualization (edit caption)</figcaption>
    </figure>
    <figure>
      <img src="/assets/img/TCF8.jpg" alt="TCF8 project image">
      <figcaption>TCF8 visualization (edit caption)</figcaption>
    </figure>
    <figure>
      <img src="/assets/img/TCF9.jpg" alt="TCF9 project image">
      <figcaption>TCF8 visualization (edit caption)</figcaption>
    </figure>
    <figure>
      <img src="/assets/img/TCF10.jpg" alt="TCF10 project image">
      <figcaption>TCF8 visualization (edit caption)</figcaption>
    </figure>
    <figure>
      <img src="/assets/img/TCF11.jpg" alt="TCF11 project image">
      <figcaption>TCF8 visualization (edit caption)</figcaption>
    </figure>
    <figure>
      <img src="/assets/img/TCF12.jpg" alt="TCF12 project image">
      <figcaption>TCF8 visualization (edit caption)</figcaption>
    </figure>
    
  </div>

  <button class="carousel-btn right" onclick="scrollCarousel(1)">&#10095;</button>
</div>


[Project details coming soon]

---

### Land Cover Classification in Fire Hazard Severity Zones
**Goal:** Quantify patterns of urban development within fire hazard severity zones over time.

**Methods:**
- Random Forest classification in Google Earth Engine
- Landsat imagery (2007–2025)
- CAL FIRE fire hazard severity zone data

**Outputs:**
- Classified land cover maps
- Change detection across multiple time periods
- Spatial summaries for planning and risk assessment

[Project details coming soon]

---

## Approach

My work emphasizes:
- Clear problem framing
- Transparency in assumptions and data limitations
- Scalable, maintainable analytical systems
- Domain knowledge as a core modeling input

I focus on applied solutions that can be operationalized, rather than purely theoretical modeling.

---

## Contact

- **GitHub:** https://alhotimski.com
- **LinkedIn:** https://www.linkedin.com/in/al-hotimski/
- **Resume:** (tbd)

<script>
function scrollCarousel(direction) {
  const carousel = document.getElementById('carousel');
  const slideWidth = carousel.clientWidth;
  carousel.scrollBy({
    left: direction * slideWidth,
    behavior: 'smooth'
  });
}
</script>

