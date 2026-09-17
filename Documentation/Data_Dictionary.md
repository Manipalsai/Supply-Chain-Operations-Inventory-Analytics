# Data Dictionary

This document outlines the complete schema, data types, field definitions, and business logic for both the raw and transformed datasets used in the **Supply Chain Operations & Inventory Analytics** project.

---

## 1. Raw Dataset Schema (`Raw_Data`)

The raw table contains **91,251 records** and **15 columns** covering daily operations throughout 2024.

| Column Name | Data Type | Field Type | Example | Description & Business Context |
| :--- | :--- | :--- | :--- | :--- |
| **`Date`** | Date | Original | `2024-01-01` | Transaction and recording date spanning from 01-Jan-2024 to 31-Dec-2024. |
| **`SKU_ID`** | Text | Original | `SKU_1` | Unique identifier for 50 distinct Stock Keeping Units (`SKU_1` to `SKU_50`). |
| **`Warehouse_ID`** | Text | Original | `WH_1` | Unique identifier for 5 fulfillment/distribution facilities (`WH_1` to `WH_5`). |
| **`Supplier_ID`** | Text | Original | `SUP_1` | Unique identifier for 10 vendor partners (`SUP_1` to `SUP_10`). |
| **`Region`** | Text | Original | `East` | Target geographic market segment (`North`, `South`, `East`, `West`). |
| **`Units_Sold`** | Integer | Original | `25` | Number of physical units sold for the specific SKU, location, and date. |
| **`Inventory_Level`** | Integer | Original | `480` | Current on-hand available inventory stock at the specified warehouse. |
| **`Supplier_Lead_Time_Days`** | Integer | Original | `8` | Vendor delivery lead time required to fulfill an order (in days). |
| **`Reorder_Point`** | Integer | Original | `350` | Predetermined threshold triggering automated replenishment when inventory falls below this level. |
| **`Order_Quantity`** | Integer | Original | `200` | Batch replenishment quantity ordered from the supplier. |
| **`Unit_Cost`** | Decimal ($) | Original | `$12.50` | Direct acquisition / manufacturing cost per unit paid to the supplier. |
| **`Unit_Price`** | Decimal ($) | Original | `$18.99` | Retail selling price per unit billed to the customer. |
| **`Promotion_Flag`** | Binary (0/1) | Original | `1` | Marketing flag: `1` indicates an active marketing/discount promotion, `0` indicates standard pricing. |
| **`Stockout_Flag`** | Binary (0/1) | Original (Raw Only) | `0` | Raw dataset flag. *Note: Audited as constant 0 across all 91,251 records; excluded from analytical model to prevent misleading insights.* |
| **`Demand_Forecast`** | Decimal | Original | `24.8` | Expected customer demand units projected by baseline predictive models. |

---

## 2. Transformed & Calculated Fields (`Clean_Data` & Analytical Layer)

Calculated during the Power Query ETL pipeline and analytical modeling layer to enable financial, operational, and forecast accuracy analysis.

| Metric / Field Name | Data Type | Field Type | Calculation Formula / Business Logic | Purpose & Context |
| :--- | :--- | :--- | :--- | :--- |
| **`Revenue`** | Currency ($) | Calculated (ETL) | `[Units_Sold] * [Unit_Price]` | Total gross monetary value generated from sales. |
| **`Cost`** | Currency ($) | Calculated (ETL) | `[Units_Sold] * [Unit_Cost]` | Total Cost of Goods Sold (COGS). |
| **`Gross_Profit`** | Currency ($) | Calculated (BI) | `[Revenue] - [Cost]` | Total gross margin generated before operating overhead. |
| **`Profit_Margin`** | Percentage (%) | Calculated (BI) | `[Gross_Profit] / [Revenue]` | Profitability percentage realized per dollar of sales. |
| **`Forecast_Variance`** | Decimal | Calculated (ETL) | `[Units_Sold] - [Demand_Forecast]` | Raw numerical difference between actual units sold and forecasted demand. |
| **`Absolute_Forecast_Error`** | Decimal | Calculated (ETL) | `ABS([Forecast_Variance])` | Absolute variance used for unbiased error evaluation. |
| **`Forecast_Accuracy`** | Percentage (%) | Calculated (ETL) | `IF([Units_Sold] = 0, 1, 1 - ([Absolute_Forecast_Error] / [Units_Sold]))` | Metric tracking forecast alignment relative to sales volume (bounded/handled for 0 sales). |
| **`Stock_Coverage_Ratio`** | Decimal | Calculated (BI) | `[Inventory_Level] / [Reorder_Point]` | Buffer safety ratio; values < 1.0 indicate potential replenishment risk. |

---

## 3. Data Integrity & Validation Rules Applied

1. **Completeness:** Every column was verified to contain 0 null / blank cells across all 91,251 records.
2. **Uniqueness:** Deduplication checks confirmed 0 duplicate rows across composite keys (`Date`, `SKU_ID`, `Warehouse_ID`, `Supplier_ID`, `Region`).
3. **Data Type Uniformity:** Date fields strictly formatted to `Date`, financial values formatted as `Currency ($)`, identifiers as `Text`, and quantities as `Integer`.
4. **ETL Filter Rules:** `Stockout_Flag` was pruned during ingestion to avoid uninformative bias.
