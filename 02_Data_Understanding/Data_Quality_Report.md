
---

# 3. `Data_Quality_Report.md`

This one documents what we checked rather than pretending the data is perfect.

```markdown
# Data Quality Report

## Objective

Validate the structural and business quality of the six
source tables before analytical modeling.

---

## Validation Areas

The following checks are required:

- Row counts
- Duplicate records
- Missing values
- Primary keys
- Foreign keys
- Data types
- Invalid dates
- Invalid quantities
- Referential integrity
- OT/IF/OTIF consistency

---

## Initial Data Observations

The dataset contains:

- Customer master data
- Product master data
- Customer-specific service targets
- Order-level performance
- Order-line-level performance
- Calendar information

The source data is sufficiently structured for service-level
analysis.

---

## Key Integrity Checks

### Customer Integrity

Customer IDs appearing in transactional data should exist
in dim_customers.

Status:

**Validated during initial data inspection.**

---

### Product Integrity

Product IDs appearing in fact_order_lines should exist in
dim_products.

Status:

**Validated during initial data inspection.**

---

### Customer Target Integrity

Customers represented in transactional data should have
corresponding service-level targets.

Status:

**Validated during initial data inspection.**

---

### Duplicate Records

Duplicate rows should be checked separately for:

- Dimension tables
- fact_orders_aggregate
- fact_order_lines

The transaction grain must be preserved.

---

### OT / IF / OTIF Logic

OTIF should represent the combination of:

On Time AND In Full.

Therefore:

OTIF = 1 only when both On Time = 1 and In Full = 1.

The order-level performance data was cross-checked against
the underlying order-line information during initial
validation.

---

## Data Quality Risks to Investigate

### 1. Date Coverage

The date dimension and transactional date fields must be
checked for complete coverage.

### 2. Multiple Fact Grains

The order-level and order-line-level tables have different
grains.

Incorrect joins can cause duplicated orders and incorrect
KPIs.

### 3. Quantity Validation

Order quantity and delivery quantity should be checked for:

- Negative values
- Zero values
- Delivery quantity greater than ordered quantity

### 4. Delivery Date Validation

Actual delivery dates should be evaluated against:

- Order placement date
- Agreed delivery date

### 5. Boolean/Flag Validation

OT, IF and OTIF flags must contain valid values and follow
the expected business logic.

---

## Data Quality Conclusion

The dataset is suitable for the planned supply-chain
service-level analysis, subject to final validation in the
analytical environment.

The most important modeling risk is the difference between
order-level and order-line-level grain.

All KPIs must therefore be calculated using the appropriate
fact table.