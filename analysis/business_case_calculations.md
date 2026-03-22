# Business Case Calculations – WoodCorp O2C (In-Depth)

> All figures are derived directly from the **Woodcorp O2C Case table** (19,953 orders)
> and the **Woodcorp O2C Activity table** (210,135 events).

---

## 1. Business Problem

WoodCorp is a manufacturer of pallets and crates that ships orders via third-party
logistics partners to customers in the Retail, Transportation, Construction, and Other
markets.  Analysis of the Order-to-Cash (O2C) process reveals a systemic on-time
delivery (OTD) failure affecting **35.54 %** of all orders, generating a measurable
financial penalty and placing a large share of annual revenue at risk.

---

## 2. Portfolio Overview

| KPI | Value |
|---|---|
| Total Orders | 19,953 |
| Total Revenue | €210,099,684 |
| Total Ordered Quantity | 47,874,284 kg |
| Total Delivered Quantity | 47,740,004 kg |
| Unique Customers | 309 |
| Activity Events Recorded | 210,135 |

---

## 3. Delivery Performance KPIs

| KPI | Value |
|---|---|
| On-Time Deliveries | 12,862 (64.46 %) |
| Late Deliveries | 7,091 (35.54 %) |
| Volume Conformance % | 49.35 % |
| Average Delivery Delay (all orders) | +0.27 days |
| Average Delay (late orders only) | +4.67 days |
| Customers Affected by at Least One Late Delivery | 219 / 309 (70.9 %) |

**Interpretation:** Nearly two-thirds of WoodCorp's customer base has experienced at
least one late delivery, creating widespread churn and satisfaction risk.

---

## 4. Cost-of-Delay Business Case

### 4.1 Penalty Rate Assumption

A penalty of **€0.75 per kg** of late-delivered product is applied, consistent with
standard contractual late-delivery clauses in the industry.

### 4.2 Current State

| Metric | Calculation | Result |
|---|---|---|
| Late Delivered Quantity | measured from data | 15,766,358 kg |
| Current Late-Delivery Penalty | 15,766,358 × €0.75 | **€11,824,769** |
| Revenue at Risk (late orders) | SUM(ORDER_VALUE) where late | **€68,619,901** |
| Revenue at Risk as % of Total | 68,619,901 / 210,099,684 | **32.7 %** |

### 4.3 Target State – OTD = 80 %

| Metric | Calculation | Result |
|---|---|---|
| Current Late Rate | 1 − 0.6446 | 35.54 % |
| Target Late Rate | 1 − 0.80 | 20.00 % |
| Scale Factor (late qty reduction) | 0.2000 / 0.3554 | 0.5628 |
| Expected Late Qty @ OTD 80 % | 15,766,358 × 0.5628 | 8,873,517 kg |
| Expected Penalty @ OTD 80 % | 8,873,517 × €0.75 | **€6,655,138** |

### 4.4 Potential Annual Savings

| Scenario | Penalty Cost | Savings vs. Current |
|---|---|---|
| Current State (OTD 64.46 %) | €11,824,769 | — |
| Target State (OTD 80 %) | €6,655,138 | **€5,169,631** |

> **Achieving an OTD rate of 80 % would save WoodCorp approximately €5.2 M per year
> in penalty costs alone**, and would reduce revenue at risk by ~€30 M.

---

## 5. Factory Performance Analysis

| Factory | Orders | Revenue (€) | OTD % | Avg Delay (days) | Vol. Conf. % |
|---|---|---|---|---|---|
| Essen | 9,093 | 111,795,290 | 65.6 % | −0.3 | 36.8 % |
| Aachen | 8,138 | 85,432,721 | 61.4 % | +0.8 | 60.4 % |
| Bonn | 1,166 | 8,408,160 | 69.0 % | +0.4 | 38.8 % |
| Crefeld | 1,415 | 3,440,940 | 70.1 % | +0.4 | 72.2 % |
| Duisburg | 133 | 828,370 | 69.2 % | +0.9 | 85.0 % |
| Wuppertal | 8 | 194,204 | 87.5 % | −3.9 | 0.0 % |

**Key findings:**
- **Essen and Aachen** account for **87 % of total orders** and **93 % of revenue** yet
  are the worst OTD performers (65.6 % and 61.4 % respectively), making them the
  primary targets for improvement.
- **Aachen** has the worst OTD (61.4 %) and a positive average delay (+0.8 days),
  indicating structural production or loading issues.
- **Duisburg** achieves the best volume conformance (85.0 %) among significant factories.

---

## 6. Product Type Analysis

| Product Type | Orders | Revenue (€) | OTD % | Avg Delay (days) |
|---|---|---|---|---|
| Crates | 10,419 | 178,133,305 | 68.8 % | −0.6 |
| Pallets | 9,534 | 31,966,379 | 59.7 % | +1.2 |

**Key findings:**
- **Crates** generate **84.8 % of total revenue** and have a relatively better OTD
  (68.8 %) with orders arriving slightly early on average.
- **Pallets** underperform with only 59.7 % OTD and a +1.2-day average delay,
  representing the highest urgency improvement target by product line.

---

## 7. Delivery Company Analysis

| Carrier | Orders | Revenue (€) | OTD % | Late Qty (kg) |
|---|---|---|---|---|
| UPS | 17,956 | 180,454,245 | 64.4 % | 13,605,519 |
| DHL | 1,259 | 19,300,716 | 75.5 % | 1,060,523 |
| FedEx | 722 | 9,707,348 | 48.3 % | 884,722 |
| DB Schenker | 16 | 637,375 | 6.2 % | 215,594 |

**Key findings:**
- **UPS** handles 90 % of orders; its 64.4 % OTD drives the bulk of the penalty cost.
  Even a modest improvement in UPS performance would yield most of the €5.2 M saving.
- **FedEx** has the worst OTD of the major carriers (48.3 %), making it a high-risk
  partner for time-sensitive shipments.
- **DB Schenker** shows a critically low OTD of 6.2 % across its 16 orders and should
  be reviewed or replaced for any new business.
- **DHL** is the best performing carrier at 75.5 % and could be considered for
  additional volume as an incentive-aligned partner.

---

## 8. Warehouse Type Analysis

| Warehouse Type | Orders | OTD % | Late % |
|---|---|---|---|
| Automated | 49 | 79.6 % | 20.4 % |
| Non-automated | 19,904 | 64.4 % | 35.6 % |

**Key findings:**
- Automated warehouses achieve an OTD rate of **79.6 %**, nearly at the 80 % target,
  versus only **64.4 %** for non-automated warehouses.
- Non-automated warehouses account for 99.8 % of orders; warehouse automation is
  therefore a high-impact, long-term investment lever.

---

## 9. Customer Market Analysis

| Market | Orders | Revenue (€) | Late % |
|---|---|---|---|
| Retail | 11,924 | 94,607,006 | 35.2 % |
| Transportation | 6,092 | 88,510,224 | 33.2 % |
| Construction | 1,683 | 23,547,017 | 44.0 % |
| Other | 254 | 3,435,437 | 53.1 % |

**Key findings:**
- **Construction** customers experience the highest late rate (44 %) among primary
  markets.  Construction projects are time-critical; late deliveries carry high
  knock-on costs and contract penalty exposure for WoodCorp customers.
- **Transportation** customers represent the second-largest revenue segment (€88.5 M)
  with a comparatively better 33.2 % late rate, suggesting more resilient supply chains.

---

## 10. Top Customer Risk Analysis

| Customer | Orders | Revenue (€) | Late % |
|---|---|---|---|
| Brand AG | 1,458 | 19,543,673 | 33.5 % |
| Götz | 765 | 16,957,266 | 48.1 % |
| Jürgens | 1,004 | 12,371,111 | 31.7 % |
| Wiegand | 647 | 11,124,956 | 22.3 % |
| Becker | 4,207 | 7,801,916 | 46.8 % |
| Schweizer | 156 | 7,696,408 | 38.5 % |
| Pietsch AG | 1,227 | 6,684,244 | 33.5 % |
| Voigt | 219 | 6,347,358 | 29.2 % |
| Fritz | 394 | 5,027,188 | 8.9 % |
| Adam KG | 639 | 4,841,755 | 22.8 % |
| Meißner GmbH & Co. KGaA | 498 | 4,369,473 | 55.4 % |
| Straub | 731 | 4,337,476 | 32.8 % |

**Key findings:**
- The **top 12 customers by revenue** collectively represent **~€105 M** in annual
  revenue.  Late delivery rates for these accounts range from 8.9 % (Fritz) to
  55.4 % (Meißner GmbH).
- **Götz** (€17 M revenue, 48.1 % late) and **Becker** (€7.8 M, 46.8 % late) are
  high-revenue, high-risk accounts where churn would materially impact WoodCorp finances.

---

## 11. Process-Level Analysis (Activity Table)

| Activity | Occurrences | Coverage |
|---|---|---|
| Order received | 19,953 | 100 % |
| Start production | 19,953 | 100 % |
| Finished production | 19,953 | 100 % |
| Load shipment | 19,953 | 100 % |
| Goods delivered | 19,953 | 100 % |
| Confirm sale | 19,931 | 99.9 % |
| Check Credit Score | 19,931 | 99.9 % |
| Change quantity | 19,525 | 97.9 % |
| Change production start date | 23,693 | 118.7 %* |
| Change delivery date | 13,661 | 68.5 % |
| Change price | 11,623 | 58.2 % |
| Credit order block | 2,006 | 10.1 % |

*Multiple change events per order are possible.

**Key findings:**
- **"Change production start date"** (23,693 events, >1 per order on average) is the
  highest-frequency rework activity, indicating widespread instability in production
  scheduling – a root cause of delivery delays.
- **"Change delivery date"** occurs in 68.5 % of orders, confirming that promised dates
  are routinely renegotiated, which masks true OTD performance and erodes customer trust.
- **"Credit order block"** affects 10.1 % of orders, creating process interruptions that
  can cascade into delivery delays.
- **"Change quantity"** affects 97.9 % of orders, suggesting that initial order
  quantities are almost never stable, driving the low volume conformance rate of 49.35 %.

---

## 12. Geographic Revenue Distribution (Top 5 Countries)

| Country | Orders | Revenue (€) |
|---|---|---|
| Germany (DE) | 12,410 | 107,178,742 |
| Spain (ES) | 1,496 | 20,085,190 |
| France (FR) | 1,207 | 14,742,865 |
| United States (US) | 272 | 9,422,171 |
| Netherlands (NL) | 939 | 8,855,373 |

**Germany** is by far the largest market (51 % of revenue), followed by Spain and France.
International shipments (ES, FR, US, NL, and others) collectively represent €102 M
(49 % of revenue) and may face longer logistics chains that compound delay risks.

---

## 13. Summary – Prioritised Improvement Roadmap

| Priority | Lever | Expected Impact |
|---|---|---|
| 1 | Fix production scheduling instability at **Essen** and **Aachen** (Change production start date events) | Largest OTD gain; reduces the 23,693 rescheduling events |
| 2 | Review **FedEx** and **DB Schenker** contracts or replace with DHL for high-value routes | Eliminate 48.3 % and 6.2 % OTD drag |
| 3 | Target **Aachen factory** for OTD improvement programme (61.4 % OTD, worst of major factories) | Direct reduction in the €5.2 M penalty pool |
| 4 | Pilot warehouse automation at top-volume non-automated sites | Automated warehouses achieve ~80 % OTD vs. 64.4 % for manual |
| 5 | Stabilise order quantities to reduce "Change quantity" events and improve 49.35 % volume conformance | Reduces rework and delivery variance |
| 6 | Assign dedicated account managers to **Götz**, **Becker**, and **Meißner** (high revenue, high late rate) | Protect €30 M+ in high-risk revenue |

---

## 14. Financial Summary

| Metric | Value |
|---|---|
| Total Annual Revenue | €210,099,684 |
| Current Late-Delivery Penalty (annual) | **€11,824,769** |
| Revenue at Risk (late orders) | **€68,619,901** (32.7 % of revenue) |
| Potential Annual Savings at OTD 80 % | **€5,169,631** |
| Revenue Risk Reduction at OTD 80 % | **~€30,002,700** |
| Penalty Cost per Late kg | €0.75 |
| Late Kg as % of Total Delivered | 33.0 % |
