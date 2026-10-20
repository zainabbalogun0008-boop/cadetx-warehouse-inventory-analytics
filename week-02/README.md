# Week 2 – Clean and Define

**Project:** Heavy Supplier, Inventory & Warehouse Analytics  
**Team:** Jency, Frank, Rofiat, Zainab  
**Goal:** Clean the data and agree on metric definitions.  
**Status:** Mostly complete — three of four tasks finished.

## What We Delivered This Week

### 1. KPI Framework — Zainab (Completed)

Defined 13 warehouse KPIs, each with a name, formula and plain-English meaning. The KPIs cover:

- Warehouse cost and performance
- Inventory health
- Stock movement
- Stock record accuracy

Six data-quality checks were also agreed upon before trusting the results.

### 2. Metric Rules — Frank (Completed)

**ABC classification:** Products are ranked by revenue: the top 80% is A, the next 15% is B, and the final 5% is C.

- Ten A products generate approximately 81% of revenue.
- Products P014 and P015 account for approximately 36% of revenue.

**Stock movement:** Rules were defined for fast-, medium-, slow- and dead-moving stock. All 180 product-branch combinations were classified as fast-moving, which requires investigation.

**Stock health:** Days of cover were compared with lead time. All 180 combinations were classified as excess stock, with approximately 31,000–39,000 days of cover. These results are implausible and suggest a data or calculation issue.

**Supplier performance:** Rules were defined for on-time delivery, delays, cancellation rate and spend. All eight suppliers showed very similar results, consistent with the concern identified in Week 1.

### 3. Customer Rules — Rofiat (Completed)

Defined rules for identifying churned customers, repeat customers and high-value customers, alongside purchase frequency. Python was also set up for the next stage.

### 4. Data Cleaning and Data Dictionary — Jency (Outstanding)

The Friday deliverable has not yet been received. The cleaned tables cannot be completed until the data cleaning and data dictionary are available.

## Decisions Still Required

1. Is the stock level of approximately 107,000 units per product per branch genuine or a data error?
2. Which table is the correct source for reorder level, safety stock and maximum stock?
3. Should cancelled orders be excluded from all analyses? The current assumption is yes.
4. Does the margin column represent markup or margin? Frank's interpretation is markup.
5. Are the ABC 80/15/5 cut-offs appropriate, and should classification be based on revenue or profit?
6. Is 180 days without movement the right definition of dead stock?
7. How long without a purchase should qualify a customer as churned?

## Blockers

Jency's data cleaning and data dictionary deliverables remain outstanding. The cleaned tables cannot be finalised until these are received.

## Week 3 Plan

- **Jency:** Merge the tables and create additional fields, including stock age and lead time.
- **Team:** Test analyses using the available data and document anomalies.
- **Zainab:** Set up a Power BI template to standardise dashboard design.

**Friday deliverables:** Merged dataset and Power BI template.
