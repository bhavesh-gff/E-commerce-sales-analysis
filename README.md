# Ecommerce Sales Analysis using Google Big Query \& SQL

An end-to-end ecommerce analytics project that uses **Google Big Query** and **SQL** to analyze revenue, product performance, customer conversion, traffic channels, and funnel behavior for the **Google Merchandise Store** dataset.

\---

## 1\. Project Overview

This project analyzes ecommerce session-level data to understand how customers move from landing on the website to completing a purchase. The analysis covers revenue performance by city, top-selling products, overall and channel-wise conversion rates, and cart abandonment — with the goal of identifying concrete opportunities to improve sales performance.

The project also includes a **data quality investigation**, since the raw dataset contained inconsistencies that had to be identified and handled before the analysis could be trusted.

\---

## 2\. Business Problem

Ecommerce businesses generate large volumes of session and transaction data, but this data is only valuable if it is cleaned, structured, and analyzed correctly. The business needed answers to:

* Where is revenue actually coming from (geographically)?
* Which products are driving the most sales volume?
* How efficiently are website sessions converting into transactions?
* Which marketing/traffic channels are worth investing more in?
* How much revenue is being lost to cart abandonment?

\---

## 3\. Business Questions

1. Which cities generate the highest revenue?
2. What are the top-selling products by units sold?
3. What is the overall session-to-transaction conversion rate?
4. Which traffic channel converts best?
5. How many sessions add products to cart but never complete a transaction (funnel drop-off)?

\---

## 4\. Dataset

* **Source:** Google Merchandise Store (Google Analytics sample dataset)
* **Platform:** Google BigQuery (Public Dataset)
* **Table:** `data-to-insights.ecommerce.all\_sessions`
* **Granularity:** Session-level ecommerce data (visits, products, transactions, traffic source)

\---

## 5\. Tools \& Technologies

|Tool|Purpose|
|-|-|
|Google Big Query|Data storage \& SQL querying|
|SQL (Standard SQL)|Data cleaning, transformation, analysis|
|Looker Studio|Dashboard \& visualization|
|GitHub|Project documentation \& portfolio|

\---

## 6\. Data Understanding

Before analysis, the dataset was explored to understand:

* Table schema and column data types
* Grain of the data (one row = one product interaction within a session)
* Key fields: `full Visitor Id`, `visit Id`, `product SKU`, `v2ProductName`, `product Revenue`, `channel Grouping`, `city`, `transaction Id`, `eCommerce Action\_type`

This step ensured that downstream aggregations (e.g., revenue, units sold) were calculated at the correct level, avoiding double-counting.

\---

## 7\. Data Quality \& Cleaning

During exploration (Q2), a **data quality issue** was discovered: certain fields contained inconsistent, missing, or placeholder values (e.g., `(not set)` city values, null product revenue on non-purchase rows, and duplicate session-product rows).

**Why this matters:** If these issues are ignored, revenue and conversion metrics get inflated or distorted, leading to incorrect business conclusions.

**Steps taken:**

* Identified rows with `(not set)` / null / placeholder values in key dimensions (city, channel, product).
* Filtered out or explicitly handled null `product Revenue` values (nulls represent non-purchase product views, not zero revenue).
* Checked for duplicate rows at the session-product grain before aggregating.
* Validated revenue totals against transaction counts to catch anomalies.

This step is documented separately in [`sql/02\_data\_quality.sql`](sql/02_data_quality.sql) to make the cleaning logic transparent and reproducible.

\---

## 8\. SQL Analysis

All analysis was performed using modular SQL scripts, each focused on one business question:

|Script|Purpose|
|-|-|
|`01\_schema.sql`|Table structure \& exploration|
|`02\_data\_quality.sql`|Identifying and handling data quality issues|
|`03\_revenue\_analysis.sql`|Revenue by city|
|`04\_product\_analysis.sql`|Top products by units sold|
|`05\_conversion\_analysis.sql`|Overall conversion rate|
|`06\_traffic\_analysis.sql`|Conversion rate by traffic channel|
|`07\_funnel\_analysis.sql`|Add-to-cart vs completed transaction (funnel drop-off)|

\---

## 9\. Key Findings

* **Highest revenue city:** Mountain View, generating approximately **$672,731.80**
* **Top product by units sold:** Google Sunglasses, with **58,149 units**
* **Overall conversion rate:** **4.57%** of sessions resulted in a transaction
* **Best-performing traffic channel:** Referral, with a **12.20%** conversion rate
* **Cart abandonment opportunity:** **143,587 sessions** added a product to cart but did not complete a transaction

\---

## 10\. Business Recommendations

1. **Double down on high-revenue cities** like Mountain View with geo-targeted promotions and localized ad spend.
2. **Feature top-performing products** (e.g., Google Sunglasses) more prominently in homepage banners and email campaigns.
3. **Invest more in Referral traffic**, since it converts far above the overall average (12.20% vs 4.57%) — likely a high-intent channel.
4. **Address cart abandonment** (143,587 sessions) through retargeting emails, exit-intent discounts, or simplifying the checkout flow.
5. **Fix upstream data quality issues** (e.g., `(not set)` city/channel values) at the tracking/tagging level to improve future analysis accuracy.

\---

## 11\. Dashboard

An interactive Looker Studio dashboard was built to visualize these insights, including:

* Revenue, Sessions, Transactions, and Conversion Rate KPIs
* Revenue by City
* Top 10 Products by Units Sold
* Conversion Rate by Traffic Channel
* Ecommerce Funnel (Sessions → Add to Cart → Transactions)

🔗 Dashboard link: see [`dashboard/dashboard\_link.txt`](dashboard/dashboard_link.txt)

\---

## 12\. Screenshots

|Screenshot|Description|
|-|-|
|`01\_schema.png`|Table schema exploration|
|`02\_data\_quality.png`|Data quality checks|
|`03\_revenue\_analysis.png`|Revenue by city results|
|`04\_product\_analysis.png`|Top products results|
|`05\_conversion.png`|Conversion rate query results|
|`06\_traffic\_analysis.png`|Traffic channel conversion results|
|`07\_funnel\_analysis.png`|Funnel/cart abandonment results|

\---

## 13\. Project Structure

```text
ecommerce-sales-analysis/
│
├── README.md
│
├── sql/
│   ├── 01\_schema.sql
│   ├── 02\_data\_quality.sql
│   ├── 03\_revenue\_analysis.sql
│   ├── 04\_product\_analysis.sql
│   ├── 05\_conversion\_analysis.sql
│   ├── 06\_traffic\_analysis.sql
│   └── 07\_funnel\_analysis.sql
│
├── screenshots/
│   ├── 01\_schema.png
│   ├── 02\_data\_quality.png
│   ├── 03\_revenue\_analysis.png
│   ├── 04\_product\_analysis.png
│   ├── 05\_conversion.png
│   ├── 06\_traffic\_analysis.png
│   └── 07\_funnel\_analysis.png
│
├── dashboard/
│   └── dashboard\_link.txt
│
└── report/
    └── Ecommerce\_Sales\_Analysis\_Report.pdf
```

\---

## 14\. How to Reproduce

1. Get access to Google Big Query (a free-tier / sandbox account is sufficient).
2. Open the public dataset: `data-to-insights.ecommerce.all\_sessions`.
3. Run the SQL scripts in the `sql/` folder **in numbered order** (01 → 07):

   * Start with `01\_schema.sql` to understand the table structure.
   * Run `02\_data\_quality.sql` to see the cleaning/validation logic.
   * Run `03` through `07` for the actual business analysis.
4. Compare your output with the corresponding screenshot in `screenshots/`.
5. (Optional) Connect the cleaned queries to Looker Studio to rebuild the dashboard.

\---

## 15\. Skills Demonstrated

* SQL (aggregation, filtering, joins, window functions, CTEs)
* Data cleaning \& data quality auditing
* Business-question-driven analysis
* KPI definition and metric calculation (conversion rate, revenue, funnel analysis)
* Dashboarding with Looker Studio
* Technical documentation \& project structuring for a portfolio

\---

## Author

*Add your name, LinkedIn profile link, and portfolio link here.*

