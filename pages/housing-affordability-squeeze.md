---
title: America's Two-Speed Housing Market
---

The "housing affordability squeeze" isn't one story anymore — it's two. Zillow's state-level home value index shows **California peaked in January 2025 and has fallen every month since** (to ~$776K), while **New York, Massachusetts, and New Jersey keep setting fresh highs**. The expensive coasts are diverging, and the post-2020 Sun Belt boom has cooled.

```sql primary
with unpivoted as (
  unpivot "housing-affordability-squeeze".data
  on columns(* exclude (RegionID, SizeRank, RegionName, RegionType))
  into
    name month_str
    value zhvi
)
select
  RegionName,
  cast(month_str as date) as month,
  zhvi
from unpivoted
where RegionName in ('California', 'New York', 'Massachusetts', 'New Jersey', 'Texas', 'Florida', 'Arizona')
  and cast(month_str as date) >= '2015-01-01'
  and zhvi is not null
order by RegionName, month
```

<LineChart
  data={primary}
  x="month"
  y="zhvi"
  series="RegionName"
  title="Typical home value by state, 2015–2026"
  yAxisTitle="Home value (USD)"
  xAxisTitle="Year"
  yFmt="$#,##0"
/>

## Post-pandemic winners and losers

Measured from the start of 2022, the Northeast keeps grinding higher while several Sun Belt stars have stalled or slipped.

```sql change
select
  RegionName,
  round(("2026-05-31" - "2022-01-31") / "2022-01-31" * 100, 1) as pct_change
from "housing-affordability-squeeze".data
where RegionName in ('California', 'New York', 'Massachusetts', 'New Jersey', 'Texas', 'Florida', 'Arizona', 'Georgia', 'North Carolina', 'Illinois')
order by pct_change desc
```

<BarChart
  data={change}
  x="RegionName"
  y="pct_change"
  title="% change in typical home value, Jan 2022 to May 2026"
  swapXY=true
  yFmt='#,##0.0"%"'
/>

---

*Source: [Zillow Research](https://www.zillow.com/research/data/) ZHVI (typical middle-tier home value, smoothed & seasonally adjusted), by state. CC BY. The most recent months include Zillow's forecast.*
