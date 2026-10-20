Week 2 – Clean and Define

Project: Heavy Supplier, Inventory & Warehouse Analytics
Team: Jency, Frank, Rofiat, Zainab
Week 2 goal: Cleaning is underway and all metrics have agreed definitions.
Status: Mostly complete. Three of four tasks finished. Jency's data cleaning is still outstanding.

What we delivered this week

KPI Framework (Zainab) — done.
We now have 13 agreed ways to measure the warehouse, with a name, formula and plain-English meaning for each. They cover four areas: warehouse cost and performance, inventory health, stock movement, and checking whether our stock records match reality. We also agreed six data-quality checks that must pass before any number is trusted.

Metric Rules (Frank) — done.
We agreed how to classify products and stock:

ABC: products ranked by revenue, with the top 80% of revenue as A, the next 15% as B, and the last 5% as C. Result: 10 A products bring in about 81% of revenue, and just two products (P014 and P015) bring in about 36%.

Movement: rules for fast, medium, slow and dead stock. Result: all 180 product-branch combinations came out as fast-moving, which is suspicious and needs checking.

Stock health: days of cover compared to lead time. Result: all 180 combinations are "excess" stock — about 31,000 to 39,000 days of cover. This is not believable and points to a data problem.

Suppliers: rules for on-time delivery, delays, cancellation rate and spend. Result: all 8 suppliers look almost identical, which matches what we found in Week 1.

Customer Rules (Rofiat) — done.
We defined what counts as a churned customer, a repeat customer, a high-value customer, and how to measure purchase frequency. Rofiat also set up Python for the next stage.

Data Cleaning and Data Dictionary (Jency) — not received.
This was the Friday deliverable and it is still missing. Without it we cannot produce the cleaned tables. This needs to be chased.

Decisions we still need to make

Is the stock level of about 107,000 units per product per branch real, or a data error? This blocks all inventory results.

Which table is the correct source for reorder level, safety stock and max stock?

Should cancelled orders be excluded from all analysis? We have assumed yes.

Is the margin column markup or margin? Frank says markup.

Do we accept the ABC 80/15/5 cut-offs, and should ABC be based on revenue or profit?

Is 180 days the right rule for dead stock?

How many days without a purchase counts as churn?

Blockers
Jency's data cleaning and data dictionary have not been received. The cleaned tables cannot be completed until they are.

Next week (Week 3)
Jency merges all the tables and creates new columns such as stock age and lead time. The rest of us test our analysis on the partial data and report problems. Zainab also sets up the Power BI template so all dashboards look the same. Friday deliverable: merged dataset and the Power BI template.
