# Multi-Channel Marketing Campaign Performance Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)

---

## Project Overview

An end-to-end marketing campaign analytics solution analyzing 2,216 customers across channel performance, customer segmentation, and product revenue. Built using Python and SQL for data preparation and feature engineering, with a 3-page interactive Power BI dashboard for stakeholder reporting.

**Domain:** Financial Services | Marketing Analytics  
**Tools:** Python, SQL, Power BI, DAX, Pandas  
**Dataset:** Maven Marketing Campaign Dataset (2,216 records, 29 variables)

---

## Business Problem

A marketing team needed to understand which customer segments, channels, and products were driving the most revenue and conversions — and where campaign budget was being wasted.

---

## Key Findings

### Channel Performance
- Store is the dominant channel at **38.98%** of total purchases
- Web is 2nd at **27.45%** — strong digital presence
- Catalogue customers show **3x higher average spend** than Deals channel
- Deals channel is the least efficient at **15.61%** purchase share

### Product Revenue
- Wines alone contributes **50.26%** of total revenue
- Top 2 products (Wines + Meat) account for **77.77%** of all revenue
- Fruits and Sweets are significantly underperforming at 4.34% and 4.45%

### Customer Segmentation
- PhD customers convert at **21%** vs **3.7%** for Basic education — 5.7x difference
- High income segment converts at **30.77%** — highest of all income groups
- Upper-Mid income drives highest average spend at **$1,391 per customer**
- Under-30 and 60+ age groups spend significantly more than middle-aged segments

### Campaign Recommendations
- Prioritize Store and Catalogue channels for high-value PhD and Upper-Mid segments
- Reallocate Deals budget to Web and Catalogue for better ROI
- Focus campaign outreach on High income and PhD segments for maximum conversion
- Promote Wines and Meat products as primary revenue drivers

---

## Dashboard Pages

### Page 1 — Campaign Overview
- 5 KPI cards: Total Customers, Total Conversions, Avg Income, Avg Spend, Conversion Rate
- Purchases by Channel (bar chart)
- Revenue by Product Category (donut chart)
- Conversion Rate by Education (column chart)
- Avg Spend by Income Group (column chart)
- Dynamic slicers: Income Group, Education

### Page 2 — Customer Segments
- 3 KPI cards: PhD Conversion Rate, High Income Conversion, Highest Avg Spend Segment
- Avg Spend by Age Group (bar chart)
- Conversion Rate by Age Group (column chart)
- Conversion Rate by Income Group (column chart)
- Avg Spend by Education Level (bar chart)
- Dynamic slicer: Marital Status

### Page 3 — Channel & Spend Analysis
- Store vs Web vs Catalogue Purchases by Education (clustered column chart)
- Channel Purchase Volume (bar chart)
- Avg Purchases per Customer by Channel (bar chart)
- Channel Share % (donut chart)

---

## SQL Analysis

5 SQL queries performed using SQLite:

```sql
-- Query 1: Overall Campaign Metrics
SELECT COUNT(*) AS total_customers,
       ROUND(AVG(Income), 2) AS avg_income,
       ROUND(AVG(TotalSpend), 2) AS avg_spend,
       SUM(Response) AS total_conversions,
       ROUND(AVG(Response) * 100, 2) AS conversion_rate
FROM marketing

-- Query 2: Channel Performance Analysis
SELECT 'Store' AS channel,
       SUM(NumStorePurchases) AS total_purchases,
       ROUND(SUM(NumStorePurchases) * 100.0 / SUM(TotalPurchases), 2) AS channel_share_pct
FROM marketing
UNION ALL
SELECT 'Web', SUM(NumWebPurchases),
       ROUND(SUM(NumWebPurchases) * 100.0 / SUM(TotalPurchases), 2)
FROM marketing
-- ... (see notebook for full queries)

-- Query 3: Product Revenue Analysis
-- Query 4: Customer Segment by Education
-- Query 5: Income Group vs Spend & Conversion
```

---

## Feature Engineering

New columns created in Python:

| Feature | Description |
|---|---|
| Age | 2024 - Year_Birth |
| TotalSpend | Sum of all product spend columns |
| TotalPurchases | Sum of all channel purchase columns |
| TotalCampaignsAccepted | Sum of all 5 campaign responses |
| AgeGroup | Binned age into 5 groups |
| IncomeGroup | Binned income into 5 groups |

---

## Project Structure

```
marketing-campaign-dashboard/
│
├── data/
│   └── marketing_campaign.xlsx          # Raw dataset
│
├── powerbi_exports/
│   ├── marketing_clean.csv              # Cleaned dataset
│   ├── channel_performance.csv          # Channel analysis
│   ├── product_revenue.csv              # Product revenue
│   ├── education_segments.csv           # Education segments
│   ├── income_groups.csv                # Income groups
│   └── age_analysis.csv                 # Age analysis
│
├── Marketing_Campaign_Dashboard.ipynb   # Python & SQL analysis
├── Marketing_Campaign_Dashboard.pbix    # Power BI dashboard file
└── README.md
```

---

## How to Use

### View the Dashboard
1. Download `Marketing_Campaign_Dashboard.pbix`
2. Open in Power BI Desktop (free download)
3. Explore all 3 pages with dynamic slicers

### Run the Analysis
```bash
pip install pandas numpy matplotlib seaborn openpyxl
jupyter notebook Marketing_Campaign_Dashboard.ipynb
```

---

## Dataset

**Maven Marketing Campaign Dataset**  
- 2,216 customer records  
- 29 variables covering demographics, spend, channel purchases, and campaign responses  
- Source: Kaggle

---

## Tools & Technologies

| Tool | Usage |
|---|---|
| Python (Pandas) | Data cleaning, feature engineering |
| SQL (SQLite) | Data analysis, aggregation queries |
| Power BI | 3-page interactive dashboard |
| DAX | Conversion rate measure |
| Matplotlib | Exploratory visualizations |
