# Homework 3 — Bank Marketing SQL Analysis

This project is a SQL homework based on the **UCI Bank Marketing** dataset. It demonstrates how to load a CSV file into PostgreSQL, prepare a typed table, check data quality, and explore the data using SQL queries.

## Dataset

- **Source:** [UCI Machine Learning Repository — Bank Marketing](https://archive.ics.uci.edu/dataset/222/bank+marketing)
- **File:** `bank-full.csv` (the full Bank Marketing dataset)
- **Size:** 45,211 records and 17 source columns
- **Format:** CSV with a semicolon (`;`) delimiter
- **Target:** `y` — whether a client subscribed to a term deposit (`yes` / `no`)

The original CSV is included in the repository root without cleaning or modification. The notebook also downloads the file directly from the official UCI archive, so the local copy is not required to execute it.

## Repository Structure

```text
goit-rdb-hw-03/
├── README.md
├── hw3_UCI_bank_Kalashnikov_Mykola.ipynb
└── bank-full.csv
```

## How to Run

1. Open `hw3_UCI_bank_Kalashnikov_Mykola.ipynb` in **Google Colab**.
2. Select **Runtime → Run all**.
3. The notebook installs the required Python packages, starts a local PostgreSQL server using `pgserver`, and downloads the original CSV from UCI.
4. The notebook loads the CSV using PostgreSQL `COPY FROM STDIN`, creates a clean table, and runs the SQL analysis.

The notebook uses Python, PostgreSQL (via `pgserver==0.1.4`), `psycopg2`, SQLAlchemy, and pandas. No external PostgreSQL instance is required. Internet access is needed for the package installation and dataset download.

**Colab runtime note:** I used Google Colab runtime version **2026.07** (an older version rather than the latest one) for compatibility with `pgserver`.

## Homework Tasks

1. **Setup and Data Loading:** Download the dataset and import 45,211 records into a staging table using `COPY FROM STDIN`.
2. **Staging and Typed DDL:** Create a clean table with appropriate data types, constraints, and documented cleaning rules.
3. **Data-quality Audit:** Compare row counts, check duplicates, and examine NULL and special values.
4. **Distributions and Anomalies:** Analyze categorical and numeric distributions and flag unusual values.
5. **DQL / EDA Queries:** Answer 12 business questions using SQL.
6. **Reflection:** Summarize data quality findings, ML considerations, and possible pipeline improvements.

## Main Findings

- All **45,211 records** were transferred to the clean table, with no exact duplicates found across the 17 source attributes.
- **11.70%** of records have a positive subscription outcome (`subscribed = TRUE`).
- Some categorical fields contain `unknown` values, especially `poutcome` (**81.75%**) and `contact` (**28.80%**).
- `pdays = -1` indicates no previous contact and is preserved as a special value.
- Call duration is strongly associated with the subscription outcome, but the final duration is not available before a call ends. It should not be used for a pre-call prediction model.

All SQL queries, saved results, explanations, and the final reflection are available in the notebook.
