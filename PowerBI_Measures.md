# Power BI model

## Relationships
Calendar[Date] (1) → Invoices[Invoice Date] (*)
Vendors[Vendor] (1) → Invoices[Vendor] (*)

## Core measures

Total Spend = SUM(Invoices[Gross Amount])

Invoice Count = DISTINCTCOUNT(Invoices[Invoice ID])

Average Invoice = DIVIDE([Total Spend], [Invoice Count])

Paid Spend = CALCULATE([Total Spend], Invoices[Status] = "Paid")

Open Spend = CALCULATE([Total Spend], Invoices[Status] = "Open")

Overdue Spend = CALCULATE([Total Spend], Invoices[Status] = "Overdue")

Review Queue = CALCULATE([Invoice Count], Invoices[Review Required] = "Review")

Duplicate Invoices = CALCULATE([Invoice Count], Invoices[Duplicate Flag] = "Yes")

Anomaly Invoices = CALCULATE([Invoice Count], Invoices[Anomaly Flag] = "Yes")

Exception Rate = DIVIDE([Review Queue], [Invoice Count])

Top Supplier Spend = MAXX(VALUES(Invoices[Vendor]), [Total Spend])

Top Supplier Share = DIVIDE([Top Supplier Spend], [Total Spend])
