# Business Insights 360

A multi-page executive analytics dashboard built in Power BI, consolidating Finance, Sales, Marketing, Supply Chain, and Executive views into a single connected reporting tool, backed by a star-schema data model.

## Project Goals

1. Give different stakeholders (finance, sales, marketing, supply chain, and executives) a single source of truth for performance metrics, instead of siloed reports per department.
2. Track profitability (P&L, Gross Margin, Net Profit%) alongside operational metrics (forecast accuracy, market share, inventory risk) in one tool.
3. Enable drill-down from company-wide totals down to individual regions, customers, and products.

## Data Model

The dashboard is built on a star schema with:

- **Fact tables**: `fact_actuals_estimates`, `fact_forecast_monthly`
- **Dimension tables**: `dim_customer`, `dim_date`, `dim_market`, `dim_product`
- **Supporting tables**: `freight_cost`, `gross_price`, `manufacturing_cost`, `operational expenses`, `marketshare`, `NsGmTarget`, and P&L-specific measure tables

This structure lets the same underlying facts feed every page (Finance, Sales, Marketing, Supply Chain, Executive) without duplicating data, and supports filtering by region/market, customer, segment/category/product, and year/quarter consistently across all views.

## Tech Stack

- **Power BI** — data model, DAX measures, and all report pages
- **Star schema data modeling** — fact and dimension tables connected for efficient, reusable filtering across pages

## Dashboard Pages

**Home** — Landing page with navigation to each view (Finance, Sales, Marketing, Supply Chain, Executive) and usage info.

**Finance View** — P&L statement (Gross Sales → Net Sales → Gross Margin → Net Profit), Net Sales performance over time, and top/bottom products and customers by Net Sales, all against benchmark (BM) and change (Chg/Chg%).

**Sales View** — Customer performance table (Net Sales, Gross Margin, Gross Margin%, % of Total NS), a region-based performance matrix (bubble chart of Net Sales vs. GM%), product segment performance, and a unit economics breakdown (Gross Price → Net Sales → COGS → Gross Margin).

**Sales Trend** — Trend visuals for customer- or product-level Net Sales and GM% over time.

**Marketing View** — Segment-level performance matrix (Net Sales vs. GM% vs. Net Profit%, sized/colored by division), plus region/market/customer performance with Net Profit and Net Profit%.

**Supply Chain View** — Forecast accuracy and net error tracking by customer and by product segment, with a risk flag (OOS = Out of Stock, EI = Excess Inventory).

**Executive View** — Top-level rollup: Revenue by Division and by Channel, yearly trend of Revenue/GM%/Net Profit%/Market Share%, key metrics by sub-zone (region), PC market share trend vs. competitors, and Top 5 Customers/Products by Revenue.

## Key Metrics (2022 snapshot, company-wide)

| Metric | Value | vs. Benchmark |
|---|---|---|
| Net Sales | $1,052.34M | +364.36% |
| Gross Margin % | 37.70% | +3.26% |
| Net Profit % | −13.99% | −114.79% |
| Forecast Accuracy | 72.04% | −10.77% (vs. LY) |

## Business Insights

- **Profitability gap despite strong sales growth**: Net Sales are up dramatically (+364% vs. benchmark) and Gross Margin is healthy at 37.7%, but Net Profit% is negative at −13.99%, meaning operating costs (manufacturing, freight, operational expenses) are eating into gross margin faster than revenue is scaling. This points to a cost-control problem rather than a demand problem.
- **APAC drives revenue, but not proportionally profitably**: APAC leads all regions in Net Sales ($550.22M, the largest single region), but Net Profit% across regions is negative everywhere (EU −12.44%, APAC −14.57%, LATAM −2.13%, NA −14.18%), so even the top-performing region isn't converting sales into profit.
- **Forecast accuracy has declined year over year**: down to 72.04% from 80.73% last year, with a large net error (−4,739.4K), worse than last year's −273K. This is a meaningful red flag for supply chain planning, since inaccurate forecasts tend to cascade into excess inventory (flagged as "EI") or stockouts (flagged as "OOS") at the product-segment level.
- **Revenue concentration in a small customer/product base**: the Top 5 customers account for ~39% of total revenue, and the Top 5 products account for ~21%, useful to know for account-management prioritization, but also a concentration risk if any of those relationships weaken.
- **Competitive position**: AtliQ holds an estimated ~22% PC market share, ahead of named competitors (bp, dale, innovo, pacer) individually, but still a minority share overall, suggesting room to grow rather than a dominant position to defend.

*Note: these insights are drawn directly from the metrics shown on the dashboard. Since the underlying dataset wasn't independently available for recomputation, treat the specific percentages as reported by the dashboard rather than externally verified figures.*

## Repository Structure

```
├── Business-Insights-360.pbix    # Power BI dashboard file (8 pages)
├── screenshots/                   # Dashboard page previews
└── README.md
```

## Next Steps

- Investigate the cost drivers behind negative Net Profit% despite strong top-line growth (freight, manufacturing cost, or operational expense trends by region).
- Root-cause the forecast accuracy decline, and identify which customers/products are consistently flagged OOS or EI.
