---
title: Watching Half the World Switch On
description: A new open dataset opens up daily electricity demand for 12 South and Southeast Asian countries. India's decade-long climb — up more than 50% — is the clearest picture yet of a continent plugging in.
---

Most energy stories are about the rich world: American grids, European prices, the AI data centers we [keep](/data-stories/ai-data-center-power-demand) [coming](/data-stories/ireland-data-centers) back to. But the fastest-growing electricity demand on the planet is in South and Southeast Asia, where hundreds of millions of people are buying their first air conditioner, fridge or electric scooter. A new open dataset now tracks daily electricity demand across 12 of these countries — and the standout is India, the only one with a clean decade of data.

```sql india_scale
select round(mean_daily_mwh / 1e6, 2) as m
from "asia-power-scale".data
where country = 'India'
```

<BigValue
  data={india_scale}
  value="m"
  title="Million MWh per day — India's average demand (2023–24), about 7× any neighbor"
  fmt='0.00'
/>

## India: a decade of plugging in

India's average daily electricity demand rose **more than 50%** between 2014 and 2023 — from roughly 2.85 to 4.36 million megawatt-hours a day. The annual sawtooth is the giveaway: every year demand spikes through the pre-monsoon summer, when hundreds of millions of air conditioners and fans run at once, then eases. Those summer peaks are climbing faster than the average — the signature of a country getting both richer and hotter.

```sql india_monthly
select
  month::date as month,
  mean_daily_mwh
from "india-power-monthly".data
order by month
```

<LineChart
  data={india_monthly}
  x="month"
  y="mean_daily_mwh"
  title="India: average daily electricity demand by month (MWh)"
  yAxisTitle="MWh per day"
  xAxisTitle="Year"
/>

## The rest of the region, to scale

India is in a league of its own — its daily demand is nearly seven times Taiwan's, the next largest in the dataset. Setting India aside to make the others legible, the rest of the region spans two orders of magnitude, from Taiwan and Thailand down to Bhutan. Each bar is that country's average daily demand over its most recent year of available data.

```sql scale
select
  country,
  mean_daily_mwh
from "asia-power-scale".data
where country != 'India'
order by mean_daily_mwh desc
```

<BarChart
  data={scale}
  x="country"
  y="mean_daily_mwh"
  title="Average daily electricity demand, excluding India (MWh)"
  xAxisTitle="MWh per day"
  yAxisTitle=""
  swapXY=true
/>

## Why it matters

How this demand gets met — coal, solar, gas, or the small reactors we [wrote about](/data-stories/smr-builders) — is one of the defining questions of the next two decades, and it will be decided largely in Asia, not the West. India alone is adding the equivalent of a mid-sized country's entire grid every few years. The line above is what energy transition looks like from the demand side: not a policy debate, but hundreds of millions of people switching something on for the first time.

---

*Source: [Open-access energy demand data for South and Southeast Asia](https://doi.org/10.5281/zenodo.17175212) (Zenodo), licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Daily national electricity demand in MWh; coverage periods differ by country, so cross-country comparisons use each country's most recent year of data. Dataset is a preprint in review (ESSD, 2026). Figures reflect metered/grid demand as compiled by the authors, not necessarily total national consumption.*
