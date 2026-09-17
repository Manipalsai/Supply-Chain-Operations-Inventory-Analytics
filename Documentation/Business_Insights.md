# Supply Chain Business Insights & Recommendations

## Overview & Executive Summary

This report documents the analytical findings from the **Supply Chain Operations & Inventory Analytics** project, based on 91,251 records spanning the full calendar year 2024 across 50 SKUs, 5 warehouses, 10 suppliers, and 4 regions.

```
┌──────────────────────────┬──────────────────────────┬──────────────────────────┐
│       TOTAL REVENUE      │       GROSS PROFIT       │      PROFIT MARGIN       │
│      33,426,337.22       │      11,088,201.23       │          33.2%           │
├──────────────────────────┼──────────────────────────┼──────────────────────────┤
│     TOTAL UNITS SOLD     │    AVG INVENTORY LEVEL   │  AVG SUPPLIER LEAD TIME  │
│      1,829,979 Units     │       471.5 Units        │         8.0 Days         │
└──────────────────────────┴──────────────────────────┴──────────────────────────┘
```

---

## 1. Key Business Observations

### A. Monthly Demand Patterns
- **Peak Month:** March recorded the highest monthly unit sales at approximately **231.6K units**.
- **Lowest Month:** September recorded the lowest monthly unit sales at approximately **76.3K units**.
- **Observation:** Demand varied noticeably by month across the year, indicating periods of higher and lower product movement.

### B. Regional Sales Performance
- **Regional Sales:** The **East** region recorded the highest unit sales among the four regions at approximately **460.0K units**.
- **Balance:** Across all four regions (East, West, North, South), sales remained relatively distributed.

### C. Warehouse Fulfillment Distribution
- **Even Facility Distribution:** Total units sold per warehouse were relatively balanced across all 5 distribution centers (`WH_1` to `WH_5`), ranging from approximately **365.1K to 366.9K units**.

### D. Supplier Volume & Lead Times
- **Highest Volume Supplier:** **SUP_7** recorded the highest supplier unit volume at approximately **248.8K units**.
- **Lead Time Consistency:** Average supplier lead time across all 10 suppliers was approximately **8.0 days**.

### E. Inventory & Reorder Point Dynamics
- **Inventory Averages:** The average inventory level maintained across the dataset was approximately **471.5 units**, with a peak inventory level of **990 units**.
- **Replenishment Volume:** Total order quantity for replenishment was **1,758,615 units** against **1,829,979 units sold**.

### F. Demand Forecast Accuracy
- **Forecast Tracking:** The provided demand forecast tracked actual units sold closely, resulting in an overall forecast accuracy of approximately **99.8%**.

---

## 2. Summary of Key Analytical Metrics

| Analytical Area | Verified Metric | Business Observation |
| :--- | :--- | :--- |
| **Sales Volume** | 1,829,979 Units | Total units sold across all 50 SKUs. |
| **Financial Summary** | Revenue: 33,426,337.22 \| Profit: 11,088,201.23 | Overall gross profit margin of 33.2%. |
| **Monthly Peak** | March (~231.6K units) | Highest sales volume month in the dataset. |
| **Monthly Low** | September (~76.3K units) | Lowest sales volume month in the dataset. |
| **Leading Region** | East (~460.0K units) | Highest unit sales among the 4 regions. |
| **Leading Supplier** | SUP_7 (~248.8K units) | Highest fulfillment volume among the 10 suppliers. |
| **Supplier Lead Time** | 8.0 Days Average | Consistent lead time across vendor partners. |
| **Inventory Level** | 471.5 Units Average | Average physical stock level across locations. |
| **Forecast Accuracy** | ~99.8% Overall | Overall accuracy based on provided demand forecast. |

---

## 3. Business Recommendations

1. **Incorporate Monthly Demand Patterns into Planning:**
   - Use observed monthly demand trends to support inventory replenishment planning ahead of higher-demand periods (such as March) and adjust stocking during lower-demand periods (such as September).

2. **Monitor Supplier Volume and Lead Times:**
   - Continue tracking supplier fulfillment volumes and lead times, particularly for high-volume suppliers such as `SUP_7`, to ensure operational continuity.

3. **Align Regional and Warehouse Allocation:**
   - Use regional and warehouse sales patterns to support stock allocation decisions across the 5 distribution centers.

4. **Track Demand Forecast Variances:**
   - Regularly evaluate forecast variances and accuracy across individual SKUs and time periods to highlight areas where demand planning may require review.

5. **Review SKU-Level Stock and Sales Dynamics:**
   - Utilize SKU-level sales and average inventory metrics to identify products that may warrant closer replenishment and stocking attention.
