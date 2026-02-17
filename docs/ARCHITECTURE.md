# ETL Toll Traffic Pipeline - Architecture

## Overview

This document describes the architecture and design decisions for the Road Traffic Toll ETL Pipeline built with Apache Airflow.

## System Architecture

The pipeline processes data from three different file formats:
- CSV files (vehicle entry logs)
- TSV files (toll plaza metadata)
- Fixed-width files (payment information)

All data flows through Apache Airflow orchestration, where extraction, transformation, and consolidation tasks are executed sequentially.

## DAG Configuration

- **DAG ID**: `ETL_toll_data`
- **Schedule**: Daily execution
- **Retry Policy**: 1 retry with 5-minute delay
- **Operators**: BashOperator for all tasks

## Task Dependencies

```
unzip_data
  → extract_data_from_csv
  → extract_data_from_tsv
  → extract_data_from_fixed_width
  → consolidate_data
  → transform_data
```

## ETL Process

### Extract Phase
- Unzip compressed archive
- Extract specific columns from CSV using cut command
- Extract specific columns from TSV using cut with tab delimiter
- Extract character ranges from fixed-width file using cut -c

### Transform Phase
- Consolidate extracted files using paste command
- Standardize text by converting to uppercase using tr command

### Load Phase
- Output written to staging directory as transformed_data.csv
- Ready for downstream analytics

## Design Decisions

**BashOperator**: Chosen for simplicity and efficiency. The transformations are straightforward column extractions and text operations that can be handled effectively with Unix utilities.

**Sequential Dependencies**: Each task depends on the output of the previous task, ensuring data integrity and making debugging easier.

## Error Handling

- Retry mechanism: 1 retry with 5-minute delay
- Email notifications on failure
- Comprehensive logging in Airflow
