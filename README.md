# Supply Chain Efficiency & Inventory Optimization Dashboard

An interactive, single-page Power BI dashboard for analyzing inventory availability, stockout risk, reorder requirements, supplier delivery performance, and demand forecast accuracy.

## Project Objective

The objective of this project is to transform supply-chain data into actionable insights that can support inventory planning, replenishment decisions, supplier evaluation, and demand forecasting.

The dashboard brings important operational indicators together in one report, allowing users to explore patterns by region, supplier, product category, warehouse, and date.

> **Data notice:** This project uses synthetic sample data for learning and portfolio demonstration. The findings do not represent the performance of a real company.

## Tools Used

- **Microsoft Power BI Desktop** — report development and visualization
- **Power Query** — data cleaning and transformation
- **DAX (Data Analysis Expressions)** — measures and KPI calculations
- **Microsoft Excel** — source dataset
- **GitHub** — project versioning and portfolio presentation

## Dataset Description

The dataset contains 180 synthetic product/warehouse observations across 2025, with 26 columns.

Key fields include:

- **Product information:** Product ID, Product Name, Product Category
- **Supply chain dimensions:** Supplier Name, Warehouse Location, Region
- **Inventory:** Opening Stock, Incoming Stock, Units Sold, Closing Stock, Reorder Level, Reorder Status
- **Delivery:** Lead Time (Days), Delivery Time (Days), Delivery Status
- **Demand planning:** Demand Forecast, Actual Demand, Forecast Accuracy %
- **Cost and movement indicators:** Inventory Holding Cost, Inventory Turnover Ratio
- **Time fields:** Date, Month, Quarter, Year

The data is intended to demonstrate Power BI analysis techniques and should not be treated as a real operational dataset.

## Power Query Steps

The data preparation workflow included:

1. Imported the Excel dataset into Power BI Desktop.
2. Reviewed column names and data structure.
3. Assigned appropriate data types to dates, text fields, and numeric fields.
4. Checked for blank values and data-quality issues.
5. Verified stock, delivery, and demand-related fields.
6. Renamed the main table to `FactSupplyChain`.
7. Loaded the cleaned dataset into the Power BI data model.
8. Created a separate calendar table named `DimDate` using DAX.
9. Created a one-to-many relationship from `DimDate[Date]` to `FactSupplyChain[Date]`.
10. Sorted the month name by month number to preserve chronological order.

## DAX Measures

The report uses DAX measures to summarize inventory, delivery, and forecasting performance.

| Measure | Purpose |
|---|---|
| Total Opening Stock | Sums opening stock across the selected observations |
| Total Incoming Stock | Sums incoming stock |
| Total Units Sold | Calculates total units sold |
| Observed Closing Stock Sum | Sums recorded closing-stock observations |
| Stockout Observation Count | Counts observations flagged for stockout risk |
| Reorder Observation Count | Counts observations requiring reorder |
| Average Lead Time (Days) | Calculates average lead time |
| Average Delivery Time (Days) | Calculates average delivery time |
| Average Delivery Delay (Days) | Measures average positive delivery delay |
| On-Time Delivery Observation % | Calculates the proportion of observations marked on time |
| Total Forecast Demand | Sums forecast demand |
| Total Actual Demand | Sums actual demand |
| Absolute Forecast Error | Sums absolute forecast errors |
| WAPE % | Calculates weighted absolute percentage error |
| Inventory Holding Cost (Estimated) | Summarizes estimated holding-cost values |

### Important calculation notes

- Stockout risk is flagged when closing stock is zero **or** actual demand exceeds units sold.
- Reorder is required when closing stock is at or below the reorder level.
- On-time delivery is assessed by comparing delivery time with lead time.
- WAPE is calculated as total absolute forecast error divided by total actual demand.
- Holding-cost values are estimates; the dataset does not establish a verified currency or cost period.
- The inventory turnover field is a proxy and is not a formal financial inventory-turnover calculation.

Exact DAX definitions may be documented in `documentation/DAX_Measures.md`.

## Dashboard Features

The single-page dashboard is designed to include:

- KPI cards for key inventory, delivery, and forecasting metrics
- Inventory analysis by product category
- Supplier on-time delivery comparison
- Monthly units-sold trend
- Delivery status distribution
- Forecast demand versus actual demand comparison
- Product stock and reorder-status table
- Conditional formatting for reorder status
- Interactive slicers for Region, Supplier, Product Category, Warehouse Location, and Date Range

Visuals and measures respond to slicer selections to support focused analysis.

## Key Insights

The following results were calculated from the synthetic sample dataset.

### 1. Inventory and stockout risk

- 113 of 180 observations (62.8%) were flagged for stockout risk.
- Bluetooth Headphones had 11 stockout flags and 5 reorder-required observations.
- Water Bottle had 8 stockout flags.

**Recommendation:** Review replenishment settings for Bluetooth Headphones and investigate whether demand, stock availability, or data-recording rules explain the flagged observations.

### 2. Supplier delivery performance

- Observed on-time delivery rate: 72.2%.
- 50 of 180 observations (27.8%) were marked delayed.
- PackRight Solutions had the lowest observed on-time rate at 56.3%.
- HomeEase Trading had the highest observed on-time rate at 90.5%.

**Recommendation:** Investigate delay causes and review lead-time commitments with lower-performing suppliers.

### 3. Regional and warehouse patterns

- South recorded the highest regional units sold (2,154) and the highest regional stockout rate (66.2%).
- North had the lowest regional on-time rate (63.2%).
- Mumbai had the lowest warehouse stockout rate (48.4%).
- Chennai had the highest warehouse stockout rate (75.0%).

**Recommendation:** Review replenishment planning in South and delivery reliability in North. Investigate warehouse-level availability separately from delivery performance.

### 4. Demand forecasting

- Total forecast demand: 7,045 units.
- Total actual demand: 7,101 units.
- Absolute forecast error: 1,118 units.
- WAPE: 15.7%.

**Recommendation:** Examine forecast misses by product, region, and month. Similar aggregate totals can conceal substantial errors at individual-observation level.

### 5. Inventory movement proxy

- Electronics had the highest average inventory-turnover proxy (0.631).
- Sports & Fitness had the lowest average proxy (0.287).

**Recommendation:** Review movement and replenishment patterns in Sports & Fitness. Treat these figures as sample-data proxies, not formal financial turnover metrics.

## Screenshots

Dashboard overview:

![Supply Chain Dashboard Overview](screenshots/dashboard-overview.png)

Supplier performance and inventory analysis:

![Supplier Performance](screenshots/supplier-performance.png)

*Replace these image paths with your actual screenshot filenames. If the screenshots are not yet available, add them after completing the dashboard.*

## Conclusion

This project demonstrates how Power BI, Power Query, DAX, data modeling, and interactive visualizations can be combined to analyze supply-chain operations.

The sample analysis highlights stockout risk, supplier delivery reliability, and forecast errors as areas worth investigating. The dashboard provides a foundation for exploring these indicators by product, region, warehouse, supplier, and time period.

The results should be validated against real operational data before being used for business decisions.

## Limitations

- The dataset is synthetic and is intended for portfolio demonstration.
- Each row is a product/warehouse observation, not necessarily a unique shipment or a complete daily inventory ledger.
- Delivery metrics are observation-level because no unique shipment ID is available.
- The sum of closing-stock observations should not be interpreted as current inventory on hand.
- Holding-cost currency and time basis are not verified.
- Inventory turnover is represented by a proxy, not a formal financial calculation.

## Repository Structure

```text
data/           Source dataset and data notes
powerbi/        Power BI report file
screenshots/    Dashboard images
documentation/  Project notes, DAX, data dictionary, insights
reports/        Project summary and optional dashboard export
README.md       Project overview and documentation
```

## Author

K B SWETAA
