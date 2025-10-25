---
title: "Data Lake ETL Readme"
permalink: /data-lake-etl-readme/
layout: single
classes: wide
# author_profile: true
---

This project contains a suite of ETL services that extract, transform, and load data into a unified Data Lake environment. The Data Lake architecture is designed as depicted in the following diagram.

![architecture-data-project-alfa-Architecture.drawio.svg](</assets/images/architecture-data-project-alfa-Architecture.drawio.svg>)

**Data Sources**

Any data source type can be integrated into the system. The following are the data source types supported by the system:

1. RDBMS (MySQL, Postgres, MSSQL, Oracle)
2. Flatfiles (CSV, TSV)
3. APIs (REST)

**Meta Data Service**

A separate metadata service is used, and the following are the functions performed by the metadata service in the system:

1. Unified metastore to store all the metadata of the data sources.
2. Track the lineage of the data pipelines.
3. Track the data pipeline errors (monitoring mechanism).

**Target Data Store**

The target data store is based on the Data Lake architecture and comprises the following layers.

- Raw data store

Raw data store is used to store the source data in the raw format (file-based). If the source data is among the following, it will be stored as the source file format.

- CSV,
- JSON,
- TSV,
- XLSX,
- XML,
- Parquet,

But if the source file format is not among the mentioned above, it can be converted into one of the above file formats.

Raw data storage is an object storage which we can use to store data as objects (files). In this project, the raw storage layer is made of **AWS S3** and can be easily migrated to another object storage solution such as **Azure object store**. 

- Processed data layer

Processed data layer consists of data which are identical to the data sources but transformed from raw format to a structured format. The processed layer comprises the following sub-layers:

- Landing storage

Landing storage is to load the changed data (delta or new) of a dataset. 

- Base layer (ODS)

This is to maintain identical structured data for the source dataset being ingested. There are transformations applied when loading data from landing to the base layer such as: cleaning data, validation, and schema enforcement.

- Analytics layer

Analytics layer consists of the data where the schema is ready for analytics (dimensional model). When loading data from the ODS to the Analytics layer, the data is denormalized and transformed into an analytics-ready format such as a dimensional model (snowflake, star, and galaxy models).

The analytics layer has two sub-layers:

- DW layer

This layer has denormalized and analytics-ready data. Normally, data users such as Data Scientists and Analysts use this layer for their analytical needs.

- Aggregate layer

This layer has aggregated data coming from the DW layer.

Both the processed and analytics layers are created in the cloud data warehouse solution called **Snowflake**, and the data layers can be migrated to other data warehouse solutions such as **AWS Redshift, BigQuery**, etc.  

**ETL Services**

All the ETL services are written in Python and use **Apache Airflow** as the orchestration tool. Hexagonal architecture is used to develop the service providers (Adapters and Ports), hence promoting separation of concerns and making the system more modular, testable, and easily migratable to other platforms (currently Snowflake, but can be extended to other platforms).


1. RDBMS to Data Lake ETL Service

    - Retrieve dataset configuration and extraction parameters from the metadata service.
    - For each dataset, determine if incremental extraction is enabled:
        - If incremental:
            - Calculate total rows and batches.
            - Extract data in chunks using offset and chunk size.
        - If not incremental:
            - Extract the entire dataset in one batch.
    - For each extracted batch:
        - Process and validate the data.
        - Save the batch as a CSV file in the data directory (or as a parquet file for full extraction).
    - Repeat extraction until all batches are processed.
    - The extracted files are ready for further transformation and loading into the processed layers (Landing, ODS) in the target data warehouse.

