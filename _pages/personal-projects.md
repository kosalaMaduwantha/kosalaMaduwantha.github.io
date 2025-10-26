---
title: "Personal Projects"
permalink: /personal-projects/
layout: single
classes: wide
sidebar:
  nav: "projects"
---
## Data Engineering and AI/ML Projects

### 1. Atlas Insights
Comprehensive, metadata‑driven ingestion and analytics framework for big data.

Data Ingestion module is implemented for three primary source types:

- File system (CSV ➜ Parquet on HDFS)
- Relational databases (MySQL / PostgreSQL / SQL Server ➜ Parquet on HDFS)
- Streaming (WebSocket JSON ➜ Kafka topics – foundation for near‑real‑time ingestion)

Built with Python, PyArrow, FastAPI, and Kafka; designed to standardize how raw operational data is landed into an analytics‑friendly lake/warehouse zone (HDFS Parquet) using a **single metadata contract**.

**Highlevel architecture:**
![Atlas Insights High-Level Architecture](</assets/images/atlas_insights_architecture.svg>)

🔧 **core module functionalities**

- Metadata‑driven: single metadata contract defines source, destination, schema, and transformations.
- Data ingestion: batch (file, RDBMS) and streaming (Kafka).
- Data transformation and validation: column mapping, type casting, basic cleansing (Can be configured via metadata).
- Target storage: writes to HDFS in Parquet format. Apache Hive will be integrated for data management in hdfs filesystem.
- Error handling and logging: centralized error handling and logging for all ingestion processes. Log aggregation and monitoring yet to be implemented.
- Downstream applications: Reporting service and Recommendation engine (in progress).

🛠️ **technology and approaches used**

- Data ingestion: Python (FastAPI, PyArrow) for RDBMS and Flat files ingestion and Apache Kafka for streaming data.
- Ochestration: Apache Airflow for scheduling and monitoring ingestion workflows.
- Data storage: HDFS for raw data, Apache Hive for data management (in progress).
- Data processing: Apache Spark for data transformation and validation on top of hdfs file system (in progress).
- Monitoring: Prometheus and Grafana for monitoring and alerting (in progress).

<a href="/atlas-insights-readme/" class="btn btn--primary">View Detailed Documentation</a>

*Project link: https://github.com/kosalaMaduwantha/atlas-insights*

### 2. Data Lake ETL
Suite of Python ETL services for extracting, transforming, and loading data into a unified Data Lake environment. The architecture is modular, metadata-driven, and cloud-agnostic, supporting seamless migration between storage and warehouse solutions.

**Highlevel architecture:**
![Data Lake ETL Architecture](</assets/images/architecture-data-project-alfa-Architecture.drawio.svg>)

🔧 **core module functionalities**

- **Data source support:** RDBMS (MySQL, Postgres, MSSQL, Oracle), flat files (CSV, TSV), and REST APIs.
- **Metadata service:** Unified metastore for source metadata, pipeline lineage, and error tracking.
- **Raw data storage:** Object storage (AWS S3 by default, easily migratable) for source files in CSV, JSON, TSV, XLSX, XML, or Parquet formats.
- **Processed data layers:**
  - *Landing storage*: Loads changed (delta/new) data.
  - *Base layer (ODS)*: Maintains structured, cleaned, and validated data identical to source.
  - *Analytics layer*: Denormalized, analytics-ready data (star/snowflake/galaxy models), with DW and aggregate sub-layers.
- **Target warehouse:** Processed and analytics layers built on Snowflake (migratable to Redshift, BigQuery, etc.).
- **ETL orchestration:** Apache Airflow for workflow management; hexagonal architecture (ports & adapters) for modularity and testability.
- **RDBMS to Data Lake ETL:**
  - Retrieves extraction configs from metadata service.
  - Supports incremental and full extraction with batching.
  - Processes, validates, and saves batches as CSV/Parquet for downstream loading.
  - Modular design enables easy extension to new platforms and data sources.

🛠️ **technology and approaches used**

- Python (ETL services)
- Apache Airflow (orchestration)
- AWS S3 (raw storage, pluggable)
- Snowflake (data warehouse, pluggable)
- Hexagonal architecture (ports & adapters)
- Metadata-driven pipeline management

<a href="/data-lake-etl-readme/" class="btn btn--primary">View Detailed Documentation</a>

*Project link: https://github.com/kosalaMaduwantha/data-lake-etl*
> **note**: Please request access to the private repo if needed.


### 3. Meta Config

This project is a RESTful API built using FastAPI, designed to manage metadata for data platforms. It provides endpoints for creating and retrieving metadata entities such as data sources, datasets, versions, schemas, columns, and data quality rules. The application is structured using the hexagonal architecture pattern (also known as ports and adapters), allowing for easy integration with various data storage solutions (e.g., MySQL, Neo4j) and providing a clear separation of concerns.

The API enables scalable data ingestion pipelines by maintaining comprehensive metadata about data sources, datasets, their schemas, versions, and quality rules. It uses Neo4j as the primary graph database for storing and querying metadata relationships.

**Core Module Functionalities:**
- Metadata Management: CRUD operations for data sources, datasets, versions, schemas, columns, and data quality rules.
- Graph Database Integration: Utilizes Neo4j to represent and manage complex relationships between metadata entities.
- RESTful API: Built with FastAPI, providing a user-friendly interface for interacting with metadata.
- Hexagonal Architecture: Implements ports and adapters pattern for flexibility and maintainability.
- Validation and Error Handling: Ensures data integrity and provides meaningful error messages.
- Documentation: API documentation using Swagger UI.

**Technology and Approaches Used:**
- Language & Framework: Python with FastAPI for building the RESTful API.
- Database: Neo4j for graph-based metadata storage; SQLAlchemy for relational database interactions (MySQL).
- Architecture: Hexagonal architecture for modularity and separation of concerns.

<a href="/meta-config-readme/" class="btn btn--primary">View Detailed Documentation</a>

*Project link: https://github.com/kosalaMaduwantha/meta-config*
> **note**: Please request access to the private repo if needed.

### 4. Contract Inspector

AI legal contract screener for rapid risk and clause assessment (LLM + RAG) This project accelerates contract reviews by grounding LLM outputs on the actual contract text. It ingests documents, retrieves the most relevant clauses, analyzes risks and deviations, answers targeted questions, and produces traceable, structured results for legal teams.

**Highlevel architecture:**
![Contract Inspector High-Level Architecture](</assets/images/Contract-nspact-RAG project-retriever.drawio.svg>)

🔧 **core module functionalities**

- RAG pipeline orchestration: entity extraction → retrieval → context construction → answer generation.
- Prompt processing: extract entities, build context, and generate answers.
- Retrieval options: BM25, vector, and hybrid searches against Weaviate collections; supports metadata filters sourced from metadata.yml.
- Indexing utilities: create/query Weaviate collections and add data.
- Exact match/BM25 utilities: BM25 indexing and scoring helpers.
- PDF processing: partition contract PDFs into chunks suitable for indexing.
- NER utilities: LLM based Named Entity Recognition.

🛠️ **technology and approaches used**

- Language & structure: Python - modular folders under with Adapter style separation of concerns.
- Vector store & search: Weaviate database for vector store - BM25, vector, and hybrid search modes with optional metadata filters.
- LLM integration: Service Provider Interface with an Ollama adapter.
- NLP & parsing: SpaCy models, PDF partitioning utilities; repository also includes dependencies for document processing (e.g., unstructured, pypdf, pdfminer.six).
- Config & metadata: Centralized configuration including Weaviate schema, system messages, and paths; metadata-driven filtering via metadata.yml.

<a href="/contract-inspect-readme/" class="btn btn--primary">View Detailed Documentation</a>

*Project link: https://github.com/kosalaMaduwantha/contract_inspect*  

### 5. Changed Data Capture (CDC) File Processor

File Change Detection and Streaming processor in Go that monitors text file modifications and publishes changes to message queues in real-time.

**Highlevel architecture:**
![CDC file processor High-Level Architecture](</assets/images/cdc-file-processor-general-architecture.drawio.svg>)

🔧 Core Features
- Real-time file change detection using SHA-256 hashing
- Thread-safe concurrent file processing
- Message streaming via RabbitMQ
- Persistent state management
- Structured logging

🛠️ Tech Stack
- Go 1.22
- RabbitMQ
- JSON for state persistence
- Logrus for logging

<a href="/cdc-file-processor-readme/" class="btn btn--primary">View Detailed Documentation</a>

*Project link: https://github.com/kosalaMaduwantha/go-changed-data-capture*

### 6. SSIS Data Warehouse for Formula 1 Championship

End-to-end ETL solution using SQL Server Integration Services (SSIS) to build a dimensional data warehouse for Formula 1 Championship analytics.

**Key Features:**
- Comprehensive ETL process for multi-source data integration
- Snowflake schema design for optimized query performance
- Support for slowly changing dimensions (SCD)

**Architecture Overview:**
![Architecture Diagram - Placeholder](</assets/images/sol-architecture-ssis-project.png>)

🔧 Core Module Functionalities
- ETL orchestration using SSIS
- Data transformation and cleansing
- Dimensional modeling for data warehouse
- Support for incremental data loads

🛠️ Technology and Approaches Used
- SQL Server Integration Services (SSIS) for ETL orchestration
- T-SQL for data transformation and cleansing
- Snowflake schema design for data warehouse
- Incremental data loading techniques

<a href="/ssis-warehouse-readme/" class="btn btn--primary">View Detailed Documentation</a>

*Project link: https://github.com/kosalaMaduwantha/Microsoft_BI_DataWarehouse_Project*


### 7. Bread Basket Analysis
A comprehensive web-based dashboard for visualizing and analyzing customer purchasing patterns in a bakery using **Association Rule Mining** and **Market Basket Analysis**.

**Highlevel architecture:**
*Interactive dashboard built with Dash (Plotly) and Python, leveraging the Apriori algorithm for association rule mining.*

🔧 **core module functionalities**

- Market Basket Analysis using the Apriori algorithm to discover frequent itemsets and association rules from transaction data.
- Interactive visualizations: bar charts (top-selling items), heatmaps (product associations), network graphs (item relationships), and dynamic tables for recommendations.
- Association rules explorer: filter and sort rules by confidence, lift, and support; view recommended pairings for any product.
- Configurable parameters: adjustable thresholds for lift and confidence, customizable number of top items/associations displayed.
- Efficient data loading with singleton pattern for performance and memory optimization.
- Modular page structure for maintainability and scalability.

🛠️ **technology and approaches used**

- Python 3.8+
- Dash (Plotly) for web UI and interactive visualizations
- mlxtend for Apriori algorithm and rule mining
- pandas for data manipulation
- scikit-learn for ML utilities
- Modular codebase: separate modules for data loading, configuration, utilities, and visualization
- Deployment-ready: Heroku configuration included (Procfile, runtime.txt)

<a href="/bread-basket-readme/" class="btn btn--primary">View Detailed Documentation</a>

*Project link: https://github.com/kosalaMaduwantha/bread-basket*


### 8. Air Passenger Satisfaction Prediction Dashboard
A web-based analytics dashboard for predicting and visualizing airline passenger satisfaction using machine learning and interactive data visualizations.

**Highlevel architecture:**
*Dash (Plotly) SPA with modular pages, SVM-based ML model, and centralized configuration for scalable analytics and real-time interactivity.*

🔧 **core module functionalities**

- Interactive data visualizations: real-time, responsive charts and graphs for multi-dimensional satisfaction analysis (age, class, gender, loyalty, travel type, service ratings)
- Machine learning: SVM classifier for binary satisfaction prediction, trained on demographic and service rating features
- Categorical and service rating analysis: dynamic histograms, bar charts, pie charts, and faceted views for deep insights
- Modular, maintainable codebase: MVC pattern, centralized config, and reusable components
- Data preprocessing: label encoding, aggregation, and efficient data loading
- Deployment-ready: Heroku and Docker support, production server with Gunicorn

🛠️ **technology and approaches used**

- Python 3.8+
- Dash (Plotly), Dash Bootstrap Components, Flask
- scikit-learn (SVM), pandas, numpy, mlxtend, statsmodels
- Plotly Express, matplotlib for visualizations
- Modular code: separate modules for config, utils, pages, and models
- Responsive UI: Bootstrap 5, Bootswatch LUX theme, custom CSS
- Production: Gunicorn, Flask-Compress, Docker, Heroku deployment

<a href="/air-passenger-pred-readme/" class="btn btn--primary">View Detailed Documentation</a>

*Project link: https://github.com/kosalaMaduwantha/air-passenger-sat*
