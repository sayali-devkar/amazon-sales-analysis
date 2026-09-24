# Amazon Sales Analysis

Exploratory data analysis on Amazon.in sales data (128,975 orders, April–June 2022), answering real business questions through data cleaning, aggregation, and visualization.

## Business Questions Answered
1. **Category Performance** — Which product categories generate the highest sales volume and revenue?
2. **Style Trends** — Which product styles are most popular among customers?
3. **Regional Delivery Volume** — Which states/cities receive the most deliveries?
4. **Cancellation Analysis by Region** — Which regions have the highest cancellations, by raw count and by rate?
5. **Revenue Trend Over Time** — How does monthly revenue change, and what's driving the trend?
6. **B2B vs B2C** — How much of total revenue and order volume comes from B2B vs B2C orders?

## Data Cleaning
- Dropped irrelevant/redundant columns (`currency` — single unique value, `SKU`, `ship-postal-code`, `promotion-ids`, `Unnamed: 22`, `fulfilled-by` — fully redundant with `Fulfilment`)
- Kept `Amount` as `NaN` for unfinalized/cancelled orders rather than filling with 0, since `.sum()`/`.mean()` skip NaN automatically but 0 would distort averages
- Filled `ship-city`/`ship-state`/`ship-country` nulls with `'Unknown'` to keep rows usable for non-geo analysis
- Filled `Courier Status` nulls with `'Not Applicable'` instead of `'Unknown'` — ~99.8% of these nulls came from Cancelled orders where no courier was ever involved, so the value is structurally inapplicable, not just missing

## Key Insights
- **Set**, **Kurta**, and **Western Dress** are the top revenue-generating categories; Blouse, Bottom, Dupatta, and Saree contribute minimally
- Demand is concentrated at the top: the best-selling style (JNE3797, 3,692 units) outsold the second-place style by ~1.8x
- Maharashtra leads in raw delivery and cancellation counts, but that's simply because it has the highest order volume — after filtering for states with 100+ orders, states like **Himachal Pradesh, Kerala, and Andaman & Nicobar Islands** actually show the highest cancellation *rates* (~15–18%), pointing to a possible regional logistics issue that raw counts alone would hide
- Revenue declined from ~₹2.86 crore (April) to ~₹2.3 crore (June). Root-cause check showed average order value stayed flat (even rose slightly), while order count dropped ~23% — so the decline is driven by fewer orders, not lower spending per order (a demand-side issue, not pricing)
- B2B makes up only ~0.75% of total orders and revenue. B2B orders are worth ~11.5% more on average (₹678.78 vs ₹608.89) but volume is too small to meaningfully affect total revenue — growing B2B would require more orders, not higher order value

## Tools Used
- Python, Pandas
- Matplotlib, Seaborn
- Jupyter Notebook
