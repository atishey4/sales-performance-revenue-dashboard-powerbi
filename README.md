# Sales Performance & Revenue Growth Dashboard

## Objective
To create an interactive Power BI dashboard that tracks sales trends, revenue growth, and product/category performance to help businesses make data-driven decisions.

---

## Tools Used
- **Power BI Desktop** – Dashboard design, data modeling, and report building
- **Power Query Editor** – Data cleaning and transformation
- **DAX (Data Analysis Expressions)** – KPI and measure creation
- **Microsoft Excel / CSV** – Source dataset

---

## Dataset Description

A realistic sales dataset containing **500+ rows** with the following columns:

| Column | Description |
|---|---|
| Date | Transaction date |
| Month | Month name extracted from date |
| Quarter | Q1 / Q2 / Q3 / Q4 |
| Year | Fiscal year |
| Region | East, West, North, South |
| State / City | Geographic location of the sale |
| Sales Executive Name | Name of the sales representative |
| Product Category | Apparel, Electronics, FMCG, Furniture |
| Product Name | Individual product name |
| Units Sold | Number of units sold per transaction |
| Selling Price | Price per unit |
| Revenue | Units Sold × Selling Price |
| Cost | Total cost of goods for the transaction |
| Profit | Revenue minus Cost |
| Profit Margin % | Profit / Revenue × 100 |
| Customer Type | New / Existing |
| Sales Channel | Online / Offline |
| Target Sales | Planned sales target for the period |
| Actual Sales | Revenue actually achieved |
| Achievement % | Actual Sales / Target Sales × 100 |
| Growth % | Period-over-period revenue growth percentage |

---

## Power Query Steps

1. **Remove null and blank values** – Cleaned rows with missing Date, Revenue, or Region to ensure accurate KPI calculations
2. **Change data types** – Set Revenue, Cost, Profit as Currency; Units Sold as Whole Number; Date as Date type
3. **Create Month, Quarter, Year columns** – Extracted from the Date column for time-based trend analysis and filtering
4. **Handle duplicates** – Removed duplicate transaction records to maintain data integrity
5. **Rename columns** – Standardized column names for clarity (e.g., "Exec_Name" → "Sales Executive Name")
6. **Format currency and percentage fields** – Applied proper number formatting for financial and percentage columns
7. **Create calculated columns** – Added Profit (Revenue − Cost) and Achievement % columns directly in Power Query where needed

---

## DAX Measures

```dax
Total Revenue = SUM(SalesData[Revenue])

Total Cost = SUM(SalesData[Cost])

Total Profit = SUM(SalesData[Profit])

Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0) * 100

Total Units Sold = SUM(SalesData[Units Sold])

Target Sales = SUM(SalesData[Target Sales])

Actual Sales = SUM(SalesData[Actual Sales])

Achievement % = DIVIDE([Actual Sales], [Target Sales], 0) * 100

Growth % =
    DIVIDE(
        [Total Revenue] - CALCULATE([Total Revenue], DATEADD(DateTable[Date], -1, YEAR)),
        CALCULATE([Total Revenue], DATEADD(DateTable[Date], -1, YEAR))
    ) * 100

Region-wise Revenue = CALCULATE([Total Revenue], ALLEXCEPT(SalesData, SalesData[Region]))

Category-wise Profit = CALCULATE([Total Profit], ALLEXCEPT(SalesData, SalesData[Product Category]))
```

---

## Dashboard Features

- **KPI Cards** – Total Revenue, Total Profit, Total Units Sold, Achievement %, Profit Margin % displayed at the top
- **Clustered Column Chart** – Total Revenue and Total Profit by Region for regional performance comparison
- **Line Chart** – Total Revenue and Total Profit by Month Name showing monthly growth trends
- **Horizontal Bar Chart** – Total Revenue and Total Profit by Product Category
- **Donut Chart** – Total Revenue by Sales Channel (Online vs Offline distribution)
- **Matrix Table** – Region, Sales Executive, Total Revenue, Total Profit, Achievement %, Total Units Sold, and Customer Type for detailed drill-down
- **Slicers & Filters** – Region, Product Category, Sales Channel, Sales Executive

---

## Key Insights

- **South region** leads in total revenue, followed closely by North, West, and East
- **Electronics** is the highest revenue-generating product category, contributing the majority of total profit
- Overall **Achievement % stands at 106.6%**, indicating the business has exceeded its sales targets
- **Online channel accounts for 78.7%** of total revenue, significantly outperforming the Offline channel
- Revenue shows a consistent **upward trend from January through December**, confirming strong business growth across the year
- **Total Revenue of ₹39.17M** and **Total Profit of ₹13.35M** reflect a healthy **Profit Margin of 34.1%**
- Sales executives like **Ananya Roy and Arjun Singh** are among the top contributors by revenue across their respective regions
- **New customers** across regions represent a significant volume of units sold, indicating successful acquisition efforts

---

## Screenshots

### Dashboard Overview
![Sales Performance Dashboard](screenshots/dashboard_overview.png)

> *Add your Power BI dashboard screenshot here. Export from Power BI → File → Export → Export to PDF or take a screenshot and save in the `screenshots/` folder.*

---

## Conclusion

This Sales Performance & Revenue Growth Dashboard gives sales managers, business analysts, and leadership teams a comprehensive, interactive view of business performance. By consolidating revenue, profit, target achievement, channel performance, and regional breakdowns into a single Power BI report, it enables faster and more confident decision-making. The dashboard is suitable for use by Sales Analysts, Revenue Managers, Business Analysts, and senior leadership in retail, e-commerce, FMCG, and any sales-driven organization looking to optimize strategy and accelerate growth.
