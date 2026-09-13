# CSC4792_Group26_Mpongwe# CSC4792 Group 26 — Mpongwe Town Council CDF Dataset

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