---
title: "Personal Projects"
permalink: /personal-projects/
layout: single
author_profile: true
sidebar:
  nav: "projects"
classes: wide
---

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
