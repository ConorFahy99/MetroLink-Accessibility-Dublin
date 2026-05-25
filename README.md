# MetroLink-Accessibility-Dublin
Marginal accessibility analysis of Dublin's proposed MetroLink line
# MetroLink: Who Benefits? — Dublin Accessibility Analysis

A GIS portfolio project analysing the **marginal accessibility gain** from Dublin's 
proposed MetroLink line: residents newly within a 10-minute walk of high-capacity rail 
who currently have none.

## Key findings

- **27,876 residents** newly served by MetroLink's marginal catchment
- **1.9%** of Dublin's population (4 Local Authority area)
- **42%** of gain-zone Small Areas fall in the most deprived third of Dublin — 
  MetroLink's marginal gain skews toward deprived communities
- Cost per newly served resident: **€340,700** (€9.5bn project cost)

## Deliverables

- [Interactive map](metrolink_interactive_map.html) — Leaflet, layers toggleable
- [Findings infographic](findings_infographic.html) — headline metrics
- [Deprivation map](metrolink_deprivation_map.png) — static print layout

## Method

Walking isochrones (ORS Tools, 10 min / 4.8 km/h) for MetroLink stations and existing 
DART, Luas, and commuter rail stops. Marginal gain = MetroLink catchment minus baseline. 
Population apportioned from CSO Census 2022 Small Areas (areal weighting). Deprivation 
proxy from SAPS variables. Analysis CRS: EPSG:2157 (ITM).

**Data:** CSO Census 2022 · TFI GTFS · MetroLink Railway Order alignment
