---
title: AI Data Centers Are Eating the Grid
---

In 2020, data centers used about **2.6%** of all the electricity in the United States. By 2025 that figure had climbed to **4.9%** — nearly one in every twenty kilowatt-hours. The AI build-out everyone talks about in abstract terawatts shows up here as a measurable, fast-growing line item on the world's biggest grids.

The numbers below are IEA estimates compiled by Our World in Data, expressed as data centers' share of total national electricity demand — an apples-to-apples comparison across regions.

```sql us_2025
select "Share of total electricity demand coming from data centers" as dc_share
from "ai-data-center-power-demand".data
where Entity = 'United States' and Year = 2025
```

<BigValue
  data={us_2025}
  value="dc_share"
  title="US electricity going to data centers (2025)"
  fmt='0.0"%"'
/>

## The climb since 2020

The US and North America have pulled away from the rest of the world. Europe is high but flat; China and the global average only crossed 1% recently.

```sql trends
select
  Entity,
  Year,
  "Share of total electricity demand coming from data centers" as dc_share
from "ai-data-center-power-demand".data
where Entity in ('United States', 'Europe (IEA)', 'China', 'Asia Pacific (IEA)', 'World')
order by Entity, Year
```

<LineChart
  data={trends}
  x="Year"
  y="dc_share"
  series="Entity"
  title="Data center share of national electricity demand, 2020–2025"
  yAxisTitle="Share of electricity (%)"
  xAxisTitle="Year"
/>

## Who's most exposed in 2025

<BarChart
  data={snapshot_2025}
  x="Entity"
  y="dc_share"
  title="Data center share of electricity demand by region, 2025"
  xAxisTitle="Share of electricity (%)"
  swapXY=true
/>

```sql snapshot_2025
select
  Entity,
  round("Share of total electricity demand coming from data centers", 2) as dc_share
from "ai-data-center-power-demand".data
where Year = 2025
order by dc_share desc
```

## Full data

<DataTable data={snapshot_2025} rows=12 />

---

*Source: [Our World in Data](https://ourworldindata.org/grapher/data-centers-share-electricity-demand) compiling IEA estimates. Licensed [CC BY](https://creativecommons.org/licenses/by/4.0/). Figures are modelled estimates; 2024–2025 values are IEA projections, not metered consumption. Most non-country rows are IEA regional aggregates.*
