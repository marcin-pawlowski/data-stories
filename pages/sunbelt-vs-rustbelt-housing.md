---
title: Sunbelt Vs Rustbelt Housing
---

# Sun Belt vs. Rust Belt: The Great Housing Market Reversal (2020-2026)


## What it is
Zillow's monthly ZHVI (smoothed, seasonally adjusted, mid-tier all-homes) for ~895 US metros from January 2000 through April 2026, sourced directly from Zillow Research. Each row is one geography (US, MSA) with ~315 monthly price columns — making YoY and peak-to-trough math trivial for every metro on the same axis.

## Why it's interesting *now*
The post-pandemic Sun Belt boom has clearly cracked: Phoenix, Dallas, Houston, Miami, and Tampa are all printing negative YoY changes in late 2025, while legacy Rust Belt and Northeast metros (Detroit, Chicago, Philadelphia, New York) are still climbing. This dataset captures the exact moment the 2020-2022 narrative inverted — and the April 2026 values let you show forward Zillow-projected continuation, not just a backward look.

## The headline finding
Dallas home values peaked at $397.6K in August 2022 and are projected at $366.7K by April 2026 — a 7.8% nominal decline over nearly four years — while Detroit, the poster child of Rust Belt decline, rose from $238K to $266K (+11.9%) over the same window.

## Three chart ideas

1. **Slope chart / dumbbell** — y = metro (RegionName), x1 = ZHVI at 2022-08-31 peak, x2 = ZHVI at 2026-04-30; color = red if declining, green if rising. Viewer learns: Instantly shows which metros gave back pandemic gains (Dallas, Phoenix, Austin, Tampa) versus which kept compounding (Detroit, Chicago, NYC, Boston).

2. **Small-multiple line chart** — x = month (2019-01 to 2026-04), y = ZHVI indexed to 100 at Jan 2020, one panel per metro, color = Sun Belt vs Rust Belt. Viewer learns: Reveals the V-shape in Sun Belt metros (sharp run-up, rolling over by mid-2022) versus the steadier staircase in Rust Belt metros.

3. **Diverging bar chart** — y = top 20 metros by SizeRank, x = YoY % change from 2024-10 to 2025-10; color = sign of change. Viewer learns: A single 'who's hot, who's not' snapshot for late 2025 — Dallas/Phoenix/Miami negative, Detroit/Chicago/NY/Philly positive.


## Suggested LinkedIn angle
> I pulled Zillow's metro-level home value index back to 2000 and the reversal jumped off the screen: Dallas home values are now lower than they were in August 2022, while Detroit — yes, Detroit — has quietly added nearly 12% over the same stretch. The 2021 'move to the Sun Belt' trade has fully unwound in the data, and I don't think the headlines have caught up yet.

## Caveats
ZHVI is a smoothed, seasonally adjusted mid-tier index — it understates volatility and lags transaction prices by a few weeks. Values past the current release date (roughly early 2026 in this file) are Zillow's forecast, not observed sales, and should be labeled as such. Metro boundaries are MSA-level, so intra-metro divergence (e.g., Austin core vs. exurbs) is hidden. Nominal dollars only — no inflation adjustment, which materially flatters the Rust Belt 'gains' in real terms. CC BY license requires attribution to Zillow.

## The chart

```sql metro_change
select 
  regionname as metro,
  case 
    when statename in ('TX', 'FL', 'AZ', 'NV', 'GA', 'NC', 'TN', 'SC') then 'Sun Belt'
    when statename in ('MI', 'OH', 'PA', 'IL', 'IN', 'NY', 'MA', 'CT', 'NJ') then 'Northeast / Rust Belt'
    else 'Other'
  end as region,
  round(("2026-04-30" - "2020-01-31") / "2020-01-31" * 100, 1) as pct_change_pct
from "sunbelt-vs-rustbelt-housing".data
where regiontype = 'msa' and sizerank between 1 and 25
order by pct_change_pct
```

<BarChart 
  data={metro_change}
  x=metro
  y=pct_change_pct
  series=region
  title="Home value change, top 25 US metros, Jan 2020 → Apr 2026"
  yAxisTitle="% change in ZHVI since January 2020"
  swapXY=true
  sort=false
/>

## Raw values for the same metros

```sql snapshot
select 
  regionname,
  sizerank,
  statename,
  round("2020-01-31") as zhvi_jan_2020,
  round("2022-08-31") as zhvi_aug_2022_peak,
  round("2026-04-30") as zhvi_apr_2026
from "sunbelt-vs-rustbelt-housing".data
where regiontype = 'msa' and sizerank between 1 and 25
order by sizerank
```

<DataTable data={snapshot} />
