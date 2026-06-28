# Chart Selection Justification — Executive Dashboard

This document explains the design decisions behind each visualization in the executive dashboard. Every chart was selected to answer a specific business question, not for aesthetic reasons.

---

## 1. Sales Trend — Dual-Axis Line Chart

**Business question:** How are monthly sales and profit moving over time, and are they tracking together?

**Chart selected:** Line chart with dual axis (Sales on primary axis, Profit on secondary axis), plotted by month.

**Why this chart:** Time-series data belongs on a line chart. A bar chart would work for monthly totals but makes it harder to read directional momentum. The dual axis allows leadership to see at a glance whether sales growth is translating into profit growth or whether margins are compressing.

**Encoding:** Date on the X axis (continuous). Sales as a blue line. Profit as an orange line on the right axis. Reference lines added for the 2-year average of each measure.

**Filters applied:** Date range slider covering Jan 2024 to Dec 2025. Region and Segment quick filters to allow drill-down.

**Design principle applied:** Minimal gridlines, clean axis labels, no chart border. The legend is kept to two items. Month labels are rotated only when space requires it.

**Mistake avoided:** Avoided stacking both metrics on the same axis, which would have made Profit almost invisible given the scale difference between the two measures.

---

## 2. Regional Performance — Filled Map + Bar Chart Combination

**Business question:** Which regions are generating the most revenue and profit, and is there a geographic concentration?

**Chart selected:** Filled map showing sales by region (color intensity), paired with a horizontal bar chart ranking regions by profit.

**Why this chart:** A map immediately grounds the audience geographically. For an executive audience, seeing "South is darker (higher sales)" requires no explanation. The bar chart alongside it provides the precise numeric comparison the map cannot convey.

**Encoding:** Map — region boundaries filled with a sequential blue color palette (lighter = lower, darker = higher). Bar chart — regions sorted descending by profit, with profit labels on bars.

**Filters applied:** Category and Ship Mode filters linked to both the map and bar chart via dashboard action.

**Design principle applied:** Single-hue sequential palette for the map to avoid implying qualitative differences between regions. Regions sorted by value in the bar chart, not alphabetically.

**Mistake avoided:** Avoided using a diverging color palette on the map, which would have implied that some regions are "negative" when all are profitable.

---

## 3. Category Profitability — Treemap

**Business question:** Which categories and sub-categories are the biggest contributors to revenue and profit, and how do they relate in size?

**Chart selected:** Treemap where rectangle size represents sales and color intensity represents profit margin.

**Why this chart:** A treemap shows part-to-whole relationships while simultaneously encoding two measures (size and color). For a category profitability view, it allows leadership to immediately spot high-revenue but low-margin areas — for example, Furniture sub-categories appear large but are lightly colored, revealing the margin problem at a glance.

**Encoding:** Size = Sales. Color = Profit Margin (sequential green palette — deeper green = higher margin). Labels show sub-category name and margin %.

**Filters applied:** Category and Region filters.

**Design principle applied:** Labels placed only on rectangles large enough to display them without crowding. Color legend included with explicit percentage markers.

**Mistake avoided:** Avoided using a simple bar chart stacked by sub-category, which would have buried the margin story and made the size comparison difficult to read.

---

## 4. Customer Segment View — Grouped Bar Chart

**Business question:** How do Consumer, Corporate, and Home Office segments compare on sales, profit, and average order value?

**Chart selected:** Grouped (side-by-side) bar chart with three bars per metric, one per segment.

**Why this chart:** When comparing a small number of categorical groups (three segments) across two or three measures, a grouped bar chart is the clearest option. It allows direct side-by-side comparison without the distortion of a stacked bar chart.

**Encoding:** X axis = metric (Sales, Profit, AOV). Bar clusters = segments (Consumer, Corporate, Home Office). Color = segment, using a distinct palette with three non-adjacent hues.

**Filters applied:** Region and Category filters, so leadership can drill into segment performance within a specific geography or product category.

**Design principle applied:** Consistent color assignment across all dashboard sheets — the same color represents each segment throughout the dashboard, so the legend does not need to be repeated on every chart.

**Mistake avoided:** Avoided using a pie chart to show segment sales share. Pie charts work for 2–3 slices with large differences; for three nearly equal segments, the visual difference is unreadable.

---

## 5. Shipping Performance — Bar Chart with Reference Line

**Business question:** Which shipping modes have the fastest delivery times, and how many orders fall into the "slow" bucket (6+ days)?

**Chart selected:** Horizontal bar chart showing average delivery days by shipping mode, with a reference line at 5 days marking the acceptable threshold. A secondary small bar chart shows order count by delivery day bucket.

**Why this chart:** A bar chart is the correct choice when comparing a continuous measure (average days) across a small set of categories (four shipping modes). Horizontal bars allow mode names to display fully without rotation.

**Encoding:** Bars sorted by average delivery days (ascending). Reference line at 5 days. Color encodes whether average is above or below the 5-day threshold (green = below, orange = above).

**Filters applied:** Region and Category filters.

**Design principle applied:** Reference line makes the threshold explicit, so leadership does not need to judge "is 4.7 days okay?" — the answer is visually immediate.

**Mistake avoided:** Avoided using a scatter plot for this view. With only four shipping modes, a scatter would have too few points to be meaningful and would not clearly communicate the delivery bucket distribution.

---

## 6. Discount vs. Profit — Scatter Plot

**Business question:** Is there a relationship between discount level and profit per order? At what discount level does profitability break down?

**Chart selected:** Scatter plot with Discount on the X axis and Profit on the Y axis, one dot per order.

**Why this chart:** A scatter plot is the appropriate chart for exploring the relationship between two continuous variables. It makes the distribution visible — showing not just the average but the full spread of outcomes at each discount level. The downward trend becomes visually obvious.

**Encoding:** X = Discount (%). Y = Profit ($). Color = Category (Technology, Furniture, Office Supplies). Reference line on the Y axis at Profit = 0, making loss-making orders immediately visible as dots below the line.

**Filters applied:** Customer Segment and Region filters. Date range slider.

**Design principle applied:** Alpha transparency on dots to handle overlapping points and reveal density. The zero-profit reference line is the most important visual element and is styled in red to draw attention.

**Mistake avoided:** Avoided aggregating this data into a bar chart by discount band only. Aggregation would have hidden the wide variance in outcomes at each discount level and made the relationship appear cleaner than it actually is.

---

## 7. Return Analysis — Highlight Table

**Business question:** Which categories, sub-categories, and segments have the highest return rates? Where should we focus return reduction efforts?

**Chart selected:** Highlight table (also called a heat table) with Category and Segment on the axes and Return Rate as the color-encoded value.

**Why this chart:** A highlight table allows simultaneous comparison across two categorical dimensions without requiring the audience to read individual numbers. High-return intersections immediately stand out as dark cells. It is particularly useful when the business question involves comparing multiple groups at once.

**Encoding:** Rows = Category. Columns = Customer Segment. Cell color = Return Rate (red sequential palette — darker = higher return rate). Cell labels display the return rate percentage.

**Filters applied:** Region and Ship Mode filters.

**Design principle applied:** Red palette was selected deliberately because a high return rate is a negative outcome. Using green or blue would have created an ambiguous signal.

**Mistake avoided:** Avoided using individual bar charts per category/segment combination. That approach would have required the audience to visually scan across many separate charts to identify the worst cells, which is slower and more error-prone than a highlight table.
