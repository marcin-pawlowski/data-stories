---
title: California Housing — The Great Coastal Cooldown
description: San Francisco home values sit well below their 2022 peak even as the US index hits new highs. California's coastal housing cooldown, mapped with Zillow's ZHVI.
---

Zillow's Home Value Index (ZHVI) tells a stark story: San Francisco's typical home
is worth roughly **$120,000 less** today than at its June 2022 peak, even as the
national index hit new highs. Meanwhile, coastal California metros that doubled
the U.S. growth rate from 2020–2022 have diverged sharply downward.

> **Note:** Columns from June 2025 onward are Zillow forecasts, not observed transactions.
> ZHVI is a smoothed, seasonally adjusted index — not a sale price.

```sql primary
with unpivoted as (
  unpivot "california-housing-rent-vs-buy".data
  on columns(* exclude (RegionID, SizeRank, RegionName, RegionType, StateName))
  into
    name month_str
    value zhvi
)
select
  RegionName,
  StateName,
  RegionType,
  SizeRank,
  cast(month_str as date) as month,
  zhvi,
  case when cast(month_str as date) >= '2025-06-01' then true else false end as is_forecast
from unpivoted
where
  RegionName in (
    'United States',
    'Los Angeles, CA',
    'San Francisco, CA',
    'San Diego, CA',
    'Riverside, CA',
    'Sacramento, CA'
  )
  and cast(month_str as date) >= '2015-01-01'
  and zhvi is not null
order by RegionName, month
```

## Home Values Since 2015

Coastal CA metros surged far above the U.S. benchmark during 2020–2022, then reversed.
San Francisco is the only major metro still meaningfully below its 2022 peak.

<LineChart
  data={primary}
  x="month"
  y="zhvi"
  series="RegionName"
  title="ZHVI by Metro, 2015–2026"
  yFmt="$#,##0"
  yAxisTitle="Home Value Index (USD)"
  xAxisTitle="Month"
/>

## Recent Snapshot: May 2026 Forecast Values

The table below shows each metro's latest forecast value alongside its position
in the dataset.

```sql snapshot
select
  RegionName,
  round("2026-05-31", 0) as zhvi_may2026,
  round("2022-06-30", 0) as zhvi_jun2022,
  round(
    ("2026-05-31" - "2022-06-30") / "2022-06-30" * 100,
    1
  ) as pct_chg_since_jun2022
from "california-housing-rent-vs-buy".data
where
  RegionName in (
    'United States',
    'Los Angeles, CA',
    'San Francisco, CA',
    'San Diego, CA',
    'Riverside, CA',
    'Sacramento, CA'
  )
order by pct_chg_since_jun2022 asc
```

<DataTable
  data={snapshot}
  rows=10
/>

## How far have values moved since June 2022?

<BarChart
  data={snapshot}
  x="RegionName"
  y="pct_chg_since_jun2022"
  title="% change in ZHVI, June 2022 to May 2026 forecast"
  yFmt='#,##0.0"%"'
  yAxisTitle="% change"
  xAxisTitle="Metro"
/>

---

*Source: [Zillow Research](https://www.zillow.com/research/data/) ZHVI,
licensed [CC BY](https://creativecommons.org/licenses/by/4.0/).
Middle tier (33rd–67th percentile), smoothed and seasonally adjusted.
Forecasts begin June 2025.*