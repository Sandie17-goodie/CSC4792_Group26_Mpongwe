# Data Dictionary — Mpongwe CDF Projects Dataset

| Column | Description |
|---|---|
| `project_id` | Unique identifier assigned to each project (format `CDF2025-XXX`) |
| `sector` | Sector the project falls under (e.g. Education, Health, Water and Sanitation). Blank for 4 records where the source PDF did not preserve a reliably extractable sector value. |
| `ward` | Ward associated with the project |
| `project_name` | Reconstructed project name/description from the source PDF |
| `approval_status` | One of `Approved`, `Not Approved`, or `Partially Approved` |
| `reason_not_approved` | Reason given for non-approval or partial approval. Blank for approved projects, since no rejection reason applies. |
| `year` | Year the projects were submitted/considered (2025) |
| `source_document` | Name of the source PDF document |
| `source_url` | Official URL of the source document on the Mpongwe Town Council website |

## Procurement Dataset

`db-unza26-csc4792-mpongwe_procurement.csv` contains annual procurement-plan
records published by Mpongwe Town Council for 2023, 2024, and 2025.

| Column | Description |
|---|---|
| `procurement_id` | Stable generated identifier based on the source plan year and printed spreadsheet row number (format `APPYYYY-NNN`). |
| `year` | Procurement-plan year stated in the source PDF. |
| `procurement_class` | Source procurement class, such as `goods`, `works`, or `non consulting services`. |
| `unspsc` | UNSPSC commodity/service code as printed in the source plan. |
| `description` | Procurement description where the source layout exposes a complete value. Blank where 2023/2025 printed cells are clipped rather than reconstructed. |
| `reference_number` | Official procurement reference number only when it can be extracted completely from the source PDF. |
| `unit_of_measure` | Unit of measure as printed in the plan. |
| `quantity` | Source quantity converted to a numeric value; blank where absent or not validly extractable. |
| `source_of_funds` | Source funding label as printed in the plan. |
| `procurement_method` | Source procurement-method code where the plan provides one. |
| `publication_date` | Planned publication date, normalized to `YYYY-MM-DD`. |
| `award_date` | Planned award date, normalized to `YYYY-MM-DD`, where supplied. |
| `start_date` | Planned start date, normalized to `YYYY-MM-DD`. |
| `estimated_budget_zmw` | 2025 planned total budget in Zambian kwacha, where supplied; blank for plans that do not provide a comparable field. |
| `comments` | Source comments where supplied. |
| `source_document` | Local filename of the official procurement-plan PDF. |
| `source_url` | Direct official Mpongwe Town Council URL for the source PDF. |
