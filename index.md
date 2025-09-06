---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: home
author_profile: true
---

## About

Data Engineer, having 3 plus years of industrial experience specialized in designing and implementing scalable server-side applications and data ingestion pipelines. Proficient in Python, with experience in API development, third-party service integration, and building scalable data pipelines from various data sources. Adept at learning new technologies and applying them effectively to create high-performance, maintainable solutions.

## Interests

- Data pipeline development
- ETL/ELT processes
- AI/ML model deployment 
- Cloud data platforms 
- Big Data technologies 
- SQL & NoSQL databases 

## Skills

- Programming: Python, Java, JavaScript, SQL, Bash
- Data: Spark, Hadoop, Airflow, Kafka, Snowflake
- Cloud: AWS (EC2, S3, SQS, ECR, EKS, Lambda, CF (CloudFormation)), Azure (Blob storage, Service bus, Key vault, AKS)
- Version Control: Git, GitHub
- Containerization: Docker, Kubernetes

---


## Work Experience

### Data Engineer BlackSwan Technologies | Feb 2023 - Present

#### Projects:

**1. Data Fabric and Knowledge Graph for fin-tech customer i.e. ING and Deutscher bank**

- Worked on developing Restful microservices using Python flask which initiates data ingestion jobs in the knowledge
mesh.
- Worked on enhancing source data invocation services which extract data using GraphQL based wrappers.
- Redesigned and implemented Job tracking service for a distributed micro services.
- Created a configurable test suite to evaluate performance and integrity of a queue-based data processing application.
- Created a library which process queue messages asynchronously.
- Followed the Git Flow branching model for source code management.

**2. Web Scrapers**

- Developed online data extraction applications from source websites(Used html parser libraries and selenium for interactive web scraping).
- Integrated web scraper data using a pipeline(set of microservices) to a domain specific schema.
- Deployed applications on AWS CloudFormation stacks.
- Developed Java-based SOAP client to extract data, transform it into a JSON structure and map it to a common domain-compliant schema.

**3. Data Screening**

- Built an application(microservice) that processes files on a file server.
- The processing involves parsing XML files in batches, transforming the data into a domain-specific format, and uploading the transformed data to an Azure Blob container for the downstream consumption.

### Intern - Data Engineer Wiley | Jan 2022 - Jan 2023

- Set up metadata-driven data pipelines to bring data from various data sources.
- Worked with multiple data sources, bring the data together into a data lake for easier access and analysis.
- Monitored data pipelines, fixing issues right away to prevent disruptions.
- Moved data workflows from Tidal to Apache Airflow, making the automation process simpler and faster.
- Leveraged a range of technologies including Python, Bash, AWS S3, Apache Airflow, Snowflake Cloud Datawarehouse, MySQL and MSSQL to achieve project objectives.


## Personal Projects 
### 1. Contract Inspector

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

Skills: Weaviate · Large Language Model Operations (LLMOps) · Retrieval-Augmented Generation (RAG) · Information Retrieval Systems · Python (Programming Language) · Ollama

### 2. Changed Data Capture (CDC) File Processor

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

Skills: Go (Programming Language) · RabbitMQ · CDC

## Contact

- Email: [your.email@example.com]
- LinkedIn: [Your LinkedIn Profile]
- GitHub: [Your GitHub Profile]
# kosalaMaduwantha.github.io
portfolio site 
