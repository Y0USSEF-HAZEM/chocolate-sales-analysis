# Chocolate Sales Performance Analysis (2023)

## Project Overview

This project evaluates the 2023 sales performance for a chocolate production company. The primary goal is to provide actionable insights into sales trends, regional distribution, and sales team efficiency to guide strategic decisions.

## Business Requirements

- **Transaction Classification:** Categorize sales transactions into high vs. low performance relative to the overall average sales value.
- **Monthly Trend Analysis:** Identify monthly sales patterns, highlighting peak and low-performing periods.
- **Regional Breakdown:** Analyze sales performance across different geographic regions to assess market concentration.

## Data Cleaning & Transformation (Power Query)

- **Exploratory Analysis:** Reviewed dataset metadata and column definitions to align transformation steps with business requirements.
- **Deduplication & Data Types:** Identified and removed duplicate records based on `Order-ID` and ensured appropriate data types (Dates, Integers, Text, Currency).
- **Text Standardization:** Applied `Trim` and `Capitalize Each Word` on `Sales Person` and `Geography` columns, resolving spelling variations across regions.
- **Calculated Attributes:** Created `Month`, `Quarter`, and `Year` attributes, along with a row-level `Total` sales column (`Units` \* `Amount`).

## Data Modeling & DAX Implementation

- **Transaction Classification:** Built a calculated column (`Sale Performance`) to classify orders into `High Value` vs. `Low Value` based on average transaction thresholds.
- **Core KPI Measures:** Created explicit DAX measures using measure branching to optimize calculation performance:
  - `Total Sales` = `SUM('Raw-data'[Total])`
  - `Units Sold` = `SUM('Raw-data'[Units])`
  - `Number of Orders` = `COUNTA('Raw-data'[Order-ID])`
  - `Average Order Value (AOV)` = `[Total Sales] / [Number of Orders]`

## Dashboard Architecture & Layout

The dashboard is structured into a logical 3-tier layout for seamless data exploration:

- **Header Tier (Executive KPIs & Control):**
  - Core KPI Cards: `Total Sales`, `Units Sold`, `Avg Order Value`, and `Number of Orders`.
  - Interactive Slicer: `Sales Tier` (`High Value` vs. `Low Value`) to filter the entire report dynamically.

- **Middle Tier (Macro Trends & Geography):**
  - `Sales Trend` (Line Chart): Displays monthly sales behavior across 2023.
  - `Region Sales` (Donut Chart): Highlights regional sales share across governorates.

- **Bottom Tier (Micro Performance & Detailed Metrics):**
  - `Top Sellers` (Horizontal Bar Chart): Ranks performance across the sales team.
  - `Product Details` (Table Visual): Provides granular unit sales and sales metrics for all catalog items.

## Dashboard Preview

![Chocolate Sales Dashboard](Dashboard_Screen.png?v=2)

## Key Insights & Actionable Recommendations

### 1. High Sales Concentration

- **Key Finding:** 76.2% of total sales (EGP 155.2M) is driven by just 33.6% of orders (106 High-Value transactions). The remaining 66.4% of order volume generates only 23.8% of sales.
- **Data Context:** November's low figure (EGP 9M) is due to data truncation on Nov 11th, not a demand drop.
- **Recommended Actions:**
  - Implement dedicated retention strategies for top B2B buyers to safeguard core sales.
  - Set a Minimum Order Quantity or offer product bundles to optimize handling costs for smaller transactions.

### 2. Geographic Market Concentration

- **Key Finding:** Sharm El Sheikh and Al Sharqia drive ~45% of total sales, while Al Giza lags at 11%.
- **Recommended Actions:**
  - Prioritize inventory allocation and targeted campaigns in top regional hubs.
  - Evaluate distribution bottlenecks in lower-performing regions like Al Giza.

### 3. Product Pricing & Anomaly Analysis

- **Key Finding:** Premium items drive core revenue, with most top-performing products priced above EGP 70k (e.g., `70% Dark Bites`, `Caramel Stuffed Bars`). However, `White Choc` presents a clear anomaly: priced similarly (~80k) but ranks in the bottom 5.
- **Recommended Actions:**
  - Focus marketing and supply on top-performing premium SKUs (`70% Dark Bites`, `Caramel Stuffed Bars`).
  - Investigate `White Choc` to identify whether low performance stems from flavor preference or stock availability.
