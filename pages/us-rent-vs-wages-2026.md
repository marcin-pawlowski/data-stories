---
title: Us Rent Vs Wages 2026
---

# Six Decades of American Paychecks: Average Hourly Earnings, 1964–2026


## What it is
FRED series AHETPI: monthly average hourly earnings in USD for production and nonsupervisory employees in the total private sector, published by the U.S. Bureau of Labor Statistics. Two columns (observation_date, AHETPI), 750 monthly observations from January 1964 through May 2026.

## Why it's interesting *now*
Rent-vs-wage anxiety is dominating mid-2026 economic discourse, and AHETPI is *the* wage series that captures what rank-and-file workers (not managers) actually earn. Pairing this nominal wage line with shelter CPI is the cleanest way to show whether take-home pay is keeping up with housing costs right now.

## The headline finding
In January 1964, the average production worker earned $2.50/hour; by May 2026 that number crosses into double digits many times over — but nominal wages hide the real story, because a 1964 dollar and a 2026 dollar buy very different apartments.

## Caveats
AHETPI is nominal (not inflation-adjusted) and covers only production/nonsupervisory workers, so it excludes managers and salaried professionals — which is a feature for a 'working-class wages' story but a bug if you want the whole labor market. Series definitions changed in 2006 when BLS extended coverage to all private industries; pre-2006 values reflect a narrower industry mix. To tell the rent-vs-wages story you'll need to separately pull the shelter CPI series (CUSR0000SAH1 or CPIHOSSL) — this file only contains wages. License is public domain / CC-BY via FRED; always cite BLS as the original source.

```sql primary
select * from "us-rent-vs-wages-2026".data
```

<DataTable data={primary} />
