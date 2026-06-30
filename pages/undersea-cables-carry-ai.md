---
title: The Internet Has a Floor, and It's at the Bottom of the Ocean
description: We picture the internet as wireless and the cloud as weightless. Almost all of it actually runs through glass cables on the seabed — and AI is driving the biggest build-out in their history.
---

Ask an AI a question and the answer probably crossed an ocean floor to reach you. We talk about "the cloud" as if it were weightless, and about the internet as if it were wireless. Almost none of it is. Roughly **99% of all intercontinental data** — every video call, every bank transfer, every chatbot reply that hops between continents — travels through fibre-optic cables lying on the seabed, some no thicker than a garden hose.

This is a story without a tidy dataset. It's a story told in a handful of numbers that are hard to believe until you sit with them.

<div class="stat-grid">
  <div class="stat">
    <span class="stat-num">694</span>
    <span class="stat-label">submarine cable systems active or under construction in 2026</span>
  </div>
  <div class="stat">
    <span class="stat-num">~99%</span>
    <span class="stat-label">of intercontinental internet and AI traffic carried by undersea cable</span>
  </div>
  <div class="stat">
    <span class="stat-num">~$13B</span>
    <span class="stat-label">in new cable projects 2025–2027 — nearly double the previous three years</span>
  </div>
  <div class="stat">
    <span class="stat-num">50,000 km</span>
    <span class="stat-label">length of the longest cable ever planned — enough to wrap the equator 1.25 times</span>
  </div>
  <div class="stat">
    <span class="stat-num">~75%</span>
    <span class="stat-label">of international bandwidth now owned by cloud giants, up from near zero in 2010</span>
  </div>
  <div class="stat">
    <span class="stat-num">68</span>
    <span class="stat-label">additional cables expected to come online by 2027</span>
  </div>
</div>

## A map most people never see

TeleGeography, which tracks the world's cables, counts **694 systems and 1,893 landing points** active or under construction in its 2026 map. Each landing point is a nondescript building on a coastline — often an unmarked beachfront hut — where a cable comes ashore and the entire internet of a region narrows to a single bundle of fibre. The whole edifice of cloud computing rests on a few hundred of these threads.

For most of their history, cables were laid by consortia of telecom carriers splitting the cost. That has flipped. Cloud companies now own or co-own about **75% of international bandwidth**, a share that was essentially zero in 2010. The internet's plumbing has quietly changed hands.

## Why the sudden surge

Cable-laying is booming, and the reason is the same one behind the power-grid strain we've [written about](/data-stories/ireland-data-centers): AI. Training and serving large models shuttles enormous volumes of data between data centers scattered across continents, and that traffic has to physically move. Investment in new cables is running at roughly **$13 billion for 2025–2027, nearly twice** the prior three-year window, with around **68 more cables** due by 2027.

The headline project shows the new scale. **Project Waterworth** is planned to run **50,000 kilometres** across five continents — long enough to circle the Earth one and a quarter times — at an estimated **$10 billion**. A single cable, longer than any before it, built for one purpose: moving model data across oceans.

## The takeaway

The cloud is not in the sky. It's a physical network with a floor, and that floor is at the bottom of the ocean — a few hundred fragile strands of glass that the entire digital economy, and now the entire AI economy, runs across. The next time a chatbot answers you in a second, picture the seabed it just travelled.

---

*Sources: [TeleGeography 2026 Submarine Cable Map](https://www.submarinecablemap.com/) (systems, landings, the ~99% and ~75% figures); [Analysys Mason](https://www.analysysmason.com/research/content/articles/submarine-cable-launches-rma22-rdfi0/) (cable launches and 2027 forecast); investment and Project Waterworth figures via [DatacenterDynamics](https://www.datacenterdynamics.com/en/analysis/submarine-cables-find-new-impetus-under-hyperscalers/) and industry reporting. Figures are industry estimates; "intercontinental traffic" excludes data that stays within a single landmass.*

<style>
  .stat-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 1rem;
    margin: 2rem 0 2.5rem 0;
  }
  .stat {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    padding: 1.5rem 1.4rem;
    border-radius: 16px;
    border: 1px solid rgba(69,161,191,0.25);
    background:
      linear-gradient(160deg, rgba(11,31,51,0.04), rgba(69,161,191,0.06));
  }
  .stat-num {
    font-size: clamp(1.9rem, 4vw, 2.6rem);
    font-weight: 800;
    line-height: 1;
    letter-spacing: -0.02em;
    color: #2f7fa0;
  }
  .stat-label {
    font-size: 0.92rem;
    line-height: 1.45;
    opacity: 0.78;
  }
</style>
