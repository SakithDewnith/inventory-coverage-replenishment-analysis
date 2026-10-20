# Inventory Coverage & Replenishment Analysis (Excel)

## Executive Summary

Inventory affects both product availability and the cash tied up in stock, but total stock alone does not show where replenishment attention is most needed.

Using **Excel (Power Query, PivotTables and formulas)**, I analyzed 91,250 daily inventory records across 50 SKUs, 5 warehouses and 10 suppliers during 2024. Demand changed seasonally while average stock per record stayed within a narrow range, so monthly coverage ranged from 15.2 days in April to 46.1 days in October.

On the latest snapshot (30 December 2024), inventory was valued at $1.40M at cost. Reorder-point and lead-time checks flagged 18 unique SKU–warehouse records for review: 14 at or below their reorder points and 5 with potential lead-time shortfalls, with 1 in both.

These results point to specific actions: replenish the flagged records, set reorder points by season, and hold new orders on the highest-coverage items.

*The dataset is synthetic; findings are analytical examples, not real-company results.*

<br>

**Workflow:**
<p align="center">
<img width="754" height="120" alt="Inventory_coverage_project_workf…_20261018213426" src="https://github.com/user-attachments/assets/41e1ca32-ea04-43af-aeda-56411ff5db14" />
</p>

<br> 

## Business Problem:
Inventory levels that do not keep pace with changing demand can lead to replenishment risk during high-demand periods and capital tied up in inventory during low-demand periods. With limited purchasing and review resources, the business needs to determine whether inventory levels are appropriate for demand, where potential replenishment issues exist, and which products and warehouses should receive attention first.
<br>
<br>

## Skills:

- **Excel:** Power Query, Excel Tables, PivotTables, PivotCharts, formulas, filtering and sorting, charts
- **Data preparation:** data cleaning, validation checks, data quality log
- **Inventory analysis:** stock coverage, reorder points, supplier lead-time analysis, inventory valuation
- **Demand analysis:** seasonality, forecast accuracy (MAE and bias)
- **Business analysis:** problem framing, prioritization, recommendations
<br>

## Methodology
1. **Data preparation:** Imported 91,250 daily SKU-warehouse records, kept the original data and a backup copy, and cleaned the data using Power Query.

2. **Data quality checks:** Checked for missing values, duplicates, repeated Date–SKU–Warehouse combinations, data types, value ranges and unit cost against unit price, and documented the results in a quality log. `Stockout_Flag` was 0 in every record, so actual stockout events could not be measured. Reorder status and lead-time shortfall were used as indicators for further review.

3. **Demand trends and forecast accuracy:** Compared monthly units sold with forecast demand, and measured forecast accuracy using mean absolute error (MAE) and bias.

4. **Monthly coverage analysis:** Divided average monthly inventory by average daily forecast demand to show how stock coverage changes through the year. Averages were used because some records have zero forecast demand.

5. **Inventory coverage analysis:** Calculated days of coverage for the latest snapshot (30 December 2024) and compared it across SKUs and warehouses.

6. **Replenishment analysis:** Applied two separate checks to the latest snapshot: records at or below their reorder point, and records where inventory was below forecast demand during supplier lead time. Kept full-year replenishment counts separate as historical context.

7. **Inventory value analysis:** Multiplied inventory level by unit cost for the latest snapshot only, avoiding repeated valuation of the same stock across daily records.

8. **Prioritized review and recommendations:** Combined both replenishment checks into one list of unique records (removing the overlap), added a table of the 10 highest-coverage records, and ranked both by risk and inventory value. Findings and recommended actions were drawn from this list and the earlier analyses.
<br>

## Key Findings & Results

The analysis covered **91,250 daily inventory records** across 50 SKUs, 5 warehouses and 10 suppliers during 2024. Seasonal results use the full year. Record-level results use the latest snapshot (**30 December 2024**, 250 SKU–warehouse records).

- **Demand is seasonal.** Units sold range from 76,304 in September to 231,596 in March, while average stock per record stays within a narrow range (about 454 to 528 units).
- **So coverage swings with the season.** Stock lasts about 15.2 days in April but about 46.1 days in October, which points to possible replenishment pressure in busy months and higher coverage in slow months.
- **Replenishment checks flagged 18 unique SKU–warehouse records** on 30 December 2024: 14 at or below their reorder points and 5 with potential lead-time shortfalls, with 1 record in both. They hold about $60.4K, or 4.3% of the $1.40M inventory value. The full list is in the `Review_List` worksheet.
- **A reorder-point check alone is not enough.** Four of the five potential-shortfall records were above their reorder points, and all five have supplier lead times of 13 to 14 days.
- **Coverage differs most at record level, not by warehouse.** Warehouse averages are similar (24.4 to 27.5 days), but individual records range from 9.2 to 165.4 days. For example, SKU_41 has 19.6 days in WH_1 but 165.4 days in WH_5.
- **Next step:** validate the flagged records against open purchase orders and expected deliveries, review the 5 shortfall records first, then investigate high-coverage records and seasonal reorder settings before making any operational change.

*These are screening indicators from synthetic data, not confirmed stockouts or proven excess stock.*

### Charts

<table>
<tr>
<td width="33%" valign="top">

**1. Demand moves, stock does not: coverage is lowest in April and highest in October**

<img width="459" height="254" alt="Combo chart of monthly units sold and days of coverage in 2024" src="https://github.com/user-attachments/assets/c37dae27-6037-4061-b76f-9a440fa8f7ab" />

</td>
<td width="33%" valign="top">

**2. Coverage differs most between records: top 10 by days of coverage, 30 Dec 2024**

<img width="459" height="254" alt="Bar chart of the top 10 SKU-warehouse records by days of coverage" src="https://github.com/user-attachments/assets/66bc0279-2494-4562-9cc9-db44e0abde77" />

</td>
<td width="33%" valign="top">

**3. Warehouses look alike in stock value ($1.40M in total, 30 Dec 2024)**

<img width="459" height="254" alt="Bar chart of inventory value at cost by warehouse" src="https://github.com/user-attachments/assets/c0c9ffb4-6cb1-40f8-9b50-5e70ef4b2e2d" />

</td>
</tr>
</table>

### Supporting Observations

- **High-coverage records:** average record-level coverage was 25.85 days, ranging from 9.17 to 165.40 days. The 10 highest-coverage records hold about $73.8K (5.3% of inventory value). High coverage alone does not confirm excess inventory, so check demand and upcoming orders before considering stock reductions.
- **Warehouses:** average coverage ranged from 24.35 days (WH_1) to 27.49 days (WH_2). WH_2 holds the most stock value ($333,000.36) and WH_1 the least ($254,826.26).
- **Stock allocation:** SKU_41 has 19.6 days of coverage in WH_1 but 165.4 days in WH_5, which points to a possible stock-allocation question, such as a transfer, to investigate after checking cost and timing.
- **Forecast:** full-year forecast demand was about 1.832M units against 1.830M sold (mean absolute error 2.38 units per record), so the seasonal gap appears to come from stock planning and not demand prediction. This does not establish accuracy for individual SKUs, warehouses or months.

## Business Recommendations

| # | What to do | Which items | Why |
|---|---|---|---|
| 1 | **Order more stock now** for the 5 shortfall records| SKU_27 (WH_4) about 119 units, SKU_44 (WH_3) about 70, SKU_29 (WH_2) about 66, SKU_50 (WH_4) about 64, SKU_2 (WH_1) about 1 | Stock won't cover demand while waiting for the supplier |
| 2 | **Place re-orders** | for the 13 records at or below reorder point (about 133 units in total | They have reached their reorder point |
| 3 | **Raise the re-order level** for items with long supplier waits | Items with 13 to 14 day delivery times | The current levels missed 4 of the 5 items that could run short |
| 4 | **Plan orders by season:** order more before spring, and less in late summer and autumn | All products | Coverage is about 15 days in April but about 46 days in October |
| 5 | **Hold new orders** for the 10 highest-coverage records | The 10 items with 52 to 165 days of stock, such as (SKU_41 in WH_5, SKU_16 in WH_4, SKU_33 in WH_3 and others)) | They hold up to 165 days of stock, about $73.8K in total |
| 6 | **Move a small amount of SKU_41 from WH_5 to WH_1** instead of ordering | About 7 units of SKU_41 from WH_5 to WH_1 |  WH_5 has far more than it needs, and WH_1 is just below its reorder point |

*Unit numbers are estimates from the 30 December forecast, and they don't count orders already placed.*

## Conclusion

Stock does not follow seasonal demand, so coverage ranges from 15.2 days in April to 46.1 days in October. On 30 December 2024, 18 SKU–warehouse records were flagged for possible replenishment risk, and the highest-coverage records, led by SKU_41 in WH_5, were identified for possible excess stock. Warehouses look similar, so review should start with these individual records, ranked by risk and inventory value, and then move to seasonal reorder settings. Because the data has no real stockouts, stock targets or open orders, these results are signals to act on and check, not confirmed problems.

## Limitations

- The data is synthetic.
- `Stockout_Flag` is 0 in every record, so real stockouts can't be measured.
- High coverage does not prove excess stock, because the data has no target levels.
- No purchase order or transfer cost data was available.
- Results use one date (30 December 2024).
- The recommendations have not been tested.
  
