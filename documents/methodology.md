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