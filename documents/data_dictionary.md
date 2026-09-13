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