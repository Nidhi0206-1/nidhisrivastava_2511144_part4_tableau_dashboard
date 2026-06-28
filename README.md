# Retail Executive Dashboard — Tableau

## Business Problem

The retail leadership team needs a single dashboard to monitor sales performance, profitability, customer behavior, and operational metrics across their business. Without a consolidated view, leadership is working from disconnected spreadsheet reports that make it difficult to spot risks, compare regions, or understand what is driving profit variability.

This dashboard answers four core leadership questions:

- Where is the business making money, and where is it losing it?
- Which regions and segments should receive more investment?
- Is the operational side of the business — shipping, returns, discounts — creating hidden costs?
- What does the next quarter look like given current trends?

---

## Dataset Description

**File:** `data/dashboard_sales_data.xlsx`  
**Rows:** 4,200 orders  
**Period:** January 2024 — December 2025  
**Source:** Internal transactional data, provided for this analysis

| Field | Type | Description |
|---|---|---|
| order_id | Text | Unique order identifier |
| order_date | Date | Date order was placed |
| ship_date | Date | Date order was shipped |
| customer_id | Text | Unique customer identifier |
| customer_segment | Categorical | Consumer, Corporate, or Home Office |
| region | Categorical | North, South, East, West |
| state | Categorical | US state |
| city | Categorical | City |
| category | Categorical | Furniture, Office Supplies, Technology |
| sub_category | Categorical | 13 sub-categories |
| product_name | Text | Product name |
| ship_mode | Categorical | Same Day, First Class, Second Class, Standard Class |
| sales | Numeric | Revenue in USD |
| quantity | Integer | Units ordered |
| discount | Numeric | Discount rate (0.00 to 0.35) |
| profit | Numeric | Profit in USD (can be negative) |
| return_flag | Binary | 1 = returned, 0 = not returned |
| delivery_days | Integer | Days from order to delivery |
| customer_rating | Numeric | Rating from 2.1 to 5.0 |
| campaign_channel | Categorical | Organic, Social, Referral, Paid, Email |

---

## Tableau Workbook

**File:** `tableau/executive_dashboard.twbx`

The packaged workbook contains the following sheets and one executive dashboard:

| Sheet Name | Purpose |
|---|---|
| Sales Trend | Monthly sales and profit over 2024–2025 |
| Regional Performance | Sales and profit by region (map + bar) |
| Category Profitability | Treemap of sub-category sales and margin |
| Customer Segment View | Segment comparison by sales, profit, AOV |
| Shipping Performance | Delivery days by ship mode and delivery bucket |
| Discount vs Profit | Scatter plot of discount rate vs. per-order profit |
| Return Analysis | Highlight table of return rates by category and segment |
| KPI Summary | Calculated KPI cards for the dashboard header |

---

## Calculated Fields

| Field Name | Formula | Business Use |
|---|---|---|
| Profit Margin | `SUM([profit]) / SUM([sales])` | Overall profitability efficiency |
| Cost | `SUM([sales]) - SUM([profit])` | Derived cost base from available data |
| Average Order Value | `SUM([sales]) / COUNT([order_id])` | Revenue per transaction |
| Return Rate | `SUM([return_flag]) / COUNT([order_id])` | Share of orders returned |
| Shipping Delay Bucket | IF/ELSEIF on delivery_days (Express ≤1, Fast 2–3, Standard 4–5, Slow 6+) | Delivery tier classification |
| Discount Band | IF/ELSEIF on discount (No Discount, Low 1–10%, Medium 11–20%, High 21–35%) | Discount impact segmentation |
| Order Year | `YEAR([order_date])` | Year-over-year comparison |

---

## Dashboard Components

**Executive Dashboard** includes:

- **KPI Cards (header row):** Total Sales, Total Profit, Profit Margin %, Return Rate %, Average Order Value
- **Sales Trend chart:** Monthly dual-axis line chart (Sales + Profit) with date range filter
- **Regional Performance:** Filled map + bar chart showing region sales and profit
- **Category Profitability:** Treemap by sub-category (size = sales, color = margin)
- **Customer Segment view:** Grouped bar chart comparing segments
- **Shipping Performance:** Bar chart by ship mode with 5-day threshold reference line
- **Discount vs Profit:** Scatter plot highlighting the margin erosion curve
- **Return Analysis:** Highlight table by category and segment

---

## Filters and Interactions

**Filters available on the dashboard:**

| Filter | Type | Applies To |
|---|---|---|
| Date Range | Continuous date slider | Sales Trend, all KPI cards |
| Region | Multi-select dropdown | All sheets |
| Category | Multi-select dropdown | All sheets |
| Customer Segment | Multi-select dropdown | Segment, Return, Discount views |
| Ship Mode | Multi-select dropdown | Shipping, Return views |

**Dashboard Actions:**

- Clicking a region on the map filters the bar chart and all segment/category views to that region
- Clicking a category cell in the treemap filters the return table and discount scatter to that category
- Hovering over any data point shows a tooltip with Order ID, Sales, Profit, and Margin for that record

---

## Key Business Insights

1. Technology generates 84% of total profit with 18.2% margin — the business depends on this category
2. Furniture has the lowest margin (6.9%) and the highest return rate (7.7%) — a double risk
3. The South region leads in both sales ($64.7M) and profit ($10.0M)
4. Orders with 25–35% discounts generate average profit of only $2,729 vs. $11,182 for minimal-discount orders
5. Standard Class shipping averages 4.7 days — 16% of all orders take 6 or more days
6. Organic channel drives $88.8M in sales — the single most productive marketing channel
7. July–August 2025 were the two highest-revenue months on record
8. Tables and Bookcases sit at 5.7% margin — the two lowest-performing sub-categories in the business

---

## Dashboard Story Summary

The business is profitable overall, but the story is not uniform. Technology is the engine — without it, the numbers look very different. Furniture is the risk — thin margins and high returns make it the most vulnerable category. Discounting above 20% is quietly destroying margin without a visible volume offset.

The South region and Home Office segment are the strongest performers. The West region has growth potential but has not reached the same output as the South. Operationally, Standard Class shipping is creating delivery friction for a meaningful share of customers.

The recommended focus areas are: protect Technology margin, fix Furniture profitability, cap discounts at 20%, and improve the Standard Class delivery experience.

---

## Assumptions and Limitations

- All monetary values are assumed to be in USD
- Delivery days are calculated as the difference between ship_date and order_date. Where delivery_days = 0, it is treated as Same Day fulfillment and not an error
- Approximately 32 records have no campaign_channel value and are excluded from channel-level analysis
- Return flag is binary (0/1). No return reason codes are available in this dataset, so return root cause cannot be determined from this data alone
- The dashboard does not include customer acquisition cost, so channel ROI is measured by sales and profit contribution only, not net return
- Two years of data (2024–2025) is sufficient for trend analysis but limits the ability to identify multi-year seasonality patterns with confidence

---

## Screenshots

| File | Description |
|---|---|
| `screenshots/full_dashboard.png` | Complete executive dashboard with all views and filters |
| `screenshots/sales_trend_view.png` | Monthly sales and profit trend (2024–2025) |
| `screenshots/regional_performance_view.png` | Region map and bar chart |
| `screenshots/category_profitability_view.png` | Sub-category treemap |
| `screenshots/filter_interaction_view.png` | Dashboard with South region filter applied |

---

## Repository Structure

```
part4_tableau_dashboard/
├── data/
│   └── dashboard_sales_data.xlsx
├── tableau/
│   └── executive_dashboard.twbx
├── outputs/
│   ├── dashboard_story.md
│   ├── business_insights.md
│   └── chart_selection_justification.md
├── screenshots/
│   ├── full_dashboard.png
│   ├── sales_trend_view.png
│   ├── regional_performance_view.png
│   ├── category_profitability_view.png
│   └── filter_interaction_view.png
└── README.md
```
