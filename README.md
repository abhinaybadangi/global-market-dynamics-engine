# Global Market Dynamics Engine

An interactive Power BI storytelling project that tracks how global market leaders evolve over time, identifies the fastest-growing companies, and explains the business forces behind shifting market momentum.

## Overview

Most dashboards show static snapshots.

This project was built to answer a more strategic question:

**How do market leaders change over time, who is accelerating fastest, and what macro business shifts are driving that change?**

Using a curated multi-industry dataset across Tech, E-commerce, Automotive, EV, and Streaming, this Power BI solution combines:
- an animated revenue race view,
- momentum and growth analysis,
- recent growth leader identification,
- and industry-level comparative insights.

The result is a portfolio project designed to demonstrate not just dashboarding, but analytical storytelling, DAX capability, and business interpretation.

## Business Objective

The objective of this project is to help decision-makers and analysts understand:

- which companies dominate market revenue over time,
- which companies are experiencing the strongest recent acceleration,
- how industry-level revenue concentration is shifting,
- and what strategic signals can be extracted from long-term market movement.

This project is positioned as a decision-support and storytelling solution rather than a static reporting dashboard.

## Dashboard Pages

### Page 1 — Global Market Revenue Race
A time-based animated bar chart race showing how leading companies evolve from 2015 to 2024.

**Key outputs:**
- Total market revenue
- Market leader in selected period
- Ranked market position by revenue
- Strategic annotation on market movement

### Page 2 — Market Momentum & Growth Analysis
A diagnostic page focused on recent growth and industry structure.

**Key outputs:**
- Highest recent growth %
- Highest recent growth company
- Overall market growth
- Revenue trend comparison
- Latest year growth by company
- Industry revenue comparison

## Skills Demonstrated

- Power BI dashboard design
- DAX measure development
- KPI design and validation
- Animated storytelling with custom visuals
- Trend and growth analysis
- Executive-style layout and insight writing
- Business interpretation of market shifts

## Core DAX Measures

```DAX
Total Revenue = SUM(MarketData[Revenue])

Highest Recent Growth % =
VAR LatestYear = MAX(MarketData[Year])
VAR PrevYear = LatestYear - 1
VAR GrowthTable =
    ADDCOLUMNS(
        ALL(MarketData[Company]),
        "GrowthValue",
            VAR CurrentRev =
                CALCULATE([Total Revenue], MarketData[Year] = LatestYear)
            VAR PrevRev =
                CALCULATE([Total Revenue], MarketData[Year] = PrevYear)
            RETURN DIVIDE(CurrentRev - PrevRev, PrevRev)
    )
RETURN
MAXX(GrowthTable, [GrowthValue])

Overall Market Growth % =
VAR LatestYear = MAX(MarketData[Year])
VAR PrevYear = LatestYear - 1
VAR CurrentMarketRevenue =
    CALCULATE([Total Revenue], ALL(MarketData[Company]), MarketData[Year] = LatestYear)
VAR PreviousMarketRevenue =
    CALCULATE([Total Revenue], ALL(MarketData[Company]), MarketData[Year] = PrevYear)
RETURN
DIVIDE(CurrentMarketRevenue - PreviousMarketRevenue, PreviousMarketRevenue)
```

## Dataset section

```md
## Dataset

The dataset was compiled from publicly available company financial information and standardized into a structured analytical format for storytelling and dashboard development.

**Coverage:**
- 15 global companies
- 5 industries
- 2015–2024 period
- Revenue values standardized in USD billions
```

