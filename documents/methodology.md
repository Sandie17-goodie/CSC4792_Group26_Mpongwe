# Methodology — Mpongwe CDF Dataset Extraction

1. **Source**: Official Mpongwe Town Council 2025 "Approved and Unapproved
   Community Projects" PDF.
2. **Extraction**: Used `pdfplumber` to extract raw text and tables from
   every page of the PDF.
3. **Segmentation**: Split the extracted text into individual project
   records using sequential project numbering, correcting for false splits
   caused by numbers embedded inside project descriptions.
4. **Field recovery**: Identified sector, ward, and approval status using
   known label lists as anchors, with targeted manual fixes for the small
   number of records where PDF column extraction split values incorrectly.
5. **Description reconstruction**: Rebuilt clean project descriptions
   directly from the PDF's table cells, searching across multiple possible
   columns, with manual corrections for a few duplicated text fragments.
6. **Rejection reasons**: Standardised recurring rejection reasons (e.g.
   "Inadequate Funding", "Not the first priority") and preserved unique
   explanations for special cases.
7. **Validation**: Checked the final dataset for correct row count (84),
   duplicate project IDs, duplicate rows, and missing values, leaving
   genuinely unrecoverable sector values blank rather than guessing.
8. **Export**: Saved the final dataset as a pipe-separated (`|`) CSV
   following the CSC4792 naming convention.

## Procurement Dataset Extraction

1. **Source discovery**: Used only the official Mpongwe Town Council
   publications page and its direct links to annual procurement plans for 2023,
   2024, and 2025.
2. **Document inspection**: Confirmed that all three PDFs contain
   machine-readable spreadsheet tables. The 2023 plan has two horizontal page
   sections, the 2024 plan is a single table, and the 2025 plan has left/right
   sections across six pages. Repeated headers and page numbers are not data.
3. **Extraction**: Used `pdfplumber` table extraction and each plan's printed
   spreadsheet row number to pair corresponding horizontal sections. Generated
   identifiers retain that year-and-row provenance (`APPYYYY-NNN`).
4. **Cleaning and normalization**: Normalized whitespace and line breaks,
   converted unambiguous source dates to ISO format, converted valid quantities
   and 2025 planned budgets to numeric values, and retained the original source
   labels for classifications, funding, and methods.
5. **Missing values**: Kept values blank when absent, malformed, or visually
   clipped in the source PDF. The 2023 and 2025 layouts clip description and
   some reference-number cells, so no descriptions or reference values are
   inferred from partial text.
6. **Validation**: Verified 47 rows for 2023, 37 for 2024, and 63 for 2025;
   verified 147 total rows, 17 columns, unique IDs, no duplicate full rows,
   source-year consistency, complete source document/URL fields, and absence of
   header/page-number records. The exported pipe-separated CSV is read back and
   checked again.
7. **Limitation**: Procurement plans describe planned activity, not confirmed
   completed procurement. No financial dataset was exported because a complete
   official financial document could not be retrieved and structurally assessed
   to the same reliability standard.
