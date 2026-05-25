# MetroLink: Who Benefits? — Dublin Accessibility Analysis

A GIS portfolio project analysing the **marginal accessibility gain** from Dublin's proposed MetroLink line: residents newly within a 10-minute walk of high-capacity rail who currently have none.

![MetroLink deprivation map](https://raw.githubusercontent.com/ConorFahy99/MetroLink-Accessibility-Dublin/main/MetroLink_Deprivation_Map_web.png)

## Key findings

- **27,876 residents** newly served by MetroLink's marginal catchment
- **1.9%** of Dublin's population across 4 Local Authorities
- **42%** of gain-zone Small Areas fall in the most deprived third of Dublin
- Cost per newly served resident: **€340,700** (€9.5bn project cost)

## Deliverables

- [Interactive map](https://conorfahy99.github.io/MetroLink-Accessibility-Dublin/metrolink_interactive_map.html)
- [Findings infographic](https://conorfahy99.github.io/MetroLink-Accessibility-Dublin/findings_infographic.html)

## Method

Walking isochrones (ORS Tools, 10 min / 4.8 km/h) for MetroLink stations and existing DART, Luas, and commuter rail stops. Marginal gain = MetroLink catchment minus baseline. Population apportioned from CSO Census 2022 Small Areas (areal weighting). Deprivation proxy from SAPS variables. Analysis CRS: EPSG:2157 (ITM).

**Data:** CSO Census 2022 · TFI GTFS · MetroLink Railway Order alignment
