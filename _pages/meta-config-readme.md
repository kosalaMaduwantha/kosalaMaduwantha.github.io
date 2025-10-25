---
title: "Meta Config Readme"
permalink: /meta-config-readme/
layout: single
classes: wide
# author_profile: true
---

# Metadata Management for Data Platforms

## Overview

This project is a RESTful API built using FastAPI, designed to manage metadata for data platforms. It provides endpoints for creating and retrieving metadata entities such as data sources, datasets, versions, schemas, columns, and data quality rules. The application is structured using the hexagonal architecture pattern (also known as ports and adapters), allowing for easy integration with various data storage solutions (e.g., MySQL, Neo4j) and providing a clear separation of concerns.

The API enables scalable data ingestion pipelines by maintaining comprehensive metadata about data sources, datasets, their schemas, versions, and quality rules. It uses Neo4j as the primary graph database for storing and querying metadata relationships.

## Features

- **RESTful API**: Built with FastAPI for high-performance async web APIs.
- **Hexagonal Architecture**: Clean separation of domain logic, application services, and infrastructure.
- **Graph Database**: Uses Neo4j for efficient storage and querying of metadata relationships.
- **Data Quality Management**: Supports defining and managing data quality rules.
- **Schema Management**: Tracks schema versions and column definitions.
- **Version Control**: Maintains version history for datasets.
- **Docker Support**: Includes Docker Compose setup for Neo4j database.

## Prerequisites

Before running this application, ensure you have the following installed:

- **Python 3.8+**: The application is built with Python.
- **Neo4j Database**: Version 4.x or 5.x for metadata storage.
- **Docker and Docker Compose**: For running Neo4j in a container (optional but recommended).

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/kosalaMaduwantha/meta-config.git
   cd meta-config
   ```

2. **Create a virtual environment** (recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up Neo4j**:
   - Using Docker Compose (recommended):
     ```bash
     cd meta
     docker-compose up -d
     ```
     This starts Neo4j on `localhost:7687` with no authentication.

   - Or install Neo4j manually and ensure it's running on the configured port.

## Configuration

The application uses environment variables for configuration. Create a `.env` file in the root directory or set environment variables:

```bash
# Database Configuration (for future extensions)
DB_USERNAME=your_db_username
DB_PASSWORD=your_db_password
DB_HOST=localhost
DB_PORT=5432
DB_NAME=your_db_name

# Neo4j Configuration
NEO4J_URI=neo4j://localhost:7687
NEO4J_USER=  # Leave empty for no auth
NEO4J_PASSWORD=  # Leave empty for no auth
```

If using the provided Docker Compose setup, Neo4j runs without authentication, so leave `NEO4J_USER` and `NEO4J_PASSWORD` empty.

## Project Structure

```
meta-config/
├── config.py                           # Configuration settings and environment variables
├── neo4j_repository_documentation.md   # Additional Neo4j-specific documentation
├── README.md                           # This file
├── requirements.txt                    # Python dependencies
├── meta/
│   └── docker-compose.yml              # Docker Compose for Neo4j setup
├── src/
│   ├── main.py                         # FastAPI application entry point
│   ├── application/
│   │   ├── ports/
│   │   │   ├── __init__.py
│   │   │   ├── api/
│   │   │   │   └── meta_service_api.py # Abstract API interface
│   │   │   └── spi/
│   │   │       ├── __init__.py
│   │   │       └── meta_spi.py         # Service Provider Interface
│   │   └── services/
│   │       ├── __init__.py
│   │       └── meta_service.py         # Business logic implementation
│   ├── domain/
│   │   ├── __init__.py
│   │   ├── request_models.py           # Pydantic models for API requests
│   │   └── response_models.py          # Response model definitions
│   └── infrastructure/
│       ├── __init__.py
│       ├── repositories/
│       │   ├── __init__.py
│       │   ├── mysql_repository.py     # MySQL repository implementation (future)
│       │   ├── neo4j_repository.py     # Neo4j repository implementation
│       │   └── model/
│       │       ├── db_models.py        # Database models
│       │       └── pydantic_models.py  # Additional Pydantic models
│       └── rest_adapter/
│           ├── __init__.py
│           ├── meta_controller.py      # FastAPI route definitions
│           └── response_messages.py    # HTTP response messages
└── tests/
    └── __init__.py                     # Test directory (tests to be added)
```

## Architecture Overview

This project follows the **Hexagonal Architecture** (Ports and Adapters) pattern:

- **Domain Layer** (`src/domain/`): Contains core business models and rules. Defines the entities like `DataSource`, `Dataset`, etc., using Pydantic for validation.

- **Application Layer** (`src/application/`):
  - **Ports**: Define interfaces for external interactions.
    - **API** (`ports/api/`): Abstract interfaces that the application provides.
    - **SPI** (`ports/spi/`): Abstract interfaces for external services the application needs.
  - **Services** (`services/`): Implement business logic and orchestrate domain operations.

- **Infrastructure Layer** (`src/infrastructure/`):
  - **Repositories**: Concrete implementations of data persistence (currently Neo4j).
  - **REST Adapter**: FastAPI controllers that adapt HTTP requests to application services.

This architecture ensures:
- **Testability**: Easy to mock external dependencies.
- **Flexibility**: Can swap databases or frameworks without changing core logic.
- **Maintainability**: Clear separation of concerns.

## Running the Application

1. **Ensure Neo4j is running** (via Docker Compose or manual setup).

2. **Set environment variables** or create `.env` file as described in Configuration.

3. **Run the application**:
   ```bash
   python src/main.py
   ```
   Or using uvicorn directly:
   ```bash
   uvicorn src.main:app --reload --host 0.0.0.0 --port 8000
   ```

4. **Access the API**:
   - API Documentation: http://localhost:8000/docs (Swagger UI)
   - Alternative Docs: http://localhost:8000/redoc

## API Endpoints

The API provides the following endpoints for metadata management:

### Data Sources

- **POST /create_source**
  - Create a new data source.
  - Request Body: `DataSource` model
  - Response: Success/failure message

- **GET /get_source/{source_id}**
  - Retrieve a data source by ID.
  - Path Parameter: `source_id` (string)
  - Response: `DataSource` object or error

### Datasets

- **POST /create_dataset**
  - Create a new dataset.
  - Request Body: `Dataset` model
  - Response: Success/failure message

- **GET /get_dataset/{dataset_id}**
  - Retrieve a dataset by ID.
  - Path Parameter: `dataset_id` (string)
  - Response: `Dataset` object or error

### Data Versions

- **POST /create_data_version**
  - Create a new data version.
  - Request Body: `DataVersion` model
  - Response: Success/failure message

### Schemas

- **POST /create_schema**
  - Create a new schema.
  - Request Body: `Schema` model
  - Response: Success/failure message

### Columns

- **POST /create_columns**
  - Create multiple columns for a schema.
  - Request Body: Array of `Column` models
  - Response: Success/failure message

### Data Quality Rules

- **POST /create_data_quality_rule**
  - Create a new data quality rule.
  - Request Body: `DataQualityRule` model
  - Response: Success/failure message

### Data Models

All request models are defined in `src/domain/request_models.py`:

- **DataSource**: Represents a data source with connection details.
- **Dataset**: Represents a dataset belonging to a source.
- **DataVersion**: Tracks versions of datasets with metadata.
- **Schema**: Describes dataset schema with versioning.
- **Column**: Represents individual columns in a schema.
- **DataQualityRule**: Defines data quality validation rules.

Example request for creating a data source:

```json
{
  "source_id": "src_001",
  "name": "Customer Database",
  "type": "postgresql",
  "connection_details": "host=localhost port=5432 dbname=customers",
  "created_at": "2023-10-15T10:00:00Z",
  "owner": "data_team",
  "status": "active"
}
```

## Testing

Currently, the test suite is minimal. To run existing tests:

```bash
pytest
```

Future enhancements will include comprehensive unit and integration tests.

## Development

### Adding New Features

1. Define domain models in `src/domain/request_models.py`.
2. Add abstract methods to `src/application/ports/api/meta_service_api.py`.
3. Implement business logic in `src/application/services/meta_service.py`.
4. Add repository methods to SPI and implement in concrete repositories.
5. Create FastAPI routes in `src/infrastructure/rest_adapter/meta_controller.py`.

### Database Migrations

For Neo4j, schema constraints are managed programmatically. The repository handles node creation and relationships.

## Future Enhancements

- Add MySQL repository implementation.
- Add data lineage tracking.
- Enhanced data quality monitoring.
- API versioning.

