---
title: Ev Adoption Norway Vs World
---

# EV Adoption: Norway vs. The World


## What it is
Country-year panel from Our World in Data (sourced from the IEA Global EV Outlook) tracking the share of new car sales that are electric. 817 rows spanning ~2010–2025 across dozens of countries, with columns Entity, Code, Year, and 'Share of new cars that are electric'.

## Why it's interesting *now*
EV sales share is the cleanest single indicator of the energy transition in road transport, and 2024–2025 is the moment several laggard markets crossed double digits while US growth visibly stalled. With Trump-era EV policy rollbacks and China's BYD surge dominating headlines, this dataset lets you cut through the noise with a single defensible number per country per year.

## The headline finding
Australia — often dismissed as an EV laggard — went from 2.7% EV share in 2021 to 15% in 2025, a ~5.5x jump in four years that puts it on the same trajectory Norway walked a decade earlier.

## Caveats
CC-BY license (attribute Our World in Data + IEA). 'Electric' includes both BEV and PHEV per IEA methodology — a pure-BEV analysis would look different. Country coverage and start years are uneven (some countries only have 3–5 data points), so cross-country comparisons in early years are noisy. 2025 figures are preliminary IEA estimates.

```sql primary
select * from "ev-adoption-norway-vs-world".data
```

<DataTable data={primary} />
