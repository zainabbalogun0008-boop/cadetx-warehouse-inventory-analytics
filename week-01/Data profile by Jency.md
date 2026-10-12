# Week 1 – Data Profile Summary
**Project:** Heavy Supplier, Inventory & Warehouse Analytics (CadetX)
**Prepared by:** Jency (Data Lead)
**Files:** `data_profile.py` (script), `data_profile_tables.csv`, `data_profile_columns.csv`, `data_profile_relationships.csv`

## 1. What we have

| Table | Rows | Columns | Key | What one row is |
|---|---:|---:|---|---|
| branches | 6 | 13 | branch_id | A branch / warehouse (DEL, PUN, CHN, HYD, KOL, AHM) |
| customers | 500 | 15 | customer_id | A customer |
| products | 30 | 23 | product_id | A spare part (heavy machinery) |
| suppliers | 8 | 12 | supplier_id | A supplier (all based in China) |
| inventory_master | 180 | 8 | product_id + branch_id | Stock settings for one product at one branch (30 × 6) |
| sales_orders_header | 20,000 | 11 | so_id | A sales order |
| sales_orders_lines | 130,402 | 9 | so_id + line_number | One product line on a sales order |
| invoices | 18,033 | 10 | invoice_id* | An invoice for a delivered sales order |
| payments | 19,257 | 5 | payment_id* | A customer payment against an invoice |
| purchase_orders_header | 24,000 | 10 | po_id | A purchase order to a supplier |
| purchase_orders_lines | 155,495 | 9 | po_id + line_number | One product line on a purchase order |
| stock_ledger | 237,230 | 9 | movement_id | One stock movement (IN / OUT / ADJUSTMENT) |

Date range: sales orders run from **Jan 2019 to Dec 2024**; the stock ledger runs to **Jan 2025**.
\* These keys are not unique; see issue 1.

## 2. What is already in good shape
- **No fully duplicated rows** in any table.
- **All 16 relationships between tables are valid.** Every customer, product, supplier, branch, order and invoice ID that one table points to exists in the table it points to (0 orphan rows).
- **Order totals reconcile.** Every sales order and purchase order header total equals the sum of its lines.
- **No negative values** in any numeric column. No product is priced below cost, and no customer is over their credit limit.
- **Order flow is consistent.** All 18,033 delivered sales orders have an invoice. The 1,967 cancelled orders correctly have no invoice. No order is delivered before it was placed.

## 3. Issues found (to fix or decide on in Week 2)

| # | Table | Issue | Size | Suggested action |
|---|---|---|---|---|
| 1 | invoices, payments | **Duplicate IDs.** The same invoice_id is used for two different invoices (different orders and customers); the same happens for payment_id. | 197 extra invoice rows (196 IDs); 202 extra payment rows | Create a new unique key. Payments join to invoices only on invoice_id, so payments for these 196 IDs can't be matched to the right invoice; flag them. |
| 2 | inventory_master | **current_stock is far above max_stock for every row** (average ~107,000 units vs a max of ~320). It matches the stock ledger's final running balance, so stock-in has far exceeded stock-out over six years. | 180 of 180 rows | Decide with the team: is this a real overstock story or a data scale problem? Don't use it for KPIs until agreed. |
| 3 | stock_ledger | **ADJUSTMENT quantities have no direction** (always positive), so we can't tell if stock was added or removed. | 2,454 rows | Infer the sign from the change in running_balance. |
| 4 | payments | **Payments dated before their invoice.** | 92 payments | Flag; check after fixing issue 1. |
| 5 | payments | **Invoices paid more than their grand total.** | 155 invoices | Likely partly caused by issue 1; recheck after the key fix. |
| 6 | purchase_orders_header | **received_date missing.** All missing values belong to cancelled POs, so this is expected, not an error. | 2,370 rows (9.9%) | Keep blank and document that cancelled POs are never received. |
| 7 | all date columns | **Dates stored as text** (12 columns across 7 tables, including customer_since). | – | Convert to proper date types. |
| 8 | branches | **warehouse_capacity is text** ("45230 sqft"). | 6 rows | Strip "sqft" and convert to a number (needed for Zainab's utilisation KPIs). |
| 9 | invoices, orders | **Floating-point noise** in GST amounts (e.g. 609423.0000000001). | many rows | Round money columns to 2 decimals. |

## 4. Early observations for the team
- **Frank (suppliers):** 3,267 of 21,630 received purchase orders (**15%**) arrived after the expected delivery date. This is a good starting point for supplier reliability.
- **Rofiat (customers):** 3,660 invoices are partially paid and 1,837 unpaid.
- **Zainab (warehouse):** capacity needs converting to numbers first (issue 8), and the inventory overstock question (issue 2) affects utilisation KPIs.

## 5. Next week (Week 2)
Fix issues 1, 3, 7, 8 and 9. Agree on issue 2 as a team. Start the data dictionary.
