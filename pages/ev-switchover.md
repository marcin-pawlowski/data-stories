---
title: In Norway, the Petrol Car Is Already Over
description: 97% of new cars sold in Norway are now electric. Plot that against China, Europe and the US and you see four very different speeds of the same transition.
---

The switch to electric cars is usually argued about as a forecast — when will it happen, will it happen at all. In one country the argument is settled. In 2025, **97% of new cars sold in Norway were electric**. The petrol car didn't get banned there; it simply stopped being what people buy. The interesting question is no longer whether the switchover happens, but how unevenly — because plot Norway against China, Europe and the United States and you get four completely different speeds.

```sql norway_latest
select "Share of new cars that are electric" as share
from "ev-sales-share".data
where Entity = 'Norway'
order by Year desc
limit 1
```

<BigValue
  data={norway_latest}
  value="share"
  title="Share of new cars sold in Norway that are electric (2025)"
  fmt='0"%"'
/>

## Four speeds of the same transition

Norway is essentially finished. China — the world's largest car market by far — crossed **53%**, meaning more than half of its enormous new-car volume is now electric. The European Union sits around **27%**, still climbing. And the United States, despite building much of the technology, is at just **10%**: the same transition, running roughly a decade behind Norway.

```sql trends
select
  Entity,
  Year,
  "Share of new cars that are electric" as share
from "ev-sales-share".data
where Entity in ('Norway', 'China', 'European Union (27)', 'United States', 'World')
  and Year >= 2015
order by Entity, Year
```

<LineChart
  data={trends}
  x="Year"
  y="share"
  series="Entity"
  title="Share of new cars that are electric, 2015–2025"
  yAxisTitle="Share of new cars (%)"
  xAxisTitle="Year"
  yFmt='0"%"'
/>

## Who's ahead in 2025

The top of the list is mostly Northern Europe and China — but the surprises are the story. **Nepal ranks third**, and Vietnam, Laos and Singapore all crack the top fifteen, powered by cheap (often hydro) electricity, mass two-wheeler electrification and aggressive home-grown EV makers. Meanwhile large, car-dependent economies like the US cluster far lower down. The gap between top and bottom is enormous: the leaders are nearly done while others have barely begun.

```sql snapshot
select
  Entity,
  "Share of new cars that are electric" as share
from "ev-sales-share".data
where Year = 2025
  and Entity not in ('World', 'Europe', 'European Union (27)')
order by share desc
limit 15
```

<BarChart
  data={snapshot}
  x="Entity"
  y="share"
  title="Top 15 countries by electric share of new car sales, 2025"
  xAxisTitle="Share of new cars (%)"
  swapXY=true
  yFmt='0"%"'
/>

## What changes next

Norway is a warning against reading any single year as the finish line. Even there the policy is shifting — from 2026 the tax break that drove adoption starts being clawed back on pricier cars and is set to disappear entirely by 2028. The lesson from the leaders isn't that the transition is automatic; it's that it moves fast once charging and incentives line up — and stalls without them. The US line is the one to watch: it shows what a slow lane looks like.

---

*Source: [Our World in Data](https://ourworldindata.org/grapher/electric-car-sales-share), compiling [IEA Global EV Outlook](https://www.iea.org/reports/global-ev-outlook-2026) estimates. Licensed [CC BY](https://creativecommons.org/licenses/by/4.0/). "Electric" includes both battery-electric and plug-in hybrid cars; 2025 values are IEA estimates.*
