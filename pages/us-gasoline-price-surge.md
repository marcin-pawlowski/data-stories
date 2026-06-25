---
title: 35 Years of Gas Prices
---

US gas prices climbed this spring on the Iran-war oil shock, peaking near **$4.49/gallon** in mid-May 2026. But the more useful view is the long one: 35 years of weekly pump prices put today's number — and every "unprecedented" surge — in perspective. As of late June the national average is **$3.91 and easing** — still high by historical standards, but already well off the spring peak and below the 2022 record.

```sql latest
select GASREGW as price
from "us-gasoline-price-surge".data
where GASREGW is not null
order by observation_date::date desc
limit 1
```

<BigValue
  data={latest}
  value="price"
  title="US regular, latest weekly average"
  fmt="$0.00"
/>

## Every shock since 1990

The Gulf War, the 2008 spike, the COVID collapse, the 2022 record near $5 — and where 2026 sits among them.

```sql prices
select observation_date::date as week, GASREGW as price
from "us-gasoline-price-surge".data
where GASREGW is not null
order by week
```

<LineChart
  data={prices}
  x="week"
  y="price"
  title="US weekly regular gasoline price ($/gallon)"
  yAxisTitle="$/gallon"
  xAxisTitle="Year"
  yFmt="$0.00"
/>

## The last four years up close

The 2022 spike to roughly $5 still stands as the record. The 2026 rise is real but smaller — and already fading.

```sql recent
select observation_date::date as week, GASREGW as price
from "us-gasoline-price-surge".data
where GASREGW is not null and observation_date::date >= '2022-01-01'
order by week
```

<LineChart
  data={recent}
  x="week"
  y="price"
  title="Gasoline price since 2022 ($/gallon)"
  yAxisTitle="$/gallon"
  xAxisTitle="Year"
  yFmt="$0.00"
/>

---

*Source: [EIA](https://www.eia.gov/petroleum/gasdiesel/) Weekly Retail Gasoline Prices (regular, all formulations) via [FRED](https://fred.stlouisfed.org/series/GASREGW) series GASREGW. Nominal dollars, not inflation-adjusted; national average masks large regional variation.*
