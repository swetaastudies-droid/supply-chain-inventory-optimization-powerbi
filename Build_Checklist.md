# Build Checklist

## Step 1 — Prepare
- [ ] Extract the ZIP into a project folder.
- [ ] Review the Excel workbook and its three sheets.

## Step 2 — Import
- [ ] Open Power BI Desktop.
- [ ] Home > Get data > Excel workbook.
- [ ] Select `data/Supply_Chain_Efficiency_Inventory_Optimization_Dataset.xlsx`.
- [ ] Select `Supply Chain Data` in Navigator.
- [ ] Choose Transform Data.

## Step 3 — Power Query cleaning
- [ ] Confirm column data types.
- [ ] Check blanks and errors.
- [ ] Check duplicates carefully; repeated product/warehouse observations may be valid.
- [ ] Standardize text and status labels.
- [ ] Validate numeric ranges and stock calculations.
- [ ] Close & Apply.

## Step 4 — Model and measures
- [ ] Rename the main query to `FactSupplyChain` if using the included DAX notes.
- [ ] Create a Date table and mark it as the date table.
- [ ] Relate the Date table to the fact table's Date column.
- [ ] Create and validate the required measures.

## Step 5 — Build visuals
- [ ] KPI cards for inventory, sales, stockout, lead time, delivery, forecast, and cost indicators.
- [ ] Inventory by product category.
- [ ] Supplier delivery performance.
- [ ] Monthly units sold / inventory trend.
- [ ] Delivery status distribution.
- [ ] Forecast demand vs actual demand.
- [ ] Product inventory and reorder table.
- [ ] Slicers for region, supplier, category, warehouse, and month/date.

## Step 6 — Design report pages
- [ ] Executive Overview.
- [ ] Inventory Optimization.
- [ ] Supplier & Procurement.
- [ ] Demand & Replenishment.
- [ ] Apply consistent colours, typography, spacing, titles, and number formats.

## Step 7 — Validate insights
- [ ] Check visual totals against data.
- [ ] Confirm slicer interactions.
- [ ] Fill in `Business_Insights_Template.md`.
- [ ] Save the PBIX in `powerbi/`.
- [ ] Add report screenshots to `screenshots/`.
