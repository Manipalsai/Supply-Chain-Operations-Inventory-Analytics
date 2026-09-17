# Data Dictionary

This document details the schema, field types, descriptions, and calculation logic for the **Supply Chain Operations & Inventory Analytics** project.

---

## 1. Raw Dataset Schema (`Raw_Data`)

The raw dataset contains **91,251 records** and **15 columns** covering the period from 01-Jan-2024 to 31-Dec-2024.

| Column Name | Data Type | Field Type | Example | Description |
| :--- | :--- | :--- | :--- | :--- |
| **`Date`** | Date | Original | `2024-01-01` | Transaction date spanning 01-Jan-2024 to 31-Dec-2024. |
| **`SKU_ID`** | Text | Original | `SKU_1` | Identifier for 50 distinct Stock Keeping Units (`SKU_1` to `SKU_50`). |
| **`Warehouse_ID`** | Text | Original | `WH_1` | Identifier for 5 distribution facilities (`WH_1` to `WH_5`). |
| **`Supplier_ID`** | Text | Original | `SUP_1` | Identifier for 10 supplier partners (`SUP_1` to `SUP_10`). |
| **`Region`** | Text | Original | `East` | Geographic market region (`North`, `South`, `East`, `West`). |
| **`Units_Sold`** | Integer | Original | `25` | Number of units sold on the given date and location. |
| **`Inventory_Level`** | Integer | Original | `480` | Available on-hand physical stock quantity. |
| **`Supplier_Lead_Time_Days`** | Integer | Original | `8` | Supplier delivery lead time in days. |
| **`Reorder_Point`** | Integer | Original | `350` | Inventory threshold triggering a replenishment order. |
| **`Order_Quantity`** | Integer | Original | `200` | Replenishment quantity ordered from the supplier. |
| **`Unit_Cost`** | Decimal | Original | `12.50` | Direct acquisition cost per unit (in currency units). |
| **`Unit_Price`** | Decimal | Original | `18.99` | Selling price per unit (in currency units). |
| **`Promotion_Flag`** | Binary (0/1) | Original | `1` | `1` = active promotion campaign; `0` = standard pricing. |
| **`Stockout_Flag`** | Binary (0/1) | Original | `0` | *Audited as constant 0 across all rows; removed from cleaned output.* |
| **`Demand_Forecast`** | Decimal | Original | `24.8` | Provided demand forecast units. |

---

## 2. Transformed & Calculated Fields (`Clean_Data` & Analytical Layer)

Created in Power Query and analytical sheets for financial, operational, and forecast evaluation.

| Metric / Field Name | Data Type | Field Type | Formula / Business Logic | Description |
| :--- | :--- | :--- | :--- | :--- |
| **`Revenue`** | Decimal | Calculated (Power Query) | `Units_Sold × Unit_Price` | Total sales revenue in currency units. |
| **`Cost`** | Decimal | Calculated (Power Query) | `Units_Sold × Unit_Cost` | Total cost in currency units. |
| **`Gross_Profit`** | Decimal | Calculated (Excel) | `Revenue − Cost` | Gross profit in currency units. |
| **`Profit_Margin`** | Percentage (%) | Calculated (Excel) | `Gross_Profit / Revenue` | Profit margin percentage. |
| **`Forecast_Variance`** | Decimal | Calculated (Power Query) | `Units_Sold − Demand_Forecast` | Difference between actual sales and forecasted demand. |
| **`Absolute_Forecast_Error`** | Decimal | Calculated (Power Query) | `ABS(Forecast_Variance)` | Absolute magnitude of forecast deviation. |
| **`Forecast_Accuracy`** | Percentage (%) | Calculated (Power Query) | `1 − (Absolute_Forecast_Error / Units_Sold)` | Forecast accuracy percentage (with zero handling). |

---

## 3. Data Integrity & Cleaning Summary

1. **Completeness:** 0 missing cells across all 91,251 records.
2. **Uniqueness:** 0 duplicate rows identified during data-quality checking.
3. **Data Types:** Enforced explicit types for Date, Text, Integer, and Decimal columns.
4. **Column Cleansing:** Removed `Stockout_Flag` because it contained only `0` values across the entire dataset.
