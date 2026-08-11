# Data Preparation & Transformation Notes

## Objective

The source dataset is already structured and relatively clean.
Therefore, this project does not introduce artificial data
cleaning steps.

The preparation stage focuses on validating the source data,
standardizing data types, enforcing business rules, and
creating fields required for analytical modeling.

---

## 1. Source Data Validation

The following checks will be performed:

- Missing values
- Duplicate records
- Primary key uniqueness
- Foreign key validity
- Data types
- Date validity
- Quantity validity
- OT/IF/OTIF consistency

---

## 2. Data Type Standardization

Expected data types:

### Identifiers

Customer, product and order identifiers will be stored as
text values.

### Dates

Order placement dates, agreed delivery dates and actual
delivery dates will use Date data types.

### Quantities

Order and delivery quantities will use whole-number data
types.

### Service Flags

On-Time, In-Full and OTIF indicators will use numeric/Boolean
representation.

### Targets

Customer service-level targets will use decimal percentage
values.

---

## 3. Business Rule Validation

The following rules will be validated:

### OTIF Rule

An order can be classified as OTIF only when:

On Time = 1

AND

In Full = 1

---

### Quantity Rule

Delivery quantity will be compared with order quantity to
identify quantity gaps.

Quantity Gap:

Order Quantity - Delivery Quantity

---

### Target Rule

Actual service performance will be compared with the
customer-specific target.

Target Gap:

Actual Performance - Target Performance

---

## 4. Analytical Fields

The following derived metrics/fields may be created during
the modeling stage:

- OT Target Gap
- IF Target Gap
- OTIF Target Gap
- Order Quantity Gap
- Delivery Performance Classification
- Customer Priority Classification

These fields are analytical transformations rather than
source-data cleaning.

---

## 5. Grain Preservation

The dataset contains two transactional grains:

### Order Level

fact_orders_aggregate

One row represents one order.

### Order-Line Level

fact_order_lines

One row represents one product line within an order.

The two fact tables will not be directly combined in a way
that duplicates order-level records.

---

## 6. Preparation Philosophy

The goal is not to artificially modify clean data.

The goal is to:

1. Preserve the integrity of the source data.
2. Validate business rules.
3. Standardize data types.
4. Prepare a reliable analytical model.
5. Create only the transformations required for business
   analysis.

All material transformations will be documented for
reproducibility.




## Validation Completed

The initial Power Query validation was completed before
loading the data into Power BI.

### Data Type Validation

The following identifiers were standardized as Text:

- customer_id
- product_id
- order_id

Date fields were validated as Date types.

Quantity fields were validated as Whole Number types.

OT, IF and OTIF indicators were retained as numeric flags.

Customer service-level targets were retained as whole-number
percentage values.

### Data Quality Checks Completed

#### Customer Key

`dim_customers.customer_id` was checked for duplicate values.

Result:

- No duplicate customer IDs identified.
- Customer ID can be treated as a dimension key.

#### Order-Level Grain

`fact_orders_aggregate.order_id` was checked for duplicates.

Result:

- No duplicate order IDs identified.
- One row represents one order.

#### Order-Line Grain

The combination of:

`order_id + product_id`

was checked for duplicate combinations.

Result:

- No duplicate combinations identified.
- One row represents one product line within an order.
- `order_id + product_id` uniquely identifies the order line
  in the current dataset.

### Transformation Philosophy

The source dataset was already relatively clean and
well-structured.

Therefore, no unnecessary row deletion, imputation, or
artificial cleaning was performed.

The preparation stage focused on:

- Data type standardization
- Grain validation
- Key validation
- Business-rule validation
- Preparing the data for analytical modeling

Further validation will be performed during data modeling and
KPI development.