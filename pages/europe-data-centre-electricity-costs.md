---
title: Europe's Data Centre Power Bill
---

Hyperscalers picking European data centre sites in 2025 face a brutal trade-off:
grids with the highest renewable share are often the smallest.
Ember's 2024 generation data makes the divide visible.

## Wind+Solar vs Fossil Share — EU-27, 2024

Size = total demand (TWh). Grids above the 30 % fossil line carry meaningful
Scope 2 risk for 24/7 matching commitments.

<ScatterPlot
  data={primary}
  x="wind_solar_pct"
  y="fossil_pct"
  size="demand_twh"
  series="Area"
  xAxisTitle="Wind + Solar %"
  yAxisTitle="Fossil %"
  title="EU Grid Cleanliness vs Scale (2024)"
/>

<BigValue
  data={primary}
  value="wind_solar_pct"
  title="Highest Wind+Solar % (2024)"
/>

## Renewable Transition Pace — Selected EU Countries

Denmark's curve is nearly vertical; France's is nearly flat (nuclear baseload).

<LineChart
  data={trends}
  x="Year"
  y="wind_solar_pct"
  series="Area"
  yAxisTitle="Wind + Solar %"
  title="Wind+Solar Share 2000–2024"
/>

## Germany's Generation Mix — The Energiewende in TWh

The gas gap opened visibly after the nuclear phase-out.

<AreaChart
  data={germany}
  x="Year"
  y="twh"
  series="Variable"
  yAxisTitle="TWh"
  title="Germany Generation Mix 2000–2024"
/>

<DataTable data={primary} rows=27 />

> **Source:** Ember Global Electricity Review 2025 (CC-BY). 2024 figures are
> provisional estimates. Clean % includes hydro and bioenergy; treat wind+solar
> separately for 24/7 matching analysis.