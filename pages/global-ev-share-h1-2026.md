---
title: Global EV Share of New Car Sales (2011–2025)
---

# Global EV Share of New Car Sales

Electric vehicles (BEV + PHEV) as a share of new car sales across ~40 countries,
sourced from Our World in Data / IEA Global EV Outlook (CC BY 4.0).

```sql primary
select
  Entity,
  Code,
  Year,
  "Share of new cars that are electric" as ev_share
from "global-ev-share-h1-2026".data
where Entity in ('Norway','China','United States','Germany',
                 'United Kingdom','Australia','India')
order by Entity, Year
```

```sql snapshot2025
select
  Entity,
  "Share of new cars that are electric" as ev_share
from "global-ev-share-h1-2026".data
where Year = 2025
order by ev_share desc
```

```sql aus_highlight
select
  round("Share of new cars that are electric", 1) as ev_share
from "global-ev-share-h1-2026".data
where Entity = 'Australia' and Year = 2025
```

The S-curve isn't coming for several markets — it already arrived.
Australia's EV share rocketed from near-zero in 2011 to:

<BigValue
  data={aus_highlight}
  value="ev_share"
  title="Australia 2025 EV Share (%)"
/>

## Adoption Trajectories (2011–2025)

Norway is saturating above 90%; China has surged past 40%; the US crawls under 15%.

<LineChart
  data={primary}
  x="Year"
  y="ev_share"
  series="Entity"
  yAxisTitle="EV Share of New Car Sales (%)"
  title="EV Adoption by Country"
/>

## 2025 Country Rankings

<BarChart
  data={snapshot2025}
  x="Entity"
  y="ev_share"
  swapXY=true
  sort="ev_share"
  yAxisTitle="EV Share (%)"
  title="2025 EV Share — All Countries Ranked"
/>

## Full Data Table

<DataTable
  data={primary}
  rows=20
/>

> **Caveats:** 2025 figures are provisional. 'Electric' bundles BEV and PHEV.
> Absent countries should not be read as zero. Source: Our World in Data (CC BY 4.0).