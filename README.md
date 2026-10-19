# Inventory Performance & Replenishment Planning (Excel)

## Executive Summary
Inventory affects both product availability and the cash tied up in stock, but total stock alone does not show where replenishment attention is most needed.

Using **Excel (Power Query, PivotTables, and formulas)**, I analyzed 91,250 daily inventory records across 50 SKUs, 5 warehouses, and 10 suppliers during 2024. The analysis examined inventory value, replenishment status, forecast performance, and stock coverage. Demand changed seasonally while average stock per record remained within a relatively narrow range, with monthly coverage ranging from **15.2 days in April to 46.1 days in October**.

On the latest snapshot (30 December 2024), inventory was valued at $**1.40M at cost**. Comparing inventory with reorder points and with forecast demand during supplier lead time flagged 14 of 250 SKU-warehouse records for reorder review and 5 for potential lead-time shortfalls.

These findings highlight opportunities to investigate seasonal replenishment planning and prioritize records for further review.

The dataset is synthetic; findings are analytical examples, not real-company results.

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
**SQL**: PostgreSQL, Data exploration(EDA), data cleaning, validation checks, aggregation, conditional aggregation (FILTER), GROUP BY analysis, calculated metrices

**Python**: Pandas, Matplotlib, SciPy and scikit-learn (Cramér's V, logistic regression cross-check), customer segmentation, factor screening, churn analysis, revenue exposure estimation, driver analysis, data visualization

**Power BI**: DAX measures, data modeling, interactive filtering, KPI cards, data visualization
<br>
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

- **Demand is seasonal.** Units sold range from 76,304 in September to 231,596 in March, while average stock per record stays within a narrow range (about 454 to 528 units).
- **So coverage swings with the season.** Stock lasts about 15.2 days in April but about 46.1 days in October, which points to possible replenishment pressure in busy months and higher coverage in slow months.
- **Replenishment checks flagged 18 unique SKU–warehouse records** on 30 December 2024: 14 at or below their reorder points and 5 with potential lead-time shortfalls, with 1 record in both. They hold about $60.4K, or 4.3% of the $1.40M inventory value.
- **A reorder-point check alone is not enough.** Four of the five potential-shortfall records were above their reorder points, and all five have supplier lead times of 13 to 14 days.
- **Coverage differs most at record level, not by warehouse.** Warehouse averages are similar (24.4 to 27.5 days), but individual records range from 9.2 to 165.4 days. For example, SKU_41 has 19.6 days in WH_1 but 165.4 days in WH_5.
- **Next step:** validate the flagged records against open purchase orders and expected deliveries, review the 5 shortfall records first, then investigate high-coverage records and seasonal reorder settings before making any operational change.

*These are screening indicators from synthetic data, not confirmed stockouts or proven excess stock.*


## Key Findings & Results

- **Demand varies significantly throughout the year**, ranging from 76,304 units in September to 231,596 in March, while inventory coverage ranges from 15.2 to 46.1 days.
- **These demand changes create different inventory coverage conditions**, indicating that replenishment settings should be reviewed against seasonal demand rather than treated as constant throughout the year.
- **Replenishment checks identified 18 unique SKU–warehouse records for review** in the latest snapshot: 14 at or below reorder points and 5 with potential lead-time shortfalls, including one record flagged by both checks.
- **Reorder-point checks alone do not capture every potential risk:** four of the five records with potential lead-time shortfalls were still above their reorder points.
- **Inventory coverage also varies considerably across individual records**, from 9.17 to 165.40 days, while the $1.40M inventory value at cost provides context for prioritizing further investigation.
- **The next step is to validate the flagged records against purchase orders and expected deliveries**, then investigate unusually high coverage, review seasonal replenishment settings, and assess whether stock allocation needs attention before making operational changes.

  


## Key Results & Business Insights

The analysis covered **91,250 daily inventory records** across 50 SKUs, 5 warehouses and 10 suppliers during 2024. Using Excel, Power Query, PivotTables and formulas, I examined demand trends, inventory coverage, replenishment indicators and inventory value. Seasonal results use the full year. Record-level results use the latest snapshot (**30 December 2024**, 250 SKU–warehouse records).

### 1. Seasonal Demand and Inventory Coverage
<br>
<p align="center">
<img width="459" height="254" alt="image" src="https://github.com/user-attachments/assets/c37dae27-6037-4061-b76f-9a440fa8f7ab" />
</p>

Demand peaked at **231,596 units in March** and fell to **76,304 in September**, while average stock stayed between about 454 and 528 units per record. Coverage ranged from **15.2 days in April to 46.1 days in October**.

**Business insight:** The same stock supports about 15 days of demand in spring and about 46 in autumn, so reorder points and order quantities warrant a seasonal review.

### 2. Replenishment Review Priorities

| Review check (30 Dec 2024) | Records | Stock value |
|---|---:|---:|
| At or below reorder point | 14 | about $40.1K |
| Potential lead-time shortfall | 5 | about $22.5K |
| Meeting both checks | 1 | about $2.2K |
| **Unique records flagged** | **18** | **about $60.4K (4.3% of $1.40M)** |

Four of the five shortfall records were above their reorder points, and all five have supplier lead times of 13 to 14 days.

**Business insight:** A long supplier wait needs more stock than a reorder point may provide, so both checks are needed. The 5 shortfall records are the first to review. The `Review_List` worksheet consolidates all 18.

### 3. High-Coverage Inventory
<br>
<p align="center">
<img width="459" height="254" alt="image" src="https://github.com/user-attachments/assets/66bc0279-2494-4562-9cc9-db44e0abde77" />
</p>

*Top 10 SKU–warehouse records by days of coverage on 30 December 2024.*
Average record-level coverage was **25.85 days**, ranging from **9.17 to 165.40 days**. The 10 highest-coverage records hold about **$73.8K** (5.3% of inventory value).

**Business insight:** Investigate demand, upcoming orders and replenishment timing before considering stock reductions. High coverage alone does not confirm excess inventory.

### 4. Warehouse Comparison
<br>
<p align="center">
<img width="459" height="254" alt="image" src="https://github.com/user-attachments/assets/c0c9ffb4-6cb1-40f8-9b50-5e70ef4b2e2d" />
</p>

*Stock value at cost on 30 December 2024. Total: $1,404,610.84.*
Average coverage ranged from **24.35 days in WH_1 to 27.49 days in WH_2**, so warehouses look alike on average. WH_2 held the highest inventory value at **$333,000.36**, compared with **$254,826.26** in WH_1. At record level, SKU_41 has **19.6 days of coverage in WH_1 but 165.4 days in WH_5**.

**Business insight:** Warehouse averages can conceal differences between individual records. Review should focus on SKU–warehouse records, and differences like SKU_41's point to a possible stock-allocation question, such as a transfer, to investigate after checking cost and timing.

### 5. Forecast Performance

Full-year forecast demand was approximately **1.832 million units**, compared with **1.830 million sold**, with a mean absolute error of **2.38 units per record**.

**Business insight:** Forecast and actual demand were close in aggregate, so the seasonal gap appears to come from stock planning and not demand prediction. This does not establish accuracy for individual SKUs, warehouses or months.

## Recommended Business Follow-Up

| Priority | Action | Confirm first |
|---|---|---|
| 1 | Review the 5 possible-shortfall records | Open purchase orders and delivery dates |
| 2 | Review the other 13 records at or below reorder point | Whether the reorder point still fits demand |
| 3 | Review reorder settings against seasonal demand and lead times | Whether the pattern repeats in other years |
| 4 | Check high-coverage records, and a possible SKU_41 transfer, before any stock reduction | Planned orders, transfer cost and time |

These are proposed actions, not implemented or tested changes.

## Limitations

- The dataset is **synthetic**, so the findings are illustrative and not results from a real company.
- `Stockout_Flag` is 0 in every record, so actual stockouts cannot be measured. Replenishment indicators identify records for investigation, not confirmed stockouts.
- High coverage does not prove excess inventory, and open purchase orders and optimal stock targets were not available.
- Record-level results reflect a single snapshot, not live inventory.
  
