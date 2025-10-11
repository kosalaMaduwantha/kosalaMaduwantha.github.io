---
title: "Personal Projects"
permalink: /personal-projects/
layout: single
classes: wide
author_profile: true
sidebar:
  nav: "projects"
---

### 1. Atlas Insights
Comprehensive, metadata‑driven ingestion and analytics framework for big data.

Data Ingestion module is implemented for three primary source types:

- File system (CSV ➜ Parquet on HDFS)
- Relational databases (MySQL / PostgreSQL / SQL Server ➜ Parquet on HDFS)
- Streaming (WebSocket JSON ➜ Kafka topics – foundation for near‑real‑time ingestion)

Built with Python, PyArrow, FastAPI, and Kafka; designed to standardize how raw operational data is landed into an analytics‑friendly lake/warehouse zone (HDFS Parquet) using a **single metadata contract**.

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

### 2. Contract Inspector

AI legal contract screener for rapid risk and clause assessment (LLM + RAG) This project accelerates contract reviews by grounding LLM outputs on the actual contract text. It ingests documents, retrieves the most relevant clauses, analyzes risks and deviations, answers targeted questions, and produces traceable, structured results for legal teams.

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

**Project link:** https://github.com/kosalaMaduwantha/contract_inspectAI legal 


### 3. Changed Data Capture (CDC) File Processor

File Change Detection and Streaming processor in Go that monitors text file modifications and publishes changes to message queues in real-time.

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

Project link: https://github.com/kosalaMaduwantha/go-changed-data-captureFile 

