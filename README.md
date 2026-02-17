# Road Traffic Toll ETL Pipeline with Apache Airflow

This project implements an automated ETL pipeline in Apache Airflow to process road traffic toll data from multiple operators. The pipeline consolidates vehicle, toll plaza, and payment information from different file formats (CSV, TSV, and fixed-width text files) into a single, cleaned dataset for traffic congestion analysis.

## Problem Statement

Different toll operators across national highways send traffic data in various formats:
- CSV files containing vehicle entry logs
- TSV files with toll plaza identifiers  
- Fixed-width files with payment details

The goal is to build a reusable, automated Airflow DAG that extracts, transforms, and consolidates this heterogeneous data into a unified, analysis-ready dataset.

## Pipeline Overview

The DAG consists of 6 sequential tasks:

1. **unzip_data** - Extracts the compressed tolldata.tgz archive
2. **extract_data_from_csv** - Extracts columns 1-4 from vehicle-data.csv
3. **extract_data_from_tsv** - Extracts columns 5-7 from tollplaza-data.tsv
4. **extract_data_from_fixed_width** - Extracts character positions 59-62 and 63-67 from payment-data.txt
5. **consolidate_data** - Merges all three extracted files horizontally using paste command
6. **transform_data** - Standardizes text data by converting to uppercase

## Project Structure

```
etl-toll-traffic-airflow/
├── README.md
├── COMMANDS.md
├── dags/
│   └── ETL_toll_data.py
├── docs/
│   ├── ARCHITECTURE.md
│   └── ETL_Project_Report.pdf
└── images/
    └── (screenshots)
```

## Technologies Used

- Apache Airflow for workflow orchestration
- BashOperator for shell-based data processing
- Unix utilities (tar, cut, paste, tr)
- CSV, TSV, and Fixed-width text file handling

## Documentation

- [Architecture Documentation](docs/ARCHITECTURE.md)
- [Project Report](docs/ETL_Project_Report.pdf)
- [Setup and Deployment Commands](COMMANDS.md)

