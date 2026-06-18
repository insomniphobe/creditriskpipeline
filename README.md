# Credit Risk ETL Pipeline

## Overview
An end-to-end ETL pipeline built on Azure, processing a credit risk dataset 
into a structured Delta Lake table for analytics and ML workflows.

## Architecture
Raw CSV (ADLS) → Azure Databricks (PySpark) → Delta Table (ADLS)

## Technologies
- Azure Data Lake Storage Gen2
- Azure Databricks
- PySpark
- Delta Lake

## Pipeline Steps
1. **Extract** — Reads raw CSV from ADLS raw container
2. **Transform**
   - Imputes missing values in `person_emp_length` and `loan_int_rate` with column means
   - Removes outliers (employment length > 60, age > 100)
   - Adds human-readable `loan_status_label` column
   - Engineers `high_risk` feature flag for high interest/high income ratio loans
3. **Load** — Writes transformed data as a Delta table to ADLS processed container

## Data Quality Issues Found
- 895 null values in `person_emp_length`
- 3,116 null values in `loan_int_rate`
- 7 records with unrealistic employment length or age values
