# Superstore Financial & Operational Analysis Dashboard (Power BI)

![Superstore Financial Analysis Dashboard](Superstore%20BI%20Dashboard%20.png)

## Project Overview
An end-to-end retail financial and operational analytics project built on the **Superstore Dataset** (Kaggle / Vivek Chowdhury), containing **9,994 raw transactional order records across 21 columns** (**9,986 unique records** after deduplication). 

Data ingestion, cleaning, feature engineering, and exploratory data analysis (EDA) were conducted in **Python** (`Visualisation_Project.ipynb`), followed by a **Power BI Desktop** implementation (`Power BI Dashboard.pbix`) designed to identify key revenue drivers, unprofitable products, regional shipping delays, and discounting risks.

## Data Cleaning & Feature Engineering (Python)
Before modeling in Power BI, the raw dataset underwent systematic validation and transformation in Pandas:
- **Deduplication & Product Mapping:** Verified zero missing values across all columns, identified **8 duplicate `(Order ID, Product ID)` pairs (16 rows total)** and removed the **8 duplicate records** (retaining 9,986 unique order-line entries), and standardized 1-to-1 mappings where multiple product names shared a single `Product ID`.
- **Data Type Standardization:** Parsed and standardized `Order Date` and `Ship Date` into proper `datetime` formats.
- **Feature Engineering:** Created temporal columns (`Year`, `Month`, `Day`) along with operational and financial KPIs (`Profit Margin = Profit / Sales` and `Shipping Days = Ship Date - Order Date`).
- **Exploratory Data Analysis:** Analyzed both sales and profit distributions using Matplotlib and Plotly—identifying right-skewed revenue outliers up to **$22,638.48** (vs. an average line-item sale of **$229.86**) and severe profit loss outliers down to **-$6,599.98** (vs. an average line-item profit of **$28.66**).

## Key Business Insights
- **Overall Financial & Operational Performance:** Generated **$2.29M** in total sales and **$285.74K** in net profit (**12.45% overall profit margin**), with an average order value of **$458.10** and **3.96** average shipping days.
- **Technology Leads Revenue & Top-Margin SKUs:** Technology drives the highest sales (**$0.84M**) and dominates the top 10 most profitable products—led by *Copiers* and *Phones* (e.g., *Canon imageCLASS 2200 Advanced Copier* at **$25K** profit), whereas Office Supplies generates high order volume at lower unit values.
- **Discounting Erodes Profitability on Expensive Items:** As shown in the *Impact of Discounts on Profitability* scatter plot, discounts exceeding **20%** consistently push high-value Technology and Furniture products into severe net losses—led by *Cubify CubeX 3D Printer Double Head Print* (**-$9K**), *Lexmark MX611dhe Monochrome Laser Printer* (**-$5K**), and *Cubify CubeX 3D Printer Triple Head Print* (**-$4K**).
- **Regional Performance & Shipping Delays:** **West** (**31.61%** of sales / **$725K**) and **East** (**29.52%**) generate over **61%** of total revenue and maintain faster shipping averages (**3.93** and **3.91** days). Conversely, **Central** captures **21.84%** of sales volume while lagging in profit efficiency and recording the slowest shipping average at **4.06 days** (exceeding the **3.96-day** company benchmark).
- **Peak Q4 Holiday Seasonality:** Sales hit their annual low in **February** before surging sharply during peak demand in **November and December**.

## Strategic Business Recommendations
1. **Audit Order Preparation Times in the Central Region:** Because `Shipping Days` measures the time from when an order is placed to when it leaves the warehouse (`Ship Date - Order Date`), the **Central** region exceeding the **3.96-day** company average (**4.06 days**) points to slower order preparation. Management should check whether this delay is caused by slow packing and handling in Central stores/warehouses, or simply because more customers in that region choose the slower *Standard Class* shipping option—and improve warehouse workflows to match faster regions like **East** (**3.91 days**) and **West** (**3.93 days**).
2. **Optimize Stock & Inventory Allocation for Peak Seasons:** Increase inventory investment and pre-position stock for top-performing, high-margin products (such as *Copiers*, *Phones*, and *Accessories*) ahead of peak seasonal demand in **November and December** to capture maximum Q4 revenue without stockouts.
3. **Rationalize Loss-Making SKUs & Tighten Discount Guardrails:** Reduce capital allocation toward chronically unprofitable items (such as the *Cubify CubeX 3D Printer* models) and use the discount scatter analysis to cap automatic discounts at **20%**—requiring managerial approval for deeper markdowns on high-value Technology and Furniture products.
4. **Benchmark Regional Commercial Performance:** Compare store-level and regional pricing, product mix, and fulfillment workflows in **West** and **East** against **Central** and **South** to close the regional profitability gap.

## Power BI Architecture & Technical Highlights
- **Dynamic Time Granularity:** Implemented a Field Parameter slicer (`Time View`) allowing stakeholders to switch trend granularity dynamically between **Year**, **Month Name**, and **Day**.
- **Custom DAX Measures:** Built dedicated measures for `Total Sales`, `Total Profit`, `Avg Order Value`, `Profit Margin %`, `Avg Shipping Days`, and conditional color formatting (`Category Color`).
- **Unified Color System & Benchmark Reference Line:** Engineered a custom color-coded `Category` button slicer serving as both an interactive cross-filter and shared visual legend across all visuals, paired with an analytics **Average Line** (`3.96`) on the regional shipping chart.

## Repository Contents
- `Power BI Dashboard.pbix` — Complete Power BI Desktop report and data model
- `Superstore BI Dashboard .png` — High-resolution dashboard export
- `Visualisation_Project.ipynb` — Python data cleaning, feature engineering, and EDA notebook
