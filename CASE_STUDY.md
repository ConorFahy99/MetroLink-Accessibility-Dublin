# MetroLink: who benefits? — case study

**Project type:** GIS portfolio — accessibility analysis  
**Tools:** QGIS · ORS Tools · PostGIS · Python (GeoPandas) · Leaflet  
**Data:** CSO Census 2022 · TFI GTFS · MetroLink Railway Order alignment  
**CRS:** EPSG:2157 (Irish Transverse Mercator)

---

## The question

MetroLink is Ireland's largest current infrastructure project — a proposed 19km metro line from Swords to Charlemont, budgeted at approximately €9.5 billion. The public conversation around it tends toward total figures: how many people live near the route, how many stations, how many minutes saved.

Those figures tell an incomplete story. Dublin already has the DART, two Luas lines, and a commuter rail network. A project's value, analytically, is not how many people live near it — it's how many people it serves who are not already served. That marginal gain is the meaningful number.

This analysis answers a single question: how many Dublin residents does MetroLink bring within a 10-minute walk of high-capacity rail for the first time?

---

## Methodology

### Baseline first

The critical step is building the existing rail catchment before touching MetroLink data. Using the TFI GTFS feed, I extracted all stops on route types 0 (tram/Luas) and 2 (rail/DART/commuter). Bus was deliberately excluded — the analysis defines "high-capacity" as fixed rail and light rail, which is the category MetroLink would join. Including BusConnects would dilute the comparison and conflate very different service types.

I generated 10-minute walking isochrones for all baseline stops using ORS Tools (openrouteservice foot-walking profile, 4.8 km/h), then dissolved the results into a single baseline catchment polygon. This represents everyone already within walking distance of high-capacity rail.

### The marginal gain polygon

MetroLink's 16 proposed stations (sourced from the current Railway Order alignment and verified in QGIS) received the same 10-minute isochrone treatment. The marginal gain polygon is the result of a Vector Difference: MetroLink catchment minus baseline catchment. What remains is the area that MetroLink serves and the existing network does not.

The distinction matters. Overlapping MetroLink catchment over existing catchment and counting all residents would produce a number roughly ten times larger — and ten times less meaningful.

### Population apportionment

I apportioned CSO Census 2022 Small Area population counts (column T1_1AGETT, 5,076 Small Areas across the four Dublin local authorities) to the marginal gain polygon using areal weighting. Each Small Area's contribution is proportional to the share of its area that falls within the gain polygon. This is more accurate than centroid-in-polygon for a corridor analysis where many Small Areas are only partially captured.

### Deprivation overlay

The Pobal HP Deprivation Index is not publicly available at Small Area resolution, so I constructed a proxy from the same SAPS Census 2022 variables Pobal uses: male and female unemployment rates, age dependency ratio, proportion with primary education only, proportion with third-level education, and lone-parent ratio. Each variable was z-scored against the Dublin mean and combined into a composite score (higher = more deprived). Small Areas were ranked into deciles, with decile 1 as most deprived and decile 10 as most affluent.

---

## Findings

### Marginal gain

MetroLink's marginal catchment covers **9.11 km²** and contains **27,876 residents** — 1.9% of Dublin's population across the four local authorities. The gain splits 77/23 between Dublin City Council (21,336 residents) and Fingal (6,540), reflecting the route's path through previously underserved northside communities before reaching the airport corridor.

### An honest counter-finding

At €9.5 billion, the implied cost per newly served resident is **€340,700**. That figure belongs in any honest assessment of the project. It does not mean MetroLink is unjustified — the primary case for metro infrastructure rests on network connectivity, journey time reduction, induced demand, and economic agglomeration, none of which are captured by a residential catchment count. But the number exists and should be stated, not buried.

### The equity finding

The marginal gain zone is not a random cross-section of Dublin. Applying the deprivation proxy to the 159 Small Areas intersecting the gain polygon: **42% fall in the most deprived third** of Dublin's Small Areas (deciles 1–3), against a 30% baseline expectation if the gain were distributed evenly. The gain zone's mean deprivation score is +0.60 against a Dublin mean of approximately zero. The least deprived deciles (8–10) account for 18% of gain-zone Small Areas against a 30% baseline.

MetroLink's marginal catchment skews toward deprived communities — particularly the north inner city and parts of Ballymun and Glasnevin. The line is not primarily serving communities that already have good transport options.

---

## Decisions and trade-offs

**Why exclude bus?** Frequency, reliability, and capacity are not comparable between bus and rail. Including bus would require a defensible frequency threshold and would substantially shrink the apparent marginal gain, since BusConnects corridors overlap heavily with the MetroLink route. The cleaner analytical choice is to define the baseline consistently as fixed rail and LRT, then note the limitation.

**Why areal weighting over centroid-in-polygon?** Centroid methods systematically under-count partial captures — Small Areas near the edge of the gain polygon whose centroid falls outside. For a narrow corridor analysis this bias is material. Areal weighting is the standard approach for this type of catchment analysis.

**Why a SAPS proxy rather than the official HP Index?** Pobal's SA-level data is not available as a public download. Rather than omit the equity dimension, I reconstructed the index from its underlying variables. This is disclosed in the methodology and is arguably preferable for a portfolio piece: it demonstrates understanding of what the index measures, not just the ability to download a file.

---

## Limitations

The MetroLink alignment is based on the current Railway Order and may change before construction. Walking isochrones use a generalised street network and assume a flat 4.8 km/h pace — individual accessibility will vary. The analysis covers residential population only; a full assessment would incorporate workplace catchment using POWSCAR data. The deprivation proxy is not validated against the official HP Index.

---

## Links

- [Interactive map](https://conorfahy99.github.io/MetroLink-Accessibility-Dublin/metrolink_interactive_map.html) — catchment layers, deprivation overlay, station popups  
- [Findings infographic](https://conorfahy99.github.io/MetroLink-Accessibility-Dublin/findings_infographic.html) — headline metrics  
- [Static map](https://conorfahy99.github.io/MetroLink-Accessibility-Dublin/MetroLink_Deprivation_Map.png) — print-quality deprivation choropleth
