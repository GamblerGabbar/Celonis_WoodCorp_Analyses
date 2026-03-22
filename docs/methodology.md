# Methodology – WoodCorp O2C Process Mining Analysis

## Step 1: Data Integration

- Upload the **Case table** (order-level, 19,953 rows) and **Activity table**
  (event-level, 210,135 rows) into Celonis EMS.
- Join on `CASE_KEY` to link each event to its parent order.

## Step 2: Data Modelling

- Set `CASE_KEY` as the Case ID, `ACTIVITY_EN` as the Activity, and `EVENTTIME`
  as the Timestamp.
- Enrich the case table with calculated columns:
  - `IS_LATE`: `DELIVERED_DATE > PROMISED_DATE`
  - `DELAY_DAYS`: `DAYS_BETWEEN(PROMISED_DATE, DELIVERED_DATE)`
  - `LATE_QTY`: `DELIVERED_QUANTITY` where `IS_LATE = true`, else 0
  - `VOLUME_CONFORMANCE`: 1 if `DELIVERED_QUANTITY` is within
    `[ORDERED_QUANTITY + MIN_ORDER_TOLERANCE, ORDERED_QUANTITY + MAX_ORDER_TOLERANCE]`

## Step 3: KPI Dashboard Creation

Build dashboard views covering:

- **Business Case** – current penalty cost, savings potential, revenue at risk
- **Sales & Orders** – total revenue, order volume, average order value by customer/country
- **Customer Analyses** – OTD %, late %, revenue, churn risk by customer and market
- **Factory Analyses** – OTD %, volume conformance, average delay by factory and warehouse type

All PQL queries are documented in `analysis/pql_queries.md`.

## Step 4: Root Cause Identification

- Identify high-frequency rework activities in the process flow:
  - **Change production start date** (23,693 occurrences) → production instability
  - **Change delivery date** (13,661 occurrences) → reactive date management
  - **Credit order block** (2,006 occurrences) → order flow interruption
  - **Change quantity** (19,525 occurrences) → demand uncertainty
- Segment OTD performance by factory, carrier, warehouse type, and product type to
  locate root-cause dimensions.

## Step 5: Business Case Quantification

Using a penalty rate of **€0.75 per kg** of late-delivered product:

| State | Late Qty (kg) | Penalty Cost | OTD % |
|---|---|---|---|
| Current | 15,766,358 | €11,824,769 | 64.46 % |
| Target (OTD 80 %) | 8,873,517 | €6,655,138 | 80.00 % |
| **Savings** | | **€5,169,631** | |

Revenue at risk from late orders: **€68,619,901** (32.7 % of €210 M total revenue).

Full calculations and dimensional breakdowns are in `analysis/business_case_calculations.md`.

## Step 6: Recommendations & Business Impact

Prioritised improvement levers:

1. **Stabilise production scheduling** at Essen and Aachen to reduce 23,693 start-date
   changes – directly reduces late deliveries at the two highest-revenue factories.
2. **Replace or renegotiate** FedEx (48.3 % OTD) and DB Schenker (6.2 % OTD) carrier
   contracts; redirect volume to DHL (75.5 % OTD).
3. **Target Aachen** for an OTD improvement programme (61.4 % OTD, worst major factory).
4. **Pilot warehouse automation** at high-volume non-automated sites (automated sites
   achieve 79.6 % OTD vs. 64.4 % for non-automated).
5. **Stabilise order quantities** to reduce the 97.9 % change-quantity rework rate and
   improve the 49.35 % volume conformance.
6. **Assign key account managers** to Götz (48.1 % late), Becker (46.8 % late), and
   Meißner GmbH (55.4 % late) to protect high-revenue relationships.
