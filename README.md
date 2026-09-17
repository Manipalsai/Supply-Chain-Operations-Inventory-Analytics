# Supply Chain Operations & Inventory Analytics

[![Microsoft Excel](https://img.shields.io/badge/Microsoft_Excel-2024-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)](https://www.microsoft.com/en-us/microsoft-365/excel)
[![Power Query](https://img.shields.io/badge/Power_Query-ETL-0078D4?style=for-the-badge&logo=powerbi&logoColor=white)](https://powerquery.microsoft.com/)
[![Excel BI](https://img.shields.io/badge/Excel_BI-Interactive_Dashboard-F2C811?style=for-the-badge&logo=googleanalytics&logoColor=black)](#10-interactive-excel-dashboard)
[![Data Analytics](https://img.shields.io/badge/Analytics-Supply_Chain-blue?style=for-the-badge)](https://github.com/Manipalsai/Supply-Chain-Operations-Inventory-Analytics)

An end-to-end **Supply Chain Business Intelligence and Analytics solution** built in **Microsoft Excel 2024**. This project demonstrates data cleaning and transformation via Power Query, analytical modeling, dynamic array calculations, custom KPI architecture, and an interactive executive BI dashboard.

![Supply Chain Operations & Inventory Analytics Dashboard](Dashboard/Supply_Chain_Operations_Inventory_Analytics_Dashboard.png)

---

## Table of Contents
- [1. Project Overview](#1-project-overview)
- [2. Business Problem](#2-business-problem)
- [3. Project Objectives](#3-project-objectives)
- [4. Dataset](#4-dataset)
- [5. Dataset Structure](#5-dataset-structure)
- [6. Tools & Technologies](#6-tools--technologies)
- [7. Data Preparation & Power Query](#7-data-preparation--power-query)
- [8. Analytical Framework](#8-analytical-framework)
- [9. KPI Summary](#9-kpi-summary)
- [10. Interactive Excel Dashboard](#10-interactive-excel-dashboard)
- [11. Analysis Performed](#11-analysis-performed)
- [12. Key Business Insights](#12-key-business-insights)
- [13. Business Recommendations](#13-business-recommendations)
- [14. Workbook Structure](#14-workbook-structure)
- [15. Project Workflow](#15-project-workflow)
- [16. Limitations](#16-limitations)
- [17. Future Improvements](#17-future-improvements)
- [18. Skills Demonstrated](#18-skills-demonstrated)
- [19. Author](#19-author)

---

## 1. Project Overview

Supply chain operations require regular coordination between customer demand, supplier lead times, distribution facilities, and inventory replenishment thresholds. Maintaining visibility across these components helps organizations balance stock availability against inventory holding costs.

This project delivers an end-to-end analytics and business intelligence solution in **Microsoft Excel 2024**. By analyzing **91,251 operational records** spanning 50 SKUs, 5 warehouses, 10 suppliers, and 4 geographic regions across 2024, the project evaluates sales performance, inventory levels, supplier lead times, and forecast accuracy.

---

## 2. Business Problem

Supply chain teams manage multiple operational challenges across their distribution network:
- **Inventory & Buffer Management:** Maintaining adequate on-hand stock across regional warehouses while avoiding excess inventory buildup.
- **Supplier Lead Time Tracking:** Monitoring vendor delivery timelines to support replenishment scheduling.
- **Demand Forecast Monitoring:** Assessing variance between forecasted demand and actual unit sales.
- **Regional & Facility Distribution:** Reviewing sales volume and stock distribution across multi-location warehouse hubs.
- **Operational Reporting:** Consolidating transactional supply chain data into a dynamic, interactive Excel BI dashboard.

---

## 3. Project Objectives

1. **Perform Data Cleaning & Transformation:** Clean, validate, and transform 91,251 raw transactional records using Power Query.
2. **Develop Core Business Metrics:** Calculate revenue, cost, gross profit, margin, and forecast accuracy metrics.
3. **Execute Multi-Dimensional Analysis:** Analyze operational data across time (monthly trends), geography (4 regions), facilities (5 warehouses), vendors (10 suppliers), and products (50 SKUs).
4. **Construct an Interactive Excel Dashboard:** Build an interactive reporting dashboard powered by a dedicated calculation layer (`Dashboard_Data`) with Data Validation dropdown filters, KPI summary cards, and analytical charts.
5. **Formulate Analytical Recommendations:** Provide grounded business suggestions based on observed sales, inventory, and supplier patterns.

---

## 4. Dataset

- **Dataset Name:** High-Dimensional Supply Chain Inventory Dataset
- **Source:** Kaggle (Created by Ziya)
- **Local Dataset File:** [`Dataset/supply_chain_dataset1.csv`](Dataset/supply_chain_dataset1.csv)
- **Dataset Documentation & Kaggle Link:** [Dataset Documentation](Dataset/dataset_source.md)
- **Time Period:** 01-Jan-2024 to 31-Dec-2024 (Full calendar year)
- **Dataset Nature:** Simulated / synthetic dataset designed for analytics, demand modeling, and reporting. *(Note: Not sourced from real-world corporate or proprietary retail databases).*

---

## 5. Dataset Structure

| Column Name | Data Type | Role | Description |
| :--- | :--- | :--- | :--- |
| `Date` | Date | Attribute | Transaction date (01-Jan-2024 to 31-Dec-2024) |
| `SKU_ID` | Text | Dimension | Product identifier (50 unique SKUs: `SKU_1` to `SKU_50`) |
| `Warehouse_ID` | Text | Dimension | Regional distribution facility (`WH_1` to `WH_5`) |
| `Supplier_ID` | Text | Dimension | Supplier partner (`SUP_1` to `SUP_10`) |
| `Region` | Text | Dimension | Geographic market (`North`, `South`, `East`, `West`) |
| `Units_Sold` | Integer | Metric | Daily units sold per SKU and location |
| `Inventory_Level` | Integer | Metric | Available on-hand physical stock quantity |
| `Supplier_Lead_Time_Days` | Integer | Metric | Supplier delivery lead time in days |
| `Reorder_Point` | Integer | Metric | Stock threshold triggering replenishment |
| `Order_Quantity` | Integer | Metric | Quantity ordered from supplier |
| `Unit_Cost` | Decimal | Metric | Procurement cost per unit (currency units) |
| `Unit_Price` | Decimal | Metric | Selling price per unit (currency units) |
| `Promotion_Flag` | Binary | Attribute | `1` = active promotion; `0` = standard pricing |
| `Stockout_Flag` | Binary | Attribute | *Audited as constant 0; removed from cleaned output* |
| `Demand_Forecast` | Decimal | Metric | Provided demand forecast units |

*For complete field definitions and calculations, see the [Data Dictionary](Documentation/Data_Dictionary.md).*

---

## 6. Tools & Technologies

- **Primary Application:** Microsoft Excel 2024
- **ETL & Transformation:** Power Query (Data type validation, column cleansing, calculated columns)
- **Formulas & Functions:** `SUMIFS`, `AVERAGEIFS`, `SUMPRODUCT`, `LET`, Dynamic Array formulas (`TAKE`, `SORTBY`)
- **Reporting & Visuals:** PivotTables, Excel Charts, KPI Cards, Conditional Formatting
- **Interactivity:** Data Validation dropdown filters
- **Documentation:** Markdown

---

## 7. Data Preparation & Power Query

Data transformation was performed using Power Query to prepare the raw dataset for analytical modeling:

```
[Raw_Data] ──▶ [Power Query ETL] ──▶ [Clean_Data] ──▶ [Analytical Sheets] ──▶ [Dashboard_Data] ──▶ [Dashboard]
```

### Transformation Steps:
1. **Raw Data Ingestion:** Loaded the raw dataset into an Excel Table named `Raw_Data` (91,251 rows).
2. **Data Type Enforcement:** Verified data types for dates, text identifiers, integer quantities, and decimal values.
3. **Data Quality Checks:**
   - Missing values: 0 missing cells identified.
   - Duplicate rows: 0 duplicate records identified during validation.
4. **Column Cleansing (`Stockout_Flag` Removal):** The `Stockout_Flag` column contained only `0` values across all 91,251 records. It was removed from the cleaned output (`Clean_Data`) rather than being used to produce misleading stockout conclusions.
5. **Calculated Fields Created in Power Query:**
   - `Revenue` = `Units_Sold × Unit_Price`
   - `Cost` = `Units_Sold × Unit_Cost`
   - `Forecast_Variance` = `Units_Sold − Demand_Forecast`
   - `Absolute_Forecast_Error` = `ABS(Forecast_Variance)`
   - `Forecast_Accuracy` = `1 − (Absolute_Forecast_Error / Units_Sold)` *(with division-by-zero handling)*

---

## 8. Analytical Framework

The analytical workflow evaluates core supply chain dimensions:

```
┌────────────────────────────────────────────────────────────────────────┐
│               Supply Chain Operational Analytics Framework             │
└───────────────────────────────────┬────────────────────────────────────┘
          ┌─────────────────────────┼─────────────────────────┐
          ▼                         ▼                         ▼
   Demand & Sales           Inventory & Supply          Forecasting
   - Units Sold Trends      - On-Hand Inventory         - Actual vs Forecast
   - Revenue & Cost         - Reorder Point Buffers     - Forecast Variance
   - Gross Profit & Margin  - Supplier Lead Times       - Forecast Accuracy (%)
   - Regional Breakdown     - Order Quantities          - SKU-Level Tracking
```

---

## 9. KPI Summary

Validated baseline metrics across the complete 2024 dataset:

| Key Performance Indicator (KPI) | Validated Value | Description |
| :--- | :--- | :--- |
| **Total Records** | **91,251** | Total transaction rows in dataset |
| **Total Units Sold** | **1,829,979 Units** | Total product volume sold |
| **Total Revenue** | **33,426,337.22** | Total sales revenue in currency units |
| **Total Cost** | **22,338,135.99** | Estimated cost based on Unit_Cost |
| **Gross Profit** | **11,088,201.23** | Total revenue minus total cost |
| **Profit Margin** | **33.2%** | Gross profit as a percentage of revenue |
| **Average Inventory Level** | **471.5 Units** | Average on-hand inventory across records |
| **Peak Inventory** | **990 Units** | Highest single on-hand inventory level |
| **Average Supplier Lead Time** | **8.0 Days** | Average supplier fulfillment lead time |
| **Total Order Quantity** | **1,758,615 Units** | Total replenishment volume ordered |
| **Overall Forecast Accuracy** | **~99.8%** | Overall accuracy based on provided forecast |

---

## 10. Interactive Excel Dashboard

The Excel BI Dashboard provides an interactive interface powered by the `Dashboard_Data` calculation sheet.

### Dynamic Filters:
- **Region Filter** (Data Validation dropdown)
- **Warehouse Filter** (Data Validation dropdown)
- **Supplier Filter** (Data Validation dropdown)

Selecting options in these dropdowns dynamically updates the calculation layer, recalculating the KPI cards and chart visuals.

### Dashboard KPI Cards:
1. **Total Units Sold**
2. **Total Revenue**
3. **Gross Profit**
4. **Profit Margin**
5. **Forecast Accuracy**

### Dashboard Charts & Visuals:
1. **Monthly Units Sold:** 12-month demand trajectory across 2024.
2. **Actual vs Forecast Demand:** Side-by-side comparison of actual units sold against forecasted demand.
3. **Units Sold by Region:** Breakdown of unit sales across North, South, East, and West.
4. **Units Sold by Warehouse:** Distribution of unit sales across warehouses `WH_1` through `WH_5`.
5. **Supplier Performance — Units Sold:** Unit volume fulfillment across suppliers `SUP_1` through `SUP_10`.
6. **Inventory vs Reorder Point by Warehouse:** On-hand inventory levels compared against reorder thresholds.
7. **Top 10 SKUs by Units Sold:** Ranking of top products by sales volume.
8. **Top 10 SKUs by Average Inventory:** Ranking of products by average inventory level.
9. **Business Insights Section:** On-dashboard summary of operational takeaways.

---

## 11. Analysis Performed

- **Regional Analysis:** Evaluated sales volume distribution across the 4 geographic regions.
- **Warehouse Analysis:** Examined unit sales and inventory levels across the 5 distribution facilities.
- **Supplier Analysis:** Assessed supplier fulfillment volumes and lead times across the 10 vendors.
- **SKU Analysis:** Analyzed unit sales, revenue, cost, and average inventory for all 50 SKUs.
- **Monthly Demand Analysis:** Evaluated monthly sales trends across 2024 to identify volume variations.
- **Promotion Analysis:** Compared units sold and pricing under promotional vs. standard conditions.
- **Inventory & Reorder Point Analysis:** Evaluated on-hand inventory levels relative to designated reorder points.
- **Forecast Variance & Accuracy Analysis:** Measured absolute forecast errors, variance, and accuracy percentages.
- **KPI Analysis:** Aggregated primary financial and operational supply chain metrics.
- **Business Insights Development:** Documented observations and analytical recommendations.

---

## 12. Key Business Insights

*For the complete detailed report, see [Business Insights](Documentation/Business_Insights.md).*

- **Monthly Sales Pattern:** March recorded the highest monthly unit sales at approximately **231.6K units**, while September recorded the lowest at approximately **76.3K units**.
- **Regional Sales:** The **East** region recorded the highest unit sales among the four regions at approximately **460.0K units**.
- **Warehouse Balance:** Unit sales across the 5 warehouses were relatively balanced, ranging from approximately **365.1K to 366.9K units**.
- **Supplier Volume:** **SUP_7** recorded the highest supplier unit volume at approximately **248.8K units**.
- **Supplier Lead Time:** Average supplier lead time was consistent at approximately **8.0 days** across all 10 suppliers.
- **Inventory Level:** Average inventory across the dataset was approximately **471.5 units**, with a peak observed level of **990 units**.
- **Forecast Accuracy:** The provided demand forecast tracked sales closely, yielding an overall forecast accuracy of approximately **99.8%**.

---

## 13. Business Recommendations

1. **Incorporate Monthly Demand Patterns into Planning:** Use observed monthly sales trends to assist in inventory planning around higher-demand periods (such as March) and lower-demand periods (such as September).
2. **Monitor Supplier Volume and Lead Times:** Track vendor lead-time metrics and volume allocations to identify suppliers (such as `SUP_7`) that represent significant fulfillment share.
3. **Align Regional & Warehouse Allocation:** Utilize regional and facility sales patterns to support stock allocation across distribution hubs.
4. **Track Demand Forecast Variance:** Continue monitoring forecast variance across individual SKUs and months to identify potential demand planning discrepancies.
5. **Review SKU-Level Inventory & Sales Dynamics:** Use product-level sales and inventory metrics to identify items that may warrant replenishment review.

---

## 14. Workbook Structure

The Excel workbook [`Excel/Supply_Chain_Operations_Inventory_Analytics.xlsx`](Excel/Supply_Chain_Operations_Inventory_Analytics.xlsx) contains exactly **14 worksheets**:

```
Supply_Chain_Operations_Inventory_Analytics.xlsx
│
├── 1. Dashboard                  - Interactive Executive BI Dashboard
├── 2. Dashboard_Data             - Dynamic helper and calculation layer
├── 3. Region_Analysis            - Sales and unit analysis by region
├── 4. Warehouse_Analysis         - Throughput and inventory by warehouse
├── 5. Supplier_Analysis          - Vendor volume, lead times, and orders
├── 6. SKU_Analysis               - Product-level sales, margins, and costs
├── 7. Monthly_Analysis           - Monthly sales and demand trends
├── 8. Promotion_Analysis         - Sales performance with and without promotions
├── 9. Inventory_Risk_Analysis    - Stock levels and reorder point comparison
├── 10. Forecast_Analysis         - Actual vs forecast demand and accuracy metrics
├── 11. Business_Insights         - Written summary of analytical findings
├── 12. Clean_Data                - Cleaned analytical table from Power Query
├── 13. KPI_Analysis              - Master KPI calculations and metrics
└── 14. Raw_Data                  - Original dataset table (91,251 records)
```

---

## 15. Project Workflow

```
┌────────────────────────────────────────────────────────┐
│                   Raw Dataset (CSV)                    │
│             91,251 rows | 15 original columns          │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│                    Excel Raw_Data                      │
│             Preserved Original Data Table              │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│              Power Query / Data Cleaning               │
│    Data Cleaning | Type Validation | Calculated Fields │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│                      Clean_Data                        │
│          Cleaned Analytical Table for Modeling         │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│                   Analytical Sheets                    │
│   PivotTables | SUMIFS | AVERAGEIFS | Dynamic Arrays   │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│                    Dashboard_Data                      │
│           Dynamic Filter Calculation Layer             │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│               Interactive BI Dashboard                 │
│      Dynamic KPI Cards | Dropdowns | Visual Charts     │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│                   Business Insights                    │
│         Analytical Observations & Suggestions          │
└───────────────────────────┬────────────────────────────┘
```

---

## 16. Limitations

- **Simulated Dataset:** The dataset is synthetically generated; real-world supply chain operations typically exhibit higher variance and unexpected disruptions.
- **Constant Stockout Flag:** The original `Stockout_Flag` column contained only zeros and was removed during cleaning; stockout evaluations were based on stock levels versus reorder points.
- **Single-Year Horizon:** Covers calendar year 2024; multi-year historical data would be needed for multi-year trend analysis.
- **Provided Forecast Field:** Forecast accuracy is evaluated against the provided `Demand_Forecast` field; this project did not build an independent machine-learning forecasting model.
- **Excel Environment:** The project is contained entirely within Excel and does not implement automated external database refreshes.

---

## 17. Future Improvements

- **Power BI / Tableau Deployment:** Building interactive dashboards in Power BI or Tableau with automated data refreshes.
- **SQL Pipeline Integration:** Migrating data ingestion and preprocessing to a SQL database (e.g., PostgreSQL or Snowflake).
- **Independent Forecasting Models:** Developing Python-based time series models (e.g., ARIMA or Prophet) to compare against baseline forecasts.
- **Advanced Inventory Modeling:** Exploring Economic Order Quantity (EOQ) and safety stock formulas factoring in lead time variability.

---

## 18. Skills Demonstrated

- **Excel Business Intelligence:** Interactive Dashboard Design, Dynamic Calculation Layers (`Dashboard_Data`), Data Validation Dropdown Filters, Visual Formatting.
- **Advanced Excel Analytics:** Excel Tables, PivotTables, `SUMIFS`, `AVERAGEIFS`, `SUMPRODUCT`, `LET`, Dynamic Array Formulas (`TAKE`, `SORTBY`).
- **Data Preparation & ETL:** Power Query, Data Type Validation, Data Cleaning, Calculated Column Creation.
- **Supply Chain Analytics:** Inventory vs Reorder Point Analysis, Supplier Lead Time Tracking, Monthly Demand Seasonality, Forecast Variance Evaluation.
- **Business Analysis & Reporting:** KPI Architecture, Financial Metric Calculation (Revenue, Cost, Margin), Written Executive Summaries.

---

## 19. Author

**Manipalsai**
- **GitHub:** [@Manipalsai](https://github.com/Manipalsai)
- **Project Repository:** [Supply-Chain-Operations-Inventory-Analytics](https://github.com/Manipalsai/Supply-Chain-Operations-Inventory-Analytics)

---
*If you find this project helpful or insightful, please consider giving it a ⭐ on GitHub!*
