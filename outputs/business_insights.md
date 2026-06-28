# Business Insights — Retail Executive Dashboard

## Calculated Fields Reference

The following calculated fields were created in Tableau to support the analysis:

| Calculated Field | Formula | Purpose |
|---|---|---|
| Profit Margin | `SUM([profit]) / SUM([sales])` | Measures profitability efficiency as a percentage |
| Cost | `SUM([sales]) - SUM([profit])` | Derives cost of goods from available data |
| Average Order Value | `SUM([sales]) / COUNT([order_id])` | Tracks average revenue per transaction |
| Return Rate | `SUM([return_flag]) / COUNT([order_id])` | Identifies proportion of returned orders |
| Shipping Delay Bucket | `IF [delivery_days] <= 1 THEN "Express (0-1 days)" ELSEIF [delivery_days] <= 3 THEN "Fast (2-3 days)" ELSEIF [delivery_days] <= 5 THEN "Standard (4-5 days)" ELSE "Slow (6+ days)" END` | Groups delivery performance into meaningful tiers |
| Discount Band | `IF [discount] = 0 THEN "No Discount" ELSEIF [discount] <= 0.10 THEN "Low (1-10%)" ELSEIF [discount] <= 0.20 THEN "Medium (11-20%)" ELSE "High (21-35%)" END` | Segments discount levels for impact analysis |
| Order Year | `YEAR([order_date])` | Enables year-over-year comparison |

---

## Insight 1 — Sales Trend

**Observation:** Monthly sales ranged between $6.3M and $10.9M over the two-year period (2024–2025). Sales dipped noticeably in mid-2024 (July–August), recovered strongly in September 2024, and showed a steadier pattern through 2025 with consistent performance above $8M from July onward.

**Evidence:** August 2024 recorded the lowest monthly sales at approximately $6.3M. July–August 2025 were the two highest months, reaching $10.7M and $10.9M respectively.

**Business Interpretation:** The mid-2024 dip likely reflects a seasonal slowdown or reduced promotional activity. The stronger second half of 2025 suggests the business gained momentum, possibly driven by improved marketing efforts or new product lines.

**Recommended Action:** Investigate what changed between mid-2024 and mid-2025 to explain the stronger 2025 performance. If promotional activity drove the improvement, consider replicating those campaigns earlier in the year to smooth the seasonal dip.

---

## Insight 2 — Regional Performance

**Observation:** The South region leads both in sales ($64.7M) and profit ($10.0M), while the West lags behind with the lowest profit ($7.4M) despite generating sales comparable to the East ($48.9M).

**Evidence:** South: $64.7M sales, $10.0M profit (15.4% margin). West: $48.9M sales, $7.4M profit (15.1% margin). East: $48.9M sales, $7.6M profit (15.6% margin). North: $54.6M sales, $8.3M profit (15.2% margin).

**Business Interpretation:** All regions maintain similar profit margins (~15%), so the South's higher profit comes from higher volume rather than a pricing advantage. The West may have growth headroom if sales strategies are strengthened.

**Recommended Action:** Study what is driving South's higher order volume — territory coverage, campaign activity, or demographic factors — and apply those learnings to the West region.

---

## Insight 3 — Category Profitability

**Observation:** Technology dominates sales ($153.9M, 70% of total) and profit ($28.0M, 84% of total) with the highest margin at 18.2%. Furniture generates significant sales ($51.6M) but the lowest margin at 6.9%. Office Supplies contributes a healthy 14.9% margin but on a much smaller sales base ($11.5M).

**Evidence:** Technology profit margin: 18.2%. Furniture: 6.9%. Office Supplies: 14.9%.

**Business Interpretation:** The business is heavily dependent on Technology, which creates concentration risk. Furniture's low margin may reflect discounting practices or higher cost structures. Office Supplies is the most balanced category in terms of margin efficiency.

**Recommended Action:** Review Furniture discounting policies and cost structures to improve its margin. Explore whether Office Supplies volume can be grown — it has better margins than Furniture and does not require the same capital intensity as Technology.

---

## Insight 4 — Sub-Category Profitability

**Observation:** Copiers, Accessories, and Phones are the top three sub-categories by profit, each exceeding $7M. All three sit within Technology. Tables and Bookcases, both in Furniture, show the lowest profit margins at 5.7% and 5.7% respectively.

**Evidence:** Copiers: $7.3M profit, 18.0% margin. Accessories: $7.2M profit, 18.3%. Phones: $7.1M profit, 18.5%. Tables: $731K profit, 5.7% margin. Bookcases: $712K profit, 5.7%.

**Business Interpretation:** The Technology sub-categories are the profit engine of the business. Furniture sub-categories (Tables, Bookcases, Chairs, Furnishings) are dragging the category average down with thin margins. These could be running at near-breakeven or even at a loss when factoring in returns and logistics costs.

**Recommended Action:** Conduct a product-level margin review on Tables and Bookcases. Consider whether these products are strategically important for customer acquisition or if they can be repriced or discontinued.

---

## Insight 5 — Customer Segment Behavior

**Observation:** All three segments — Consumer, Corporate, and Home Office — perform similarly in both sales and profit. Home Office leads slightly at $74.5M sales and $11.6M profit (15.5% margin), but the differences across segments are modest.

**Evidence:** Home Office margin: 15.5%. Corporate: 15.2%. Consumer: 15.3%.

**Business Interpretation:** There is no standout segment by profitability. This suggests pricing and product mix are consistent across segments. However, the even split may mask segment-specific behaviors in categories — for example, Corporate buyers may concentrate in Technology while Consumers purchase more Furniture.

**Recommended Action:** Build a cross-tab of segment by category to identify where each segment over-indexes. Use those patterns to design targeted promotions — for example, technology bundles for Corporate customers or home office setup offers for Home Office customers.

---

## Insight 6 — Discount Impact on Profit

**Observation:** Average profit per order declines sharply as discounts increase. Orders with no or minimal discount (0–5%) generate average profit of $11,182. Orders at the highest discount tier (25–35%) generate only $2,729 on average — a 76% drop.

**Evidence:** Discount 0–5%: avg profit $11,182. Discount 5–15%: $7,440. Discount 15–25%: $4,749. Discount 25–35%: $2,729.

**Business Interpretation:** Heavy discounting significantly erodes profit margins without a clear offsetting volume benefit. The 25–35% discount band collectively contributes only $1.6M in total profit compared to $5.6M in the 0–5% band, despite involving a substantial number of orders.

**Recommended Action:** Set a maximum discount threshold of 20% without management approval. Review all accounts or campaigns where discounts routinely exceed 20% and assess whether the incremental volume justifies the margin sacrifice.

---

## Insight 7 — Shipping Performance

**Observation:** Standard Class is the dominant shipping mode and averages 4.7 delivery days. Same Day shipping is at 0.4 days on average, while Second Class averages 2.7 days. Orders taking 6 or more days represent 666 transactions (roughly 16% of all orders).

**Evidence:** Standard Class: 4.71 avg delivery days. First Class: 1.77 days. Second Class: 2.68 days. Same Day: 0.40 days. Orders with 6+ delivery days: 666.

**Business Interpretation:** Most customers opt for Standard Class, which has the longest delivery time. The 16% of orders that take 6 or more days may be linked to lower customer ratings and higher return rates, though this requires further validation.

**Recommended Action:** Cross-reference the Slow (6+ days) delivery bucket with customer ratings and return rates to confirm the link. If confirmed, consider offering a service guarantee or proactive communication for Standard Class shipments expected to exceed 5 days.

---

## Insight 8 — Return Analysis and Business Risk

**Observation:** Furniture has the highest return rate at 7.7%, more than double the rate for Technology (3.0%) and nearly double that of Office Supplies (3.7%). The total return count across all orders is 191, representing a 4.6% overall return rate.

**Evidence:** Furniture returns: 88 orders, 7.7% rate. Technology: 42 orders, 3.0% rate. Office Supplies: 61 orders, 3.7% rate. Total returns: 191.

**Business Interpretation:** Furniture's high return rate is a material risk. Given Furniture's already thin 6.9% margin, returns can quickly push individual transactions into negative margin territory once reverse logistics costs are accounted for. High return rates may also reflect product quality, mismatched customer expectations, or damage in transit.

**Recommended Action:** Investigate the root cause of Furniture returns — whether driven by specific sub-categories (Tables vs. Chairs), specific ship modes, or specific regions. Improve product descriptions and imagery to reduce expectation mismatches, and review packaging standards for large Furniture items to reduce transit damage.
