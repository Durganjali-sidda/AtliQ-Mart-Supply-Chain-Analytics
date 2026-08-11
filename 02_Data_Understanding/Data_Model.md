# Data Model

## Modeling Objective

The data model should support analysis of supply-chain
service performance across customers, products, locations,
and time while preserving the different grains of the
transactional tables.

---

## Tables

### Dimension Tables

- dim_customers
- dim_products
- dim_date
- dim_targets_orders

### Fact Tables

- fact_orders_aggregate
- fact_order_lines

---

## Logical Structure

```text
                  dim_date
                     |
                     |
                     v
             fact_orders_aggregate
                     |
                     |
              Customer Analysis
                     |
              dim_customers
                     |
                     |
             dim_targets_orders


              fact_order_lines
                     |
              +------+------+
              |             |
       dim_customers   dim_products


Fact Table Grain
fact_orders_aggregate

Grain:

One row = one order.

Used primarily for order-level OT, IF and OTIF analysis.

fact_order_lines

Grain:

One row = one product line within an order.

Used primarily for product, quantity and detailed delivery
analysis.

Key Relationships
Customer

dim_customers.customer_id

connects to:

fact_orders_aggregate.customer_id
fact_order_lines.customer_id
dim_targets_orders.customer_id
Product

dim_products.product_id

connects to:

fact_order_lines.product_id
Date

dim_date.date

will be evaluated against the relevant date field used for
time-based analysis.

### Important Modeling Consideration

Because fact_orders_aggregate and fact_order_lines have
different grains, they should not be joined directly in a
many-to-many relationship.

Order-level KPIs should be calculated from the order-level
fact table unless there is a specific analytical reason to
derive them from order-line data.

### Modeling Principle

The model should preserve:

One order as one order-level business event.
One product line as one order-line business event.
Customer-specific service targets.
Product-level detail.
Time-based analysis.

The final Power BI model will be validated before KPI
development.