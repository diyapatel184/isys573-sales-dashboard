# Data Dictionary — sales.csv

This document describes all columns in `data/sales.csv`, the source
dataset for the ISYS 573 Retail Sales Dashboard.

| Column | Data Type | Description | Example Value | Constraints / Business Rules |
|---|---|---|---|---|
| date | datetime | Transaction date in ISO format | 2024-03-15 | Required; format YYYY-MM-DD; range 2024-01-01 to 2024-12-31 |
| region | string | Sales region where transaction occurred | West | Required; one of: West, East, South, Midwest |
| category | string | Product category | Electronics | Required; one of 6 categories |
| product | string | Product name | Laptop Pro 15 | Required; must exist in product master |
| units_sold | integer | Number of units sold in transaction | 3 | Required; must be > 0 |
| unit_price | float | Price per unit before discount | 1299.99 | Required; must be > 0 |
| discount_pct | float | Discount percentage applied | 0.10 | Required; range 0.0 to 1.0 |
| revenue | float | Final revenue after discount | 3509.97 | Required; = units_sold × unit_price × (1 - discount_pct) |
| channel | string | Sales channel used | Online | Required; one of: Online, In-Store, Partner |
| sales_rep | string | Name of sales representative | Jane Smith | Required; must match HR employee list |

## Notes
- **Never modify this file** — it is the read-only source of truth
- All monetary values are in USD
- Revenue is pre-calculated; do not recompute from other columns
- Date range covers full calendar year 2024 (500 transactions total)
