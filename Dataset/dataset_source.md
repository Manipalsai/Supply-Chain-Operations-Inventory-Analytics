# Dataset Source & Overview

## Dataset Information
- **Dataset Title:** High-Dimensional Supply Chain Inventory Dataset
- **Source Platform:** Kaggle
- **Creator / Publisher:** Ziya
- **Direct Kaggle URL:** [High-Dimensional Supply Chain Inventory Dataset on Kaggle](https://www.kaggle.com/datasets/ziya07/high-dimensional-supply-chain-inventory-dataset)
- **Data Type:** Simulated Supply Chain Operational Data
- **File Format:** CSV (`supply_chain_dataset1.csv`)

---

## Dataset Characteristics

| Attribute | Specification |
| :--- | :--- |
| **Total Record Count** | 91,251 rows |
| **Original Attributes** | 15 columns |
| **Time Period Covered** | 01-Jan-2024 to 31-Dec-2024 (Full Year 2024) |
| **Product Breadth** | 50 unique SKUs (`SKU_1` to `SKU_50`) |
| **Distribution Network** | 5 Warehouses (`WH_1` to `WH_5`) |
| **Supplier Base** | 10 Suppliers (`SUP_1` to `SUP_10`) |
| **Market Scope** | 4 Geographic Regions (East, West, North, South) |
| **Missing Values** | 0 missing cells |
| **Duplicate Records** | 0 duplicate rows |

---

## Scope & Nature of Data

This dataset represents a simulated multi-echelon supply chain operational environment across 2024. It records daily transactions across 50 SKUs, multiple regional distribution centers, and supplier fulfillment channels. 

> **Important Note:** This dataset is a simulated, synthetic dataset specifically designed for analytics, demand forecasting, inventory modeling, and business intelligence portfolio development. It does not represent proprietary or confidential data from any single commercial entity (e.g., Amazon or other commercial retailers).

---

## Raw Schema vs. Clean Analytical Schema

### Original Attributes (15 Columns):
1. `Date` – Transaction / recording date (DD-MM-YYYY)
2. `SKU_ID` – Unique product identifier (`SKU_1` to `SKU_50`)
3. `Warehouse_ID` – Warehouse location identifier (`WH_1` to `WH_5`)
4. `Supplier_ID` – Supplier partner identifier (`SUP_1` to `SUP_10`)
5. `Region` – Target geographical sales region (`North`, `South`, `East`, `West`)
6. `Units_Sold` – Daily units sold per SKU / location
7. `Inventory_Level` – Stock quantity on hand
8. `Supplier_Lead_Time_Days` – Vendor replenishment lead time in days
9. `Reorder_Point` – Inventory threshold triggering a replenishment order
10. `Order_Quantity` – Quantity ordered from supplier
11. `Unit_Cost` – Procurement cost per unit ($)
12. `Unit_Price` – Selling price per unit ($)
13. `Promotion_Flag` – Binary indicator (1 = Active promotional campaign, 0 = Standard pricing)
14. `Stockout_Flag` – Binary indicator in raw data (Contains only `0` values across all 91,251 rows)
15. `Demand_Forecast` – Model-generated expected demand units

### ETL Handling of `Stockout_Flag`:
During Power Query data transformation, `Stockout_Flag` was audited and found to contain exclusively `0` across all 91,251 records. Rather than retaining an uninformative constant or using it to construct misleading stockout insights, this column was intentionally excluded from the analytical dataset (`Clean_Data`). All stockout and inventory risk evaluations were instead rigorously calculated based on actual stock levels vs. reorder points (`Inventory_Level` vs. `Reorder_Point`).

---

## How to Access
The raw CSV file can be downloaded directly from the Kaggle link above or viewed in raw form within the `Raw_Data` worksheet of the project's Excel workbook: [`Excel/Supply_Chain_Operations_Inventory_Analytics.xlsx`](../Excel/Supply_Chain_Operations_Inventory_Analytics.xlsx).
