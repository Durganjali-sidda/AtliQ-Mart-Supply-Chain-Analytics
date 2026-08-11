# Data Limitations

## Purpose

This document identifies information that is not available
in the current dataset and explains how those gaps affect
the business analysis.

The objective is to avoid making unsupported claims and to
identify what additional data AtliQ Mart would need for
deeper root-cause and customer-retention analysis.

---

# 1. No Contract Renewal Outcome

The dataset does not contain:

- Contract start date
- Contract end date
- Contract value
- Renewal status
- Cancellation status
- Customer churn status

### Impact

We cannot directly prove that a customer failed to renew
because of poor OTIF performance.

We can identify customers with persistent service-level
problems and classify them as potential intervention
priorities.

### Additional Data Required

A customer contract/renewal table containing:

- customer_id
- contract_start_date
- contract_end_date
- contract_value
- renewal_status
- cancellation_reason

---

# 2. No Customer Revenue or Profitability

The current data focuses primarily on orders and quantities.

It does not provide a reliable customer-level measure of:

- Revenue
- Gross margin
- Profit
- Customer lifetime value
- Contract value

### Impact

We cannot accurately rank customers by financial value.

Therefore, customer prioritization will primarily use the
service-performance and order-level information available in
the dataset.

### Additional Data Required

Customer financial data containing:

- Revenue
- Margin
- Contract value
- Profitability
- Customer lifetime value

---

# 3. No Inventory Data

The dataset does not contain:

- Opening inventory
- Closing inventory
- Stock availability
- Stock-outs
- Safety stock
- Reorder point

### Impact

If an order is delivered partially, we can observe the
incomplete delivery but cannot determine whether inventory
shortage was the underlying cause.

### Additional Data Required

Inventory snapshot data by:

- Product
- Location
- Date

---

# 4. No Warehouse Information

The dataset does not identify the warehouse or distribution
center responsible for fulfilling each order.

### Impact

We cannot determine whether a particular warehouse is
responsible for poor service performance.

### Additional Data Required

Warehouse/order fulfillment mapping:

- order_id
- warehouse_id
- dispatch_date
- warehouse_location

---

# 5. No Supplier Information

There is no supplier-level information.

### Impact

If a product is frequently incomplete, we cannot determine
whether supplier performance contributed to the shortage.

### Additional Data Required

Supplier information such as:

- supplier_id
- product_id
- purchase order
- supplier lead time
- supplier fulfillment rate
- supplier delays

---

# 6. No Transportation / Logistics Data

The dataset does not identify:

- Logistics provider
- Vehicle
- Dispatch time
- Transit time
- Route
- Delivery attempt
- Transportation delay reason

### Impact

We can identify late deliveries but cannot determine the
specific transportation cause.

### Additional Data Required

Transportation event data containing:

- order_id
- logistics_partner
- dispatch_date
- expected_arrival
- actual_arrival
- delay_reason

---

# 7. No Delay Reason

The dataset tells us whether an order was late, but not why.

Possible real-world reasons could include:

- Inventory shortage
- Production delay
- Warehouse delay
- Transportation delay
- Route disruption
- Demand spike
- Customer-side receiving issue

However, these cannot be identified directly from the
current dataset.

### Analytical Treatment

These will be treated as hypotheses rather than confirmed
root causes unless supporting data becomes available.

---

# 8. No In-Full Failure Reason

The data contains ordered and delivered quantities, but it
does not identify the reason for quantity shortages.

### Impact

We can identify products associated with incomplete
deliveries but cannot definitively identify the cause.

---

# 9. Limited Geographic Information

Customer location is available at the city level.

However, the dataset does not contain:

- Warehouse location
- Delivery route
- Customer coordinates
- Distribution center
- Distance
- Travel time

### Impact

Geographic analysis can be performed at customer/city level,
but detailed logistics optimization is outside the scope of
the current dataset.

---

# 10. No Cost Data

The dataset does not provide:

- Transportation cost
- Inventory holding cost
- Stock-out cost
- Penalty cost
- Expedited shipping cost
- Cost of lost sales

### Impact

We cannot calculate the financial cost of poor service
directly.

Recommendations will therefore focus on operational
prioritization rather than precise financial ROI unless
additional financial data is provided.

---

# 11. No Customer Satisfaction Data

There is no:

- Customer satisfaction score
- NPS
- Customer complaint data
- Service ticket information
- Customer feedback

### Impact

The analysis cannot directly measure customer satisfaction.

Service-level performance can instead be used as an
operational indicator of potential customer experience risk.

---

# 12. No Causal Relationship Between OTIF and Churn

The business problem suggests that poor service may have
contributed to contract non-renewal.

However, without contract renewal and customer feedback data,
this relationship cannot be statistically or causally
established.

Therefore:

> Poor OTIF = observed operational problem.

But:

> Poor OTIF caused contract cancellation = unproven hypothesis.

This distinction will be maintained throughout the project.

---

# Overall Data Limitation

The current dataset is strong enough to answer:

- What is the service-level performance?
- Which customers are underperforming?
- Which products have poor fulfillment?
- Which cities have service-level gaps?
- How does performance change over time?
- Where are the largest service-level exceptions?

However, it is not sufficient to fully answer:

> Why did the operational failure happen?

or:

> Did the operational failure cause the customer to leave?

---

# Recommended Data Expansion

For a production-level supply-chain analytics solution,
AtliQ Mart should integrate:

1. Contract & renewal data
2. Customer revenue/profitability
3. Inventory data
4. Warehouse data
5. Supplier data
6. Transportation data
7. Delay reason codes
8. Customer complaints
9. Logistics cost
10. Production data

This would enable deeper root-cause analysis and more accurate
business-impact measurement.