# Decision Log 
## 1. Missing Customer ID
- Found: 107,927 rows (about 20% of the data) have no Customer ID.
- Decision: Keep these rows in the main dataset. Leave them out only for the customer analysis.
- Why: Each of these rows is still a real sale with a product, price and date. Deleting them would make product, monthly and country totals about 20% too low. They cannot be used for customer questions because we do not know who bought.
## 2. What counts as a sale
- Found: Not every row is a real sale. Invoices starting with C are cancellations (negative quantity), invoices starting with A are bad debt adjustments, and some rows with negative quantity and price 0 are stock adjustments (lost or damaged items).
- Decision: A sale is a row that is not a C or A invoice, with quantity above 0 and price above 0. Cancellations are kept in a separate table.
- Why: Counting these rows would make sales totals wrong. Cancellations are kept so we can later see which products are returned most.
## 3. Duplicate rows
- Found: 34,335 rows were exact duplicates (about 3%), partly because the two yearly sheets overlap in early December 2010.
- Decision: Remove exact duplicates, keeping the first copy.
- Why: Counting the same sale twice would make totals too high. A few may have been genuine repeat lines, but we cannot tell them apart.
## 4. Huge orders cancelled by mistake
- Found: Two sales were enormous (80,995 and 74,215 units, invoices 581483 and 541431), and each was cancelled minutes later by the same customer.
- Decision: Remove these two orders from the sales table.
- Why: They were never real sales. Keeping them made two products look like top sellers. Smaller orders that were later cancelled are still counted; this is noted as a limitation.