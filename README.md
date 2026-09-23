Inventory & Stock Movement: Exploratory Data Analysis
1. Domain Context
This dataset records inventory ledger transactions from a healthcare facility or pharmaceutical dispensary. In clinical supply chains, pharmaceutical items (such as Prednisolone, Fuclear V Pessaries, and Isocet P) move continuously between central receiving hubs (Main Store), operational dispensing units (Pharmacy), and end users or external vendors.

Tracking every ledger event—whether a routine internal stock transfer, an invoice-backed vendor receipt, or a manual stock adjustment—is critical for:

Preventing stockouts of essential medications and patient treatments.

Minimizing financial leakage caused by shrinkage, spoilage, or unrecorded adjustments.

Ensuring clinical and regulatory compliance across handling facilities.

2. Problem Statement
Pharmaceutical inventory systems are susceptible to discrepancies caused by unrecorded transfers, miscalibrated manual adjustments, and dead-stock accumulation. Without transparency into internal movement velocities and adjustments, the organization risks holding tied-up capital in excess buffer stock or facing sudden shortages of critical clinical supplies.

Analytical Objectives:

Movement Flow & Velocity: Profile the volume and financial value of stock transfers across facilities (source_location → destination_location).

Adjustment Auditing: Analyze the frequency, scale, and personnel attribution (created_by) behind Stock_Adjustment events to detect reconciliation anomalies or shrinkage.

Data Integrity & Type Rectification: Identify structural defects in the current ledger (such as quantity stored as text instead of a signed numeric type, and sparse columns like client and stock_invoice).

Value Concentration: Determine which stock items account for the highest transactional volume and monetary throughput.

3. Data Dictionary
item_code: Stored as text (object) with 1,000 complete entries (0.0% missing), representing the unique SKU or catalog code assigned to each pharmaceutical item.

item_name: Stored as text (object) with 1,000 complete entries (0.0% missing), describing the proprietary brand name, active formulation, strength, and packaging of the medicine.

date: Stored as text (object) with 1,000 complete entries (0.0% missing), tracking the recorded date and timestamp of the transaction, which requires parsing into a standard datetime type.

reference: Stored as text (object) with 1,000 complete entries (0.0% missing), serving as the unique journal voucher, batch record, or internal document ID.

description: Stored as text (object) with 995 non-null entries (0.5% missing), summarizing the operational nature of the journal movement, such as an internal transfer or inventory adjustment.

client: Stored as a floating-point number (float64) with only 5 non-null entries (99.5% missing), indicating an external counterparty identifier that is almost entirely unpopulated across internal records.

quantity: Stored as text (object) with 1,000 complete entries (0.0% missing), recording the unit volume moved or adjusted, where positive numbers denote incoming stock and negative numbers denote disbursements, requiring conversion to a numeric data type.

movement_type: Stored as text (object) with 1,000 complete entries (0.0% missing), categorizing high-level inventory events into core types such as stock entries or manual stock adjustments.

purpose: Stored as text (object) with 1,000 complete entries (0.0% missing), specifying the underlying business reason for the record, including department transfers and reconciliation adjustments.

source_location: Stored as text (object) with 999 non-null entries (0.1% missing), detailing the originating facility or store room supplying the items.

destination_location: Stored as text (object) with 736 non-null entries (26.4% missing), identifying the receiving facility or clinic unit, with missing entries corresponding to unilateral adjustments that lack an internal transfer recipient.

created_by: Stored as text (object) with 1,000 complete entries (0.0% missing), logging the system username of the employee who generated and posted the ledger transaction.

prev_stock_qty: Stored as a floating-point number (float64) with 982 non-null entries (1.8% missing), reflecting the on-hand physical stock quantity recorded immediately prior to the transaction event.

price: Stored as a floating-point number (float64) with 1,000 complete entries (0.0% missing), indicating the unit monetary price or standard cost assigned to a single item unit.

amount: Stored as a floating-point number (float64) with 996 non-null entries (0.4% missing), representing the total financial value associated with the movement, calculated as unit price multiplied by movement quantity.

stock_invoice: Stored as text (object) with 228 non-null entries (77.2% missing), capturing external vendor invoice numbers for purchases, which remain unpopulated for internal movements.