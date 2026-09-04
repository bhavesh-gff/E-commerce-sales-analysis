# E-commerce Sales Analysis Dashboard

An e-commerce analytics project using **Google BigQuery** and **SQL** to analyze revenue, product performance, conversion, traffic channels, and funnel behavior for the **Google Merchandise Store** dataset.

---

## 1. Project Overview

This project analyzes e-commerce session-level data to understand how customers move from landing on the website to completing a purchase. The analysis covers revenue performance by city, top-selling products, overall and channel-wise conversion rates, and cart abandonment — with the goal of identifying concrete opportunities to improve sales performance.

The project also includes a **data quality investigation**, since the raw dataset contained inconsistencies that had to be identified and handled before the analysis could be trusted.

---

## 2. Business Problem

E-commerce businesses generate large volumes of session and transaction data, but this data is only valuable if it is cleaned, structured, and analyzed correctly. The business needed answers to:

* Where is revenue actually coming from (geographically)?
* Which products are driving the most sales volume?
* How efficiently are website sessions converting into transactions?
* Which marketing/traffic channels are worth investing more in?
* How much revenue is being lost to cart abandonment?

---

## 3. Business Questions

1. Which cities generate the highest revenue?
2. What are the top-selling products by units sold?
3. What is the overall session-to-transaction conversion rate?
4. Which traffic channel converts best?
5. How many sessions add products to cart but never complete a transaction (funnel drop-off)?

---

## 4. Dataset

* **Source:** Google Merchandise Store (Google Analytics sample dataset)
* **Platform:** Google BigQuery (Public Dataset)
* **Table:** `data-to-insights.e-commerce.all_sessions`
* **Granularity:** Session-level e-commerce data (visits, products, transactions, traffic source)

---

## 5. Tools and Technologies

|Tool|Purpose|
|-|-|
|Google BigQuery|Data storage and SQL querying|
|SQL (Standard SQL)|Data cleaning, transformation, analysis|
|Chart.js|Interactive dashboard charts|
|GitHub|Project documentation and portfolio|

---

## 6. Data Understanding

Before analysis, the dataset was explored to understand:

* Table schema and column data types
* Grain of the data (one row = one product interaction within a session)
* Key fields: `fullVisitorId`, `visitId`, `productSKU`, `v2ProductName`, `productRevenue`, `channelGrouping`, `city`, `transactionId`, `eCommerceActionType`

This step ensured that downstream aggregations (e.g., revenue, units sold) were calculated at the correct level, avoiding double-counting.

---

## 7. Data Quality and Cleaning

During exploration, a **data quality issue** was discovered: certain fields contained inconsistent, missing, or placeholder values (e.g., `(not set)` city values, null product revenue on non-purchase rows, and duplicate session-product rows).

**Why this matters:** If these issues are ignored, revenue and conversion metrics get inflated or distorted, leading to incorrect business conclusions.

**Steps taken:**

* Identified rows with `(not set)` / null / placeholder values in key dimensions (city, channel, product).
* Filtered out or explicitly handled null `product Revenue` values (nulls represent non-purchase product views, not zero revenue).
* Checked for duplicate rows at the session-product grain before aggregating.
* Validated revenue totals against transaction counts to catch anomalies.

The cleaning approach should be documented in the SQL query used to build the dashboard dataset so that the metrics remain transparent and reproducible.

---

## 8. SQL Analysis

The analysis is summarized in the dashboard and is based on modular SQL queries for each business question. The original query files are not included in this workspace.

|Analysis area|Dashboard output|
|-|-|
|Revenue|Revenue by city|
|Product performance|Top product by units sold|
|Conversion|Overall and channel conversion rates|
|Funnel|Sessions, add-to-cart sessions, and transactions|

---

## 9. Key Findings

* **Highest revenue city:** Mountain View, generating approximately **$672,731.80**
* **Top product by units sold:** Google Sunglasses, with **58,149 units**
* **Overall conversion rate:** **4.57%** of sessions resulted in a transaction
* **Best-performing traffic channel:** Referral, with a **12.20%** conversion rate
* **Cart abandonment opportunity:** **143,587 sessions** added a product to cart but did not complete a transaction

---

## 10. Business Recommendations

1. **Double down on high-revenue cities** like Mountain View with geo-targeted promotions and localized ad spend.
2. **Feature top-performing products** (e.g., Google Sunglasses) more prominently in homepage banners and email campaigns.
3. **Invest more in Referral traffic**, since it converts far above the overall average (12.20% vs 4.57%) — likely a high-intent channel.
4. **Address cart abandonment** (143,587 sessions) through retargeting emails, exit-intent discounts, or simplifying the checkout flow.
5. **Fix upstream data quality issues** (e.g., `(not set)` city/channel values) at the tracking/tagging level to improve future analysis accuracy.

---

## 11. Dashboard

The local dashboard visualizes these findings with responsive HTML, CSS, and Chart.js charts:

* KPI summary for the leading city, product, conversion rate, channel, and cart drop-off
* Revenue by city
* Conversion rate by traffic channel
* E-commerce funnel: sessions, add to cart, and transactions

Open [e-commerce_sales_dashboard.html](ecommerce_sales_dashboard.html) in a browser to view the dashboard.

---

## 12. Data Availability

The source SQL files, screenshots, and report are not included in this workspace. The dashboard is a static presentation of the findings listed above; it does not query BigQuery at runtime.

---

## 13. Project Structure

```text
e-commerce-sales-analysis/
├── README.md
└── e-commerce_sales_dashboard.html
```

---

## 14. How to Reproduce

1. Get access to Google BigQuery (a free-tier or sandbox account is sufficient).
2. Open the public dataset: `data-to-insights.e-commerce.all_sessions`.
3. Recreate the cleaning and aggregation queries described above.
4. Compare the resulting metrics with the dashboard findings.
5. Open `e-commerce_sales_dashboard.html` locally to view the presentation layer.

---

## 15. Skills Demonstrated

* SQL (aggregation, filtering, joins, window functions, CTEs)
* Data cleaning and data quality auditing
* Business-question-driven analysis
* KPI definition and metric calculation (conversion rate, revenue, funnel analysis)
* Dashboard with HTML, CSS, and Chart.js
* Technical documentation and project structuring for a portfolio

---

## Author

Add your name, LinkedIn profile, and portfolio link here.

