# Dataset Source & Overview

## Dataset Information
- **Dataset Title:** High-Dimensional Supply Chain Inventory Dataset
- **Source Platform:** Kaggle
- **Creator / Publisher:** Ziya
- **Direct Kaggle URL:** [High-Dimensional Supply Chain Inventory Dataset on Kaggle](https://www.kaggle.com/datasets/ziya07/high-dimensional-supply-chain-inventory-dataset)
- **Data Type:** Simulated / Synthetic Supply Chain Operational Dataset
- **Time Period:** 01-Jan-2024 to 31-Dec-2024 (Full Year 2024)

---

## Dataset Characteristics

| Attribute | Specification |
| :--- | :--- |
| **Total Records** | 91,251 rows |
| **Original Columns** | 15 columns |
| **Time Coverage** | 01-Jan-2024 to 31-Dec-2024 |
| **Products (SKUs)** | 50 unique SKUs (`SKU_1` to `SKU_50`) |
| **Distribution Centers** | 5 Warehouses (`WH_1` to `WH_5`) |
| **Suppliers** | 10 Suppliers (`SUP_1` to `SUP_10`) |
| **Geographic Regions** | 4 Regions (`North`, `South`, `East`, `West`) |
| **Missing Values** | 0 missing cells identified |
| **Duplicate Rows** | 0 duplicate rows identified during validation |

---

## Nature of the Dataset

This dataset is a simulated, synthetic supply chain dataset designed for inventory modeling, sales demand analysis, and business intelligence reporting. 

> **Important Note:** This dataset is simulated and not sourced from any proprietary or real-world corporate database (such as Amazon or any other retailer).

---

## Original Schema (15 Columns)

1. `Date` – Transaction date (01-Jan-2024 to 31-Dec-2024)
2. `SKU_ID` – Stock Keeping Unit identifier (`SKU_1` to `SKU_50`)
3. `Warehouse_ID` – Warehouse location identifier (`WH_1` to `WH_5`)
4. `Supplier_ID` – Supplier partner identifier (`SUP_1` to `SUP_10`)
5. `Region` – Geographic sales region (`North`, `South`, `East`, `West`)
6. `Units_Sold` – Daily units sold
7. `Inventory_Level` – Physical inventory units on hand
8. `Supplier_Lead_Time_Days` – Supplier fulfillment lead time in days
9. `Reorder_Point` – Minimum stock threshold triggering replenishment
10. `Order_Quantity` – Replenishment quantity ordered from supplier
11. `Unit_Cost` – Acquisition cost per unit
12. `Unit_Price` – Selling price per unit
13. `Promotion_Flag` – Binary indicator (`1` = active promotion, `0` = standard pricing)
14. `Stockout_Flag` – Binary indicator in raw data (*Contains only `0` values across all 91,251 records*)
15. `Demand_Forecast` – Provided demand forecast units

---

## Data Cleaning & Transformation Notes

- **Handling of `Stockout_Flag`:** During Power Query ETL, `Stockout_Flag` was audited and found to be constant `0` across all 91,251 rows. To avoid misleading analysis, it was excluded from the cleaned analytical dataset (`Clean_Data`).
- **Calculated Fields Created:**
  - `Revenue` = `Units_Sold × Unit_Price`
  - `Cost` = `Units_Sold × Unit_Cost`
  - `Forecast_Variance` = `Units_Sold − Demand_Forecast`
  - `Absolute_Forecast_Error` = `ABS(Forecast_Variance)`
  - `Forecast_Accuracy` = `1 − (Absolute_Forecast_Error / Units_Sold)` *(with division-by-zero handling)*

---

## How to Access the Data

The raw data can be downloaded directly from the Kaggle link above or viewed in the `Raw_Data` worksheet of the project workbook: [`Excel/Supply_Chain_Operations_Inventory_Analytics.xlsx`](../Excel/Supply_Chain_Operations_Inventory_Analytics.xlsx).
