# PQL Queries – WoodCorp O2C (Complete Dashboard Query Set)

> **Note:** Queries below are written in SQL-like PQL style and aligned to the case table fields available in this repository.  
> Main table used: `Woodcorp O2C Case table` (order-level).

---

## 1) Global KPI Cards

### Total Orders
```sql
COUNT(CASE_KEY)
```

### Total Revenue
```sql
SUM(ORDER_VALUE)
```

### On-Time Delivery %
```sql
AVG(
  CASE
    WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1
    ELSE 0
  END
)
```

### Late Orders
```sql
SUM(
  CASE
    WHEN DELIVERED_DATE > PROMISED_DATE THEN 1
    ELSE 0
  END
)
```

### Delivered Quantity
```sql
SUM(DELIVERED_QUANTITY)
```

### Late Delivered Quantity
```sql
SUM(
  CASE
    WHEN DELIVERED_DATE > PROMISED_DATE THEN DELIVERED_QUANTITY
    ELSE 0
  END
)
```

### Volume Conformance %
```sql
AVG(
  CASE
    WHEN DELIVERED_QUANTITY BETWEEN ORDERED_QUANTITY + MIN_ORDER_TOLERANCE
                                AND ORDERED_QUANTITY + MAX_ORDER_TOLERANCE
    THEN 1
    ELSE 0
  END
)
```

### Average Delivery Delay (Days)
```sql
AVG(DAYS_BETWEEN(PROMISED_DATE, DELIVERED_DATE))
```

### Average Positive Delay (Late-Only, Days)
```sql
AVG(
  CASE
    WHEN DELIVERED_DATE > PROMISED_DATE
    THEN DAYS_BETWEEN(PROMISED_DATE, DELIVERED_DATE)
    ELSE NULL
  END
)
```

---

## 2) Business Case / Cost KPIs

### Current Late Delivery Cost
```sql
SUM(
  CASE
    WHEN DELIVERED_DATE > PROMISED_DATE THEN DELIVERED_QUANTITY
    ELSE 0
  END
) * 0.75
```

### Expected Penalty Cost at Target OTD = 80%
```sql
(
  SUM(
    CASE
      WHEN DELIVERED_DATE > PROMISED_DATE THEN DELIVERED_QUANTITY
      ELSE 0
    END
  )
  *
  (
    CASE
      WHEN 1 - AVG(CASE WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1 ELSE 0 END) > 0
      THEN (1 - 0.80) / (1 - AVG(CASE WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1 ELSE 0 END))
      ELSE 0
    END
  )
) * 0.75
```

### Potential Savings if OTD = 80%
```sql
(
  SUM(
    CASE
      WHEN DELIVERED_DATE > PROMISED_DATE THEN DELIVERED_QUANTITY
      ELSE 0
    END
  ) * 0.75
)
-
(
  (
    SUM(
      CASE
        WHEN DELIVERED_DATE > PROMISED_DATE THEN DELIVERED_QUANTITY
        ELSE 0
      END
    )
    *
    (
      CASE
        WHEN 1 - AVG(CASE WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1 ELSE 0 END) > 0
        THEN (1 - 0.80) / (1 - AVG(CASE WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1 ELSE 0 END))
        ELSE 0
      END
    )
  ) * 0.75
)
```

### Revenue at Risk (Late Revenue)
```sql
SUM(
  CASE
    WHEN DELIVERED_DATE > PROMISED_DATE THEN ORDER_VALUE
    ELSE 0
  END
)
```

---

## 3) Dimension-Based Visuals

### Product Revenue
**Dimension:** `PRODUCT_TYPE`
```sql
SUM(ORDER_VALUE)
```

### Revenue by Delivery Company
**Dimension:** `DELIVERY_COMPANY`
```sql
SUM(ORDER_VALUE)
```

### Revenue by Factory
**Dimension:** `FACTORY`
```sql
SUM(ORDER_VALUE)
```

### Revenue by Country / Region Map
**Dimension:** `CUST_COUNTRY`
```sql
SUM(ORDER_VALUE)
```

### Top Customers by Revenue
**Dimension:** `CUST_NAME` (Top-N sort by revenue desc)
```sql
SUM(ORDER_VALUE)
```

### Distribution of Customers by Region
**Dimension:** `CUST_COUNTRY`
```sql
COUNT_DISTINCT(CUST_ID)
```

### Customer Market Served by Factory
**Dimensions:** `FACTORY`, `CUST_MARKET`
```sql
COUNT(CASE_KEY)
```

### Product Type Distribution per Factory
**Dimensions:** `FACTORY`, `PRODUCT_TYPE`
```sql
COUNT(CASE_KEY)
```

### Warehouse Type Count by Factory
**Dimensions:** `FACTORY`, `WAREHOUSE_TYPE`
```sql
COUNT(CASE_KEY)
```

---

## 4) OTD and Volume Conformance Breakdowns

### On-Time Delivery % by Product Type
**Dimension:** `PRODUCT_TYPE`
```sql
AVG(
  CASE
    WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1
    ELSE 0
  END
)
```

### On-Time Delivery % by Delivery Company
**Dimension:** `DELIVERY_COMPANY`
```sql
AVG(
  CASE
    WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1
    ELSE 0
  END
)
```

### On-Time Delivery % by Factory
**Dimension:** `FACTORY`
```sql
AVG(
  CASE
    WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1
    ELSE 0
  END
)
```

### OTD % by Warehouse Type
**Dimension:** `WAREHOUSE_TYPE`
```sql
AVG(
  CASE
    WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1
    ELSE 0
  END
)
```

### OTD % for Automated Warehouse
```sql
AVG(
  CASE
    WHEN WAREHOUSE_TYPE = 'Automated' AND DELIVERED_DATE <= PROMISED_DATE THEN 1
    WHEN WAREHOUSE_TYPE = 'Automated' THEN 0
    ELSE NULL
  END
)
```

### Late % for Automated Warehouse
```sql
AVG(
  CASE
    WHEN WAREHOUSE_TYPE = 'Automated' AND DELIVERED_DATE > PROMISED_DATE THEN 1
    WHEN WAREHOUSE_TYPE = 'Automated' THEN 0
    ELSE NULL
  END
)
```

### OTD % for Non-Automated Warehouse
```sql
AVG(
  CASE
    WHEN WAREHOUSE_TYPE = 'Non-automated' AND DELIVERED_DATE <= PROMISED_DATE THEN 1
    WHEN WAREHOUSE_TYPE = 'Non-automated' THEN 0
    ELSE NULL
  END
)
```

### Late % for Non-Automated Warehouse
```sql
AVG(
  CASE
    WHEN WAREHOUSE_TYPE = 'Non-automated' AND DELIVERED_DATE > PROMISED_DATE THEN 1
    WHEN WAREHOUSE_TYPE = 'Non-automated' THEN 0
    ELSE NULL
  END
)
```

### Volume Conformance by Product Type
**Dimension:** `PRODUCT_TYPE`
```sql
AVG(
  CASE
    WHEN DELIVERED_QUANTITY BETWEEN ORDERED_QUANTITY + MIN_ORDER_TOLERANCE
                                AND ORDERED_QUANTITY + MAX_ORDER_TOLERANCE
    THEN 1
    ELSE 0
  END
)
```

### Volume Conformance by Factory
**Dimension:** `FACTORY`
```sql
AVG(
  CASE
    WHEN DELIVERED_QUANTITY BETWEEN ORDERED_QUANTITY + MIN_ORDER_TOLERANCE
                                AND ORDERED_QUANTITY + MAX_ORDER_TOLERANCE
    THEN 1
    ELSE 0
  END
)
```

---

## 5) Late Quantity / Delay Distributions

### Late Delivery Quantity by Delivery Company
**Dimension:** `DELIVERY_COMPANY`
```sql
SUM(
  CASE
    WHEN DELIVERED_DATE > PROMISED_DATE THEN DELIVERED_QUANTITY
    ELSE 0
  END
)
```

### Delivery Delay Distribution (Histogram)
**Dimension:** `DAYS_TO_DEL_DEADLINE` (bucketed)
```sql
COUNT(CASE_KEY)
```

### Delay in Days by Product Type
**Dimension:** `PRODUCT_TYPE`
```sql
AVG(DAYS_BETWEEN(PROMISED_DATE, DELIVERED_DATE))
```

---

## 6) Matrix and Table Widgets

### Product × Delivery Company (OTD)
**Dimensions:** `PRODUCT_TYPE`, `DELIVERY_COMPANY`
```sql
AVG(
  CASE
    WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1
    ELSE 0
  END
)
```

### Product × Delivery Contractor Matrix – Revenue
**Dimensions:** `DELIVERY_COMPANY`, `PRODUCT_TYPE`
```sql
SUM(ORDER_VALUE)
```

### Product × Delivery Contractor Matrix – OTD %
**Dimensions:** `DELIVERY_COMPANY`, `PRODUCT_TYPE`
```sql
AVG(
  CASE
    WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1
    ELSE 0
  END
)
```

### Factory Performance Table – Orders
**Dimension:** `FACTORY`
```sql
COUNT(CASE_KEY)
```

### Factory Performance Table – On-Time %
**Dimension:** `FACTORY`
```sql
AVG(
  CASE
    WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1
    ELSE 0
  END
)
```

### Factory Performance Table – Volume Conformance %
**Dimension:** `FACTORY`
```sql
AVG(
  CASE
    WHEN DELIVERED_QUANTITY BETWEEN ORDERED_QUANTITY + MIN_ORDER_TOLERANCE
                                AND ORDERED_QUANTITY + MAX_ORDER_TOLERANCE
    THEN 1
    ELSE 0
  END
)
```

### Factory Performance Table – Avg Delay
**Dimension:** `FACTORY`
```sql
AVG(DAYS_BETWEEN(PROMISED_DATE, DELIVERED_DATE))
```

---

## 7) Customer Risk Widgets

### Customers Affected by Delays
```sql
COUNT_DISTINCT(
  CASE
    WHEN DELIVERED_DATE > PROMISED_DATE THEN CUST_ID
    ELSE NULL
  END
)
```

### Customer Risk % (Delayed Customers / Total Customers)
```sql
COUNT_DISTINCT(
  CASE
    WHEN DELIVERED_DATE > PROMISED_DATE THEN CUST_ID
    ELSE NULL
  END
)
/
COUNT_DISTINCT(CUST_ID)
```

### Customer-Level OTD %
**Dimension:** `CUST_NAME` (or `CUST_ID`)
```sql
AVG(
  CASE
    WHEN DELIVERED_DATE <= PROMISED_DATE THEN 1
    ELSE 0
  END
)
```

### Customer-Level Average Order Value
**Dimension:** `CUST_NAME` (or `CUST_ID`)
```sql
SUM(ORDER_VALUE) / COUNT(CASE_KEY)
```
