---
title: Inflation Is Back at a 3-Year High
---

US consumer prices rose **4.2%** over the year to May 2026 — the hottest annual inflation since 2023, and a clear reversal of the disinflation everyone had penciled in. But the driver isn't the "sticky shelter" story you keep hearing. The category running hottest is **transportation, at 8.3%**, while energy inflation has nearly vanished (0.9%) and housing has cooled to 3.9%.

```sql headline
select yoy_pct
from "cpi-three-year-high".data
where component = 'All items'
order by date desc
limit 1
```

<BigValue
  data={headline}
  value="yoy_pct"
  title="CPI inflation, May 2026 (year over year)"
  fmt='0.0"%"'
/>

## The reacceleration

After cooling through 2023–2024, headline inflation has turned back up.

```sql allitems_yoy
select date, yoy_pct
from "cpi-three-year-high".data
where component = 'All items' and date >= '2015-01-01' and yoy_pct is not null
order by date
```

<LineChart
  data={allitems_yoy}
  x="date"
  y="yoy_pct"
  title="CPI inflation rate, year over year (%)"
  yAxisTitle="YoY %"
  xAxisTitle="Year"
  yFmt='0.0"%"'
/>

## What's actually driving the 4.2%

Transportation is doing the heavy lifting — not shelter or energy.

```sql components_latest
select component, yoy_pct
from "cpi-three-year-high".data
where date = (select max(date) from "cpi-three-year-high".data)
  and component <> 'All items'
order by yoy_pct desc
```

<BarChart
  data={components_latest}
  x="component"
  y="yoy_pct"
  title="Inflation by category, May 2026 (year over year)"
  swapXY=true
  yFmt='0.0"%"'
/>

---

*Source: [US Bureau of Labor Statistics](https://www.bls.gov/cpi/) CPI-U, seasonally adjusted (series CUSR0000*). Public domain. Year-over-year change computed from the monthly index; categories are BLS summary components.*
