# Order-Tracker-and-Delay-analysis
Order tracker and delay analysis in Excel: KPIs, pivot tables and a dashboard

# Order Tracker & Delay Analysis

An Excel project that tracks project orders, flags delivery risks and analyses the causes of delay, built to support the daily follow-up work of an order or customer coordinator.

> **Note:** The dataset is **simulated** for portfolio purposes. It is not real company data.

---

## Business Problem

Project orders pass through Sales, Production, Supply Chain, Dispatch and Warehouse teams. When delivery dates slip, nobody sees it until the customer complains. This project answers four questions:

1. Which open orders are already overdue and need escalation?
2. Which orders have had no progress for several days?
3. How often are delivery commitments changed?
4. What causes delays most often, and where?

## Dataset

- **60 orders**, 14 input columns (Order ID, Customer, Product, Plant, Region, Qty, Order Date, Committed Date, Revised Date, Status, Owner, Last Updated, Actual Delivery Date, Delay Cause)
- 6 plants, 5 product types, 4 owners, 6 order statuses
- Data was cleaned before analysis: date formats, blanks, duplicates, inconsistent text and logical checks (for example, delivered orders must have a delivery date)
- **Report date used:** 19 Nov 2026 (fixed, so results are reproducible)

## Method

**Calculated columns**

| Column | Logic |
|---|---|
| Current Promise Date | Revised Date if present, otherwise Committed Date |
| Date Changed? | Yes if a Revised Date exists |
| Date Pushed | Revised Date minus Committed Date (days) |
| Overdue? | Not delivered **and** report date is after the Current Promise Date |
| Stagnant? | Not delivered **and** no update for 7 or more days |
| On-Time? | Delivered on or before the Current Promise Date |

**KPIs:** open orders, on-time delivery %, overdue orders, stagnant orders, orders with a revised date

**Pivot analysis:** orders by status, delay cause, plant and owner

**Tools:** Microsoft Excel (Tables, `IF`, `AND`, `COUNTIF`, `COUNTIFS`, `INDEX/MATCH`, Pivot Tables, Charts, Conditional Formatting)

## Key Findings (as of 19 Nov 2026)

- **58% on-time delivery:** 19 of 33 delivered orders arrived on time. Late orders were late by 3.8 days on average (maximum 9 days).
- **7 of 27 open orders are overdue.** Three of them are marked *Ready for Dispatch*, which points to a dispatch and warehouse bottleneck rather than a production problem.
- **Stock Shortage caused the most late days** among delivered orders (19 days), followed by Warehouse (14) and Dispatch (11).
- **Chennai had 0% on-time delivery** (4 orders). Kandla (43%) and Hoshiarpur (55%) also lagged.
- **MDF Boards had the lowest on-time rate (22%)** across 9 delivered orders.
- **37% of orders (22 of 60) had their delivery date revised**, by 8.8 days on average.

*Plant-level results are based on small samples (2 to 11 delivered orders per plant), so they indicate where to look rather than prove a cause.*

## Recommended Actions

- Escalate overdue *Ready for Dispatch* orders to Dispatch and Warehouse teams.
- Review stock planning at plants with repeated stock-related delays.
- Investigate recurring delays for MDF Boards and at Chennai.
- Review why delivery commitments are changed so often and set more realistic dates.

## Repository Contents

```
├── README.md
├── Order_Tracker_Delay_Analysis.xlsx   # Orders, KPIs, pivots, dashboard
├── data/
│   └── orders_sample_data.csv          # Raw simulated data
└── images/
    └── dashboard.png                   # Dashboard screenshot
```

## How to Use

1. Open the Excel file and go to the **Order data** sheet.
2. Change the report date in the Overdue? and Stagnant? formulas (or replace it with `TODAY()` for live use).
3. Refresh the pivot tables (Data > Refresh All) to update the Dashboard.

## Limitations and Next Steps

- Simulated data and a small sample size.
- Planned: a stock-availability check to flag shortages before they delay orders, and a Power BI version of the dashboard.

## Author

**Srijita Kayal**
MBA in Business Analytics & Data Science
[LinkedIn](https://www.linkedin.com/in/srijita-kayal-data-analytic-business-analytic) | [Portfolio](https://srijita205.github.io)
