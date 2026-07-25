# Saudi Arabia Oil Sales Dashboard — Power BI

An end-to-end Power BI project analyzing 2,000 oil sales transactions
across Saudi Arabia (2022–2024).

![Dashboard Screenshot](exports/dashboard_screenshot.png)

## Project Overview
- **Data source:** Oil sales dataset (Kaggle)
- **Tools:** Power BI Desktop (Power Query, DAX, Data Modeling)
- **Goal:** Practice project for Microsoft PL-300 (Power BI Data Analyst) certification

## Process

### 1. Data Cleaning (Power Query)
- Profiled all columns using Column Quality, Column Distribution, and Column Profile
- Verified no nulls, no duplicate rows, no errors across the full 2,000-row dataset
- Fixed `size` column: stripped unit text ("L"), converted to decimal number
- Removed inconsistent double-spacing in `store_name`
- Verified `year` (2022–2024) and `month` (1–12) ranges for validity
- Correctly left `price_bracket` as text (categorical bucket, not a true number)

### 2. Data Modeling
- Built a star schema with a dedicated Date table using `CALENDAR()`
- Added `Year`, `Month Number`, and `Month Name` calculated columns
- Created a `SalesDate` bridging column on the fact table (from separate
  `year`/`month` fields) to enable a proper date relationship
- Established a one-to-many (*:1) relationship with single-direction
  cross-filtering between the fact table and Date table

### 3. DAX Measures
```dax
Total Sales = SUM(oil_sales_assignment_dataset[value_sales])
Total Volume = SUM(oil_sales_assignment_dataset[volume_sales])
Avg Price = AVERAGE(oil_sales_assignment_dataset[average_price])
Total Transactions = COUNTROWS(oil_sales_assignment_dataset)
```

### 4. Visualizations
- KPI cards for headline metrics (Total Sales, Total Volume, Avg Price, Total Transactions)
- Clustered bar charts: sales by city, sales by manufacturer
- Line chart: sales trend by year with drill-down to quarter/month

## Key Insight
Al Baha leads all cities in total sales value, while overall sales dipped
in 2023 before recovering in 2024.

## Files
- `report/oil_sales_dashboard.pbix` — open in Power BI Desktop to explore interactively
- `exports/oil_sales_dashboard.pdf` — static preview, no Power BI required
- `data/oil_sales_assignment_dataset.csv` — raw source data

## Skills Demonstrated
Data profiling · Data cleaning · Star schema modeling · DAX · Data visualization · Dashboard design
