---
title: The Cocoa & Coffee Shelf-Price Shock
---

Cocoa futures hit all-time highs in 2024 and arabica coffee followed in 2025.
Shelf prices lag wholesale by 6–12 months — BLS retail data shows that catch-up
happening in real time.

```sql primary
select
  series_id,
  year,
  period,
  cast(value as double) as price_usd,
  cast(year as varchar) || '-' || right(period, 2) as year_month,
  cast(year as integer) * 100 + cast(right(period, 2) as integer) as sort_key
from "cocoa-coffee-price-collapse".data
where series_id in ('APU0000717111', 'APU0000717311')
  and period != 'M13'
order by series_id, sort_key
```

```sql heatmap_coffee
select
  year,
  cast(right(period, 2) as integer) as month_num,
  cast(value as double) as price_usd
from "cocoa-coffee-price-collapse".data
where series_id = 'APU0000717111'
  and period != 'M13'
order by year, month_num
```

## Retail Price Trend: Coffee vs. Chocolate

<LineChart
  data={primary}
  x="year_month"
  y="price_usd"
  series="series_id"
  title="Coffee (APU0000717111) & Chocolate (APU0000717311) — USD/unit"
  yAxisTitle="Avg Retail Price (USD)"
/>

Both series share the same upward slope, but coffee led the shock while
chocolate is accelerating faster through 2024–25.

## Monthly Price Heatmap — Ground Coffee

<Heatmap
  data={heatmap_coffee}
  x="year"
  y="month_num"
  value="price_usd"
  title="Ground Coffee Retail Price by Year & Month"
  colorScale="blue"
/>

The darkest cells reveal the exact months when commodity costs passed through
to the shelf — the 2024–25 cluster is the most concentrated shock in 30 years.

## Data Table

<DataTable data={primary} rows=15 />

> **Source:** US Bureau of Labor Statistics, Average Retail Prices
> (`ap.data.0.Current`). Series APU0000717111 (coffee) and APU0000717311
> (chocolate). US city average, not seasonally adjusted.