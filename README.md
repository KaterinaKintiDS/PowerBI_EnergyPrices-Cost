# PowerBI_EnergyPrices-Cost
# Energy Market Dashboard (Power BI)

This project analyzes electricity price evolution, electricity demand, and bill composition (taxes & regulated charges) across six European countries using Power BI. The dashboard is designed to answer CEO-style questions around cost competitiveness, volatility/risk, and the drivers behind final consumer bills.

## Files in this repository
- `Energy.pbix` — Power BI report file
- `Energy.pdf` — exported PDF version of the dashboard
- `/data/` — source files (Eurostat electricity prices, consumption, and bill components)
- `/screenshots/` — optional PNG screenshots for quick preview

> Tip: GitHub cannot preview `.pbix` files. The PDF + screenshots help reviewers understand the work quickly.

---

## Business Questions (CEO Focus)
1. Which countries face structurally higher electricity prices?
2. Which years show the strongest price shocks (YoY spikes)?
3. Where is electricity demand concentrated (scale effect)?
4. What drives final electricity bills beyond the energy price (taxes, VAT, network costs)?
5. Which markets appear more predictable vs more exposed to cost risk?

---

## Data Sources
- Electricity prices: Eurostat dataset (downloaded in 2025)
- Electricity demand/consumption: IEA dataset (available through 2022)
- Bill components: taxes/levies categories (VAT, network costs, environmental/nuclear/renewable taxes)

---

## Data Model (Star Schema)
The report uses a star schema:
- Dimensions:
  - `DimCountry`
  - `DimYear`
- Fact tables:
  - `EnergyPrice`
  - `ElectricityConsumption` (demand)
  - Taxes/charges tables (VAT, network costs, environmental taxes, etc.)

Relationships are:
- One-to-many from dimensions to fact tables
- Single-direction filtering
- Active relationships

This structure keeps filtering consistent and avoids ambiguous joins and double counting.

---

## Key Measures (DAX)
### Average Energy Price
Calculates average electricity price in the current filter context (country/year).

### YoY % Energy Price Growth
Compares each year’s average energy price with the previous year to detect shock periods and acceleration in costs.
- Returns blank when the previous year is missing.

### Cost Exposure (Conceptual)
A derived metric combining price and demand:
- `Cost Exposure = Energy Price × Electricity Demand`
Used to illustrate how price and scale jointly shape the financial impact.

---

## Dashboard Pages & Insights

### 1) Electricity Prices Over Time (2017–2024)
Shows price evolution and cross-country differences.
**Key takeaway:** 2022 is a peak year for several markets; Ireland trends higher while Iceland remains low-cost.

### 2) Price Comparison & YoY Growth
Highlights annual acceleration/deceleration of prices using YoY % Growth.
**Key takeaway:** YoY spikes indicate cost shocks and increased procurement/budgeting risk.

### 3) Electricity Consumption (2017–2022)
Shows total demand by country.
**Key takeaway:** Italy dominates total demand; values are country totals (not per capita).

### 4) Estimated Cost Exposure (Price × Demand)
Combines price and demand to estimate relative exposure.
**Key takeaway:** Total exposure is driven strongly by demand scale, not only price level.

### 5) KPI Summary & Extremes
Identifies maximum/minimum exposure and price ranges.
**Key takeaway:** High prices do not automatically mean highest total impact—volume matters.

### 6) 2022 vs 2021 Shock View
Focuses on the crisis jump year.
**Key takeaway:** shock intensity differs across countries, indicating uneven risk.

### 7) Bills Decomposition: Energy vs Taxes
Breaks down bill components beyond energy price.
**Key takeaway:** taxes and regulated costs materially change final bills; some high-price markets apply offsets via lower taxes.

---

## Limitations / Notes
- Consumption is total country demand, not per capita (population and industrial scale affect comparisons).
- Some datasets do not cover the same time span (e.g., demand available only to 2022).
- Taxes are modeled separately from electricity price to isolate market price dynamics from policy/regulatory effects.

---

## How to Open
1. Download `Energy.pbix`
2. Open with Power BI Desktop
3. If prompted, update file paths to the local `/data/` folder

---

## Author
Katerina Kinti
