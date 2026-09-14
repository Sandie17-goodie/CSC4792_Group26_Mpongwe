# CSC4792 Group 26 — Mpongwe Town Council CDF Dataset

This project extracts and cleans a structured dataset of **84 Constituency
Development Fund (CDF) community projects** for Mpongwe Town Council
(Copperbelt Province, Zambia), for the CSC4792 Data Mining and Warehousing
mini-project.

## Source

The dataset is derived from Mpongwe Town Council's official 2025
"Approved and Unapproved Community Projects" PDF, published on the
council website.

## Tools

- Python 3
- pandas
- pdfplumber
- Jupyter Notebook

## Process

1. Extract raw text and tables from the source PDF using `pdfplumber`.
2. Segment the text into 84 individual numbered project records, correcting
   for false splits caused by numbers inside descriptions (e.g. "3 toilets").
3. Recover each project's sector, ward, and approval status using known
   label lists, with manual fixes for records split across PDF columns.
4. Extract and standardise rejection reasons for projects that were not
   approved.
5. Reconstruct clean project descriptions directly from the PDF's table
   cells, with a small number of manual corrections for duplicated
   fragments.
6. Validate the final dataset (row count, duplicate IDs, missing values).
7. Export as a pipe-separated (`|`) CSV following the CSC4792 naming
   convention.

## Repository structure

```text
CSC4792_Group26_Mpongwe/
├── data/
│   ├── raw/                 # source PDF (not committed if large/restricted)
│   └── processed/           # final exported CSV
├── notebooks/
│   └── group26_mpongwe_dataset_creation.ipynb
├── documents/
│   ├── data_dictionary.md
│   ├── methodology.md
│   └── cdf_dataset_schema.txt
├── requirements.txt
└── README.md
```

## Reproducing the dataset

1. Install dependencies: `pip install -r requirements.txt`
2. Place the source PDF at `data/raw/mpongwe_cdf_projects_2025.pdf`
3. Run all cells in `notebooks/group26_mpongwe_dataset_creation.ipynb`
4. The cleaned dataset is written to
   `data/processed/db-unza26-csc4792-mpongwe_cdf_projects.csv`

## Completed datasets

The repository contains two completed, official-source datasets:

| Dataset | Records | Coverage | Output |
|---|---:|---|---|
| CDF projects | 84 | 2025 | `data/processed/db-unza26-csc4792-mpongwe_cdf_projects.csv` |
| Annual procurement plans | 147 | 2023-2025 | `data/processed/db-unza26-csc4792-mpongwe_procurement.csv` |

Both files are UTF-8 CSVs with `|` as the separator. The original CDF
content remains unchanged. A financial dataset is not included because the
official financial source assessed for this update could not be retrieved as a
complete file for structural validation; no values were inferred or exported.

## Procurement sources and coverage

The procurement dataset uses annual procurement plans published directly by
Mpongwe Town Council. The raw PDFs are retained in `data/raw/procurement/`:

- `mpongwe_procurement_plan_2023.pdf` - 47 plan rows.
- `mpongwe_procurement_plan_2024.pdf` - 37 plan rows.
- `mpongwe_procurement_plan_2025.pdf` - 63 plan rows.

The plans are machine-readable spreadsheets rendered as PDFs. The 2023 and
2025 plans use horizontal page splits; the notebook joins paired page sections
by the original spreadsheet row number. It excludes repeated headers and page
numbers, normalizes whitespace/dates/numeric values, and retains missing values
where the PDF does not provide a complete value. Source-visible description
text is retained verbatim, including visible truncation; incomplete reference
numbers are not guessed.

## Repository structure

```text
data/
  raw/
    mpongwe_cdf_projects_2025.pdf
    procurement/                 # official 2023-2025 procurement PDFs
  processed/
    db-unza26-csc4792-mpongwe_cdf_projects.csv
    db-unza26-csc4792-mpongwe_procurement.csv
notebooks/
  group26_mpongwe_dataset_creation.ipynb
documents/
  data_dictionary.md
  methodology.md
```

## Reproducing all completed datasets

1. Install dependencies: `pip install -r requirements.txt`
2. Ensure the CDF source and the three procurement PDFs are present in the raw
   paths shown above.
3. Open `notebooks/group26_mpongwe_dataset_creation.ipynb` and restart the
   kernel, then run all cells from top to bottom.
4. The notebook recreates both processed CSV files and validates their exports.
