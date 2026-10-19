# DAX Measures — Working Notes

Create measures after loading the data and confirming the table/column names. If the imported table is not named `FactSupplyChain`, rename it or update the formulas.

```DAX
Total Opening Stock =
SUM ( FactSupplyChain[Opening Stock] )

Total Incoming Stock =
SUM ( FactSupplyChain[Incoming Stock] )

Total Units Sold =
SUM ( FactSupplyChain[Units Sold] )

Observed Closing Stock Sum =
SUM ( FactSupplyChain[Closing Stock] )

Stockout Observation Count =
CALCULATE (
    COUNTROWS ( FactSupplyChain ),
    FactSupplyChain[Stockout Status (Yes/No)] = "Yes"
)

Reorder Observation Count =
CALCULATE (
    COUNTROWS ( FactSupplyChain ),
    FactSupplyChain[Reorder Status] = "Reorder Required"
)

Average Lead Time (Days) =
AVERAGE ( FactSupplyChain[Lead Time (Days)] )

Average Delivery Time (Days) =
AVERAGE ( FactSupplyChain[Delivery Time (Days)] )

Average Delivery Delay (Days) =
AVERAGEX (
    FactSupplyChain,
    MAX (
        0,
        FactSupplyChain[Delivery Time (Days)]
            - FactSupplyChain[Lead Time (Days)]
    )
)

On-Time Delivery Observation Count =
CALCULATE (
    COUNTROWS ( FactSupplyChain ),
    FactSupplyChain[Delivery Status (On Time/Delayed)] = "On Time"
)

Delivery Observation Count =
COUNTROWS ( FactSupplyChain )

On-Time Delivery Observation % =
DIVIDE (
    [On-Time Delivery Observation Count],
    [Delivery Observation Count]
)

Total Forecast Demand =
SUM ( FactSupplyChain[Demand Forecast] )

Total Actual Demand =
SUM ( FactSupplyChain[Actual Demand] )

Absolute Forecast Error =
SUMX (
    FactSupplyChain,
    ABS (
        FactSupplyChain[Actual Demand]
            - FactSupplyChain[Demand Forecast]
    )
)

WAPE % =
DIVIDE (
    [Absolute Forecast Error],
    [Total Actual Demand]
)

Inventory Holding Cost (Estimated) =
SUM ( FactSupplyChain[Inventory Holding Cost] )
```

## Interpretation notes
- Format percentage measures as Percentage.
- Delivery counts/rates are observation-level proxies, not unique shipment metrics.
- `Observed Closing Stock Sum` is not current inventory.
- WAPE is undefined when total actual demand is zero.
- Holding-cost currency and period are not confirmed in the sample.
- Formal inventory turnover requires COGS / average inventory value.
