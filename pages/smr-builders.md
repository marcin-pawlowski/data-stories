---
title: Everyone's Racing to Build a Small Nuclear Reactor. China Already Finished One.
description: Small modular reactors are pitched as the answer to AI's power demand. A dozen companies are building them — but only one design is actually going live in 2026, and it isn't American.
---

Small modular reactors — SMRs — are the energy industry's current favorite answer to a problem we've [covered before](/data-stories/ireland-data-centers): the electricity that AI and data centers need, faster than big conventional plants can deliver it. The pitch is appealing: factory-built reactors, small enough to site next to a data center, quick to deploy. A dozen companies are racing to build them, several now publicly listed.

But "racing" is doing a lot of work in that sentence. Strip away the announcements and look at what's actually being built, and one fact stands out: the first land-based commercial SMR to switch on is in China, years ahead of every Western design.

```sql first_commercial
select capacity_mwe
from "smr-builders".data
where status like '%commercial%'
limit 1
```

<BigValue
  data={first_commercial}
  value="capacity_mwe"
  title="MWe — China's Linglong One, the first land-based commercial SMR (online 2026)"
/>

## The designs, by size

"Small" is relative. The designs below range from NuScale's 77-megawatt module to Rolls-Royce's 470 — the latter pushing the upper edge of what still counts as "modular." NuScale and X-energy are built to be ganged together into bigger plants; the others are single units. What they share is the promise of factory production instead of decade-long bespoke megaprojects.

```sql by_size
select
  design,
  capacity_mwe,
  country
from "smr-builders".data
order by capacity_mwe desc
```

<BarChart
  data={by_size}
  x="design"
  y="capacity_mwe"
  title="Net electrical output per reactor or module (MWe)"
  xAxisTitle="MWe per unit"
  yAxisTitle=""
  swapXY=true
/>

## Who's actually building, and where

Valuation and press releases are easy; first concrete is hard. The table below sorts the talk from the steel. China's Linglong One is entering commercial operation. Canada's Darlington has a GE Hitachi BWRX-300 physically under construction. Almost everything else — including America's NRC-certified NuScale — is still in licensing or site-selection, with no reactor yet being built.

```sql builders
select
  design as "Design",
  company as "Company",
  country as "Lead country",
  capacity_mwe as "MWe",
  status as "Status",
  ownership as "Ownership"
from "smr-builders".data
order by capacity_mwe desc
```

<DataTable data={builders} rows=10 />

## Why it matters

For investors, the listed SMR names (NuScale, Oklo, X-energy, Rolls-Royce) are a way to bet on the AI-power build-out without buying the chipmakers everyone already owns. For everyone else, the table is a reality check: the technology is real and the demand is real, but commercial SMR power is mostly a 2030s story in the West — and a 2026 fact in China. The gap between the two is the thing actually worth watching.

---

*Sources: design capacities and status compiled from the [World Nuclear Association](https://world-nuclear.org/information-library/nuclear-power-reactors/small-modular-reactors/small-modular-reactors), [World Nuclear News](https://www.world-nuclear-news.org/), [US EIA](https://www.eia.gov/todayinenergy/detail.php?id=67584), and company filings (2025–2026). Capacities are net electrical output per reactor or module; multi-module plants reach higher totals. Status reflects publicly reported progress as of mid-2026.*
