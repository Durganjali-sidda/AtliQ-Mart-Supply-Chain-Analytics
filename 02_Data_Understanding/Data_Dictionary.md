# Data Dictionary

## Dataset Overview

The AtliQ Mart Supply Chain Analytics dataset contains
customer, product, date, customer service targets, order-level,
and order-line-level information.

The dataset consists of six analytical tables:

1. dim_customers
2. dim_products
3. dim_date
4. dim_targets_orders
5. fact_orders_aggregate
6. fact_order_lines

---

## 1. dim_customers

### Purpose

Contains master information about AtliQ Mart's business
customers.

### Grain

One row represents one customer record.

### Columns

| Column | Description | Business Usage |
|---|---|---|
| customer_id | Unique customer identifier | Customer analysis and joins |
| customer_name | Name of the business customer | Customer reporting |
| city | Customer operating city | Geographic analysis |

### Business Questions

- Which customers have poor service levels?
- Which cities contain the affected customers?
- Which customers require intervention?

---

## 2. dim_products

### Purpose

Contains the product master information.

### Grain

One row represents one product/SKU.

### Columns

| Column | Description | Business Usage |
|---|---|---|
| product_id | Unique product identifier | Product joins |
| product_name | Product name | Product analysis |
| category | Product category | Category analysis |

### Business Questions

- Which products have poor service performance?
- Which products contribute to incomplete deliveries?
- Are problems concentrated in particular categories?

---

## 3. dim_date

### Purpose

Provides calendar information for time-based analysis.

### Grain

One row represents one calendar date.

### Columns

| Column | Description | Business Usage |
|---|---|---|
| date | Calendar date | Time relationship |
| mmm_yy | Month-year label | Monthly analysis |
| week_no | Week number | Weekly analysis |

### Business Questions

- Is service performance improving?
- Is performance deteriorating?
- Which periods experienced poor service levels?

---

## 4. dim_targets_orders

### Purpose

Contains customer-specific service-level targets.

### Grain

One row represents the service-level targets associated
with a customer.

### Columns

| Column | Description | Business Usage |
|---|---|---|
| customer_id | Customer identifier | Customer relationship |
| ontime_target | Target On-Time delivery percentage | OT target comparison |
| infull_target | Target In-Full delivery percentage | IF target comparison |
| otif_target | Target OTIF percentage | OTIF target comparison |

### Business Importance

Targets allow actual performance to be evaluated against
the service level expected by each customer.

---

## 5. fact_orders_aggregate

### Purpose

Contains order-level delivery performance.

### Grain

One row represents one customer order.

### Columns

| Column | Description | Business Usage |
|---|---|---|
| order_id | Unique order identifier | Order analysis |
| customer_id | Customer placing the order | Customer analysis |
| order_placement_date | Date order was placed | Time analysis |
| on_time | Indicates whether the order was delivered on time | OT KPI |
| in_full | Indicates whether the complete order was delivered | IF KPI |
| otif | Indicates whether the order was both on time and in full | OTIF KPI |

### Business Questions

- What percentage of orders are on time?
- What percentage are delivered in full?
- What percentage are OTIF?
- Which customers have the lowest service levels?

---

## 6. fact_order_lines

### Purpose

Provides product-level details for individual customer
orders.

### Grain

One row represents one product line within an order.

### Columns

| Column | Description | Business Usage |
|---|---|---|
| order_id | Order identifier | Order relationship |
| order_placement_date | Order placement date | Time analysis |
| customer_id | Customer identifier | Customer analysis |
| product_id | Product identifier | Product analysis |
| order_qty | Quantity ordered | Demand/quantity analysis |
| agreed_delivery_date | Promised delivery date | Delivery performance |
| actual_delivery_date | Actual delivery date | Delivery performance |
| delivery_qty | Quantity actually delivered | Fill analysis |
| In Full | Indicates whether ordered quantity was delivered | IF analysis |
| On Time | Indicates whether delivery met agreed date | OT analysis |
| On Time In Full | Indicates both OT and IF conditions were met | OTIF analysis |

---

## Fact Table Relationship

The dataset contains two different levels of transactional
detail:

### fact_orders_aggregate

Order level.

### fact_order_lines

Order-line level.

These tables must not be directly joined in a way that
duplicates order-level records.

The different grains must be respected during analysis.

---

## Core Analytical Metrics

### On-Time Delivery %

Percentage of orders delivered on or before the agreed
delivery date.

### In-Full Delivery %

Percentage of orders where the complete ordered quantity
was delivered.

### OTIF %

Percentage of orders delivered both on time and in full.

### Target Gap

Actual performance minus the applicable customer target.

Example:

Actual OTIF = 72%

Target OTIF = 80%

OTIF Gap = -8 percentage points.