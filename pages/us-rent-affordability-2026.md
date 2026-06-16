---
title: 111 Years of US Rent
---

The Consumer Price Index for rent goes back to December 1914, when it sat at **21**. By 2026 it had reached **446** — a roughly 21× nominal rise. The striking part: nearly half of that entire 111-year increase has happened just since the year 2000. When people say housing "feels different now," the long view agrees.

```sql primary
select
  observation_date::date as obs_date,
  "CUUR0000SEHA" as rent_cpi,
  year(observation_date::date) as obs_year
from "us-rent-affordability-2026".data
where "CUUR0000SEHA" is not null
order by obs_date
```

```sql latest
select "CUUR0000SEHA" as rent_cpi
from "us-rent-affordability-2026".data
where "CUUR0000SEHA" is not null
order by observation_date::date desc
limit 1
```

<BigValue
  data={latest}
  value="rent_cpi"
  title="CPI rent index, latest (1982–84 = 100)"
  fmt="#,##0.0"
/>

## The long-run trend, 1914–2026

The flat interwar plateau, the 1970s acceleration, and the post-2021 jump are all visible on one line.

<LineChart
  data={primary}
  x="obs_date"
  y="rent_cpi"
  title="CPI rent index — US city average"
  xAxisTitle="Year"
  yAxisTitle="Index (1982–84 = 100)"
/>

## How inflationary was each decade?

The 2020s are on pace to rival the 1970s as the most rent-inflationary decade in the modern era — despite a lower headline-inflation backdrop.

```sql decades
with base as (
  select
    (floor(year(observation_date::date) / 10) * 10)::int as decade_start,
    "CUUR0000SEHA" as rent_cpi
  from "us-rent-affordability-2026".data
  where "CUUR0000SEHA" is not null
)
select
  concat(decade_start::varchar, 's') as decade,
  round((max(rent_cpi) - min(rent_cpi)) / min(rent_cpi) * 100, 1) as pct_change
from base
group by decade_start
order by decade_start
```

<BarChart
  data={decades}
  x="decade"
  y="pct_change"
  title="Rent CPI % change within each decade"
  xAxisTitle="Decade"
  yAxisTitle="% change"
/>

---

*Source: [FRED](https://fred.stlouisfed.org/series/CUUR0000SEHA) series CUUR0000SEHA (BLS, Rent of Primary Residence). Public domain. Pre-1940 data is December-only, so sub-annual analysis should start in the 1940s. This is a price index, not a dollar rent level.*
