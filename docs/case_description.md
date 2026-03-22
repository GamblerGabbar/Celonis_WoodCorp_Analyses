# Case Description – WoodCorp O2C Process Mining

## Company

WoodCorp is a manufacturing company producing **pallets and crates**.  It operates
out of six factories in Germany (Essen, Aachen, Bonn, Crefeld, Duisburg, Wuppertal)
and ships to customers in the Retail, Transportation, Construction, and Other markets
across Europe and the United States.

## Dataset

| Table | Rows | Key Fields |
|---|---|---|
| Case table (order level) | 19,953 | CASE_KEY, FACTORY, PRODUCT_TYPE, DELIVERY_COMPANY, WAREHOUSE_TYPE, ORDERED_QUANTITY, DELIVERED_QUANTITY, ORDER_VALUE, DELIVERED_DATE, PROMISED_DATE, CUST_ID, CUST_COUNTRY |
| Activity table (event level) | 210,135 | CASE_KEY, ACTIVITY_EN, EVENTTIME |

## Business Problem

WoodCorp's On-Time Delivery (OTD) rate stands at **64.46 %**, well below the 80 %
industry benchmark.  This results in:

- **€11.8 M per year** in late-delivery penalty costs.
- **€68.6 M** of annual revenue being placed at risk (32.7 % of total revenue).
- **70.9 %** of all customers (219 of 309) affected by at least one late delivery.

## Objective

Use Celonis process mining to:

1. Quantify the financial impact of delivery failures.
2. Identify the root causes of delays (factory, carrier, warehouse, process).
3. Prioritise improvement initiatives that close the OTD gap to 80 %.
4. Calculate the potential annual savings (~€5.2 M) from targeted process improvements.

## Key Dimensions

- **Factories:** Essen (largest, 9,093 orders), Aachen (8,138 orders), Bonn, Crefeld,
  Duisburg, Wuppertal.
- **Products:** Crates (€178 M revenue, 68.8 % OTD) and Pallets (€32 M revenue, 59.7 % OTD).
- **Carriers:** UPS (90 % of orders), DHL, FedEx, DB Schenker.
- **Warehouse types:** Automated (79.6 % OTD) vs. Non-automated (64.4 % OTD).
