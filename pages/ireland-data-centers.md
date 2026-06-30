---
title: The Country Where Data Centers Eat a Quarter of the Grid
description: In Ireland, data centers now use 22% of all metered electricity — up from 4% in 2015. The clearest real-world picture of what the AI build-out does to a national grid.
---

We've [written before](/data-stories/ai-data-center-power-demand) about data centers taking a growing slice of national electricity — around 5% in the US, based on modelled estimates. Ireland is the place to see the same force without the modelling. Its statistics office meters the consumption directly, and the number is in a different league: data centers now draw **22% of all the electricity used in the country** — nearly a quarter of the entire national grid, up from a rounding error a decade ago.

```sql latest_share
with q as (
  select
    make_date(left("Quarter", 4)::int, (right("Quarter", 1)::int - 1) * 3 + 1, 1) as quarter,
    sum(case when "Electricity Consumption" = 'Data centres' then "VALUE"::int else 0 end) as dc,
    sum(case when "Electricity Consumption" = 'All metered electricity consumption' then "VALUE"::int else 0 end) as total
  from "ireland-data-centers".data
  group by 1
)
select round(dc * 100.0 / total, 1) as dc_share
from q
order by quarter desc
limit 1
```

<BigValue
  data={latest_share}
  value="dc_share"
  title="Ireland's electricity going to data centers (Q4 2024)"
  fmt='0.0"%"'
/>

## From a rounding error to a fifth of the grid

In early 2015 data centers used about 290 gigawatt-hours a quarter — a rounding error next to the rest of the country. By the end of 2024 they were pulling **1,829 GWh** a quarter, a **531% increase**. Over the same stretch, everyone else's consumption barely moved. The grid didn't grow to fit the data centers; the data centers grew into the grid.

```sql by_category
select
  make_date(left("Quarter", 4)::int, (right("Quarter", 1)::int - 1) * 3 + 1, 1) as quarter,
  "Electricity Consumption" as category,
  "VALUE"::int as gwh
from "ireland-data-centers".data
where "Electricity Consumption" in ('Data centres', 'Customers other than data centres')
order by quarter
```

<LineChart
  data={by_category}
  x="quarter"
  y="gwh"
  series="category"
  title="Quarterly metered electricity in Ireland (GWh): data centers vs everyone else"
  yAxisTitle="GWh per quarter"
  xAxisTitle="Quarter"
/>

## The share that keeps climbing

Plotted as a percentage of all metered electricity, the line has gone almost straight up — from roughly 4% a decade ago toward a quarter today. This is why Ireland imposed a de-facto moratorium on new data-center grid connections around Dublin: the system operator ran out of headroom.

```sql share_over_time
with q as (
  select
    make_date(left("Quarter", 4)::int, (right("Quarter", 1)::int - 1) * 3 + 1, 1) as quarter,
    sum(case when "Electricity Consumption" = 'Data centres' then "VALUE"::int else 0 end) as dc,
    sum(case when "Electricity Consumption" = 'All metered electricity consumption' then "VALUE"::int else 0 end) as total
  from "ireland-data-centers".data
  group by 1
)
select quarter, round(dc * 100.0 / total, 1) as dc_share
from q
order by quarter
```

<LineChart
  data={share_over_time}
  x="quarter"
  y="dc_share"
  title="Data centers as a share of all metered electricity in Ireland (%)"
  yAxisTitle="Share of electricity (%)"
  xAxisTitle="Quarter"
  yFmt='0.0"%"'
/>

## Why this is the story to watch

Most countries are heading where Ireland already is, just earlier on the curve. A small economy that courted tech investment for decades ended up hosting a concentration of data centers with nowhere left to plug them in. As the AI build-out accelerates, the Irish line is a preview of the squeeze larger grids will feel next — measured, not estimated.

---

*Source: [Ireland Central Statistics Office](https://www.cso.ie/en/statistics/energy/datacentresmeteredelectricityconsumption/), table MEC02 (Data Centres Metered Electricity Consumption), via the [PxStat open API](https://ws.cso.ie/public/api.restful/PxStat.Data.Cube_API.ReadDataset/MEC02/CSV/1.0/en). Quarterly metered consumption, 2015–2024. "Metered electricity" excludes a small amount of unmetered supply, so figures are slightly below total generation.*
