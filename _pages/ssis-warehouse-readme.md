---
title: "SSIS Data Warehouse - Formula 1 Championship ETL Project"
excerpt: "A comprehensive ETL solution using SSIS for Formula 1 Championship data warehousing"
permalink: /ssis-warehouse-readme/
toc: true
toc_sticky: true
---

## Project Overview

This project demonstrates the development of a complete ETL (Extract, Transform, Load) solution using SQL Server Integration Services (SSIS) for a Formula 1 Championship data warehouse. The solution processes transactional data from Kaggle into a structured data warehouse using a snowflake schema design.

### Dataset Source

The data is sourced from the Kaggle Formula 1 World Championship dataset:
- **Link**: [https://www.kaggle.com/rohanrao/formula-1-world-championship-1950-2020](https://www.kaggle.com/rohanrao/formula-1-world-championship-1950-2020)
- **Coverage**: Complete information on races, drivers, constructors, circuits, and qualifying results from 1950-2020

---

## Data Source Types and Structure

### Source Data Classification

The ETL solution processes two main source types:

#### 1. **TEXT Files**
- Constructors
- Countries

#### 2. **Database Tables (from CSV)**
- Circuits
- Constructor_Standings
- Driver
- Race
- Results

---

## Data Dictionary

### Source Tables Schema

#### **Circuits Table**

| Column Name | Data Type | Description |
|---|---|---|
| circuitId | int | Unique identifier for circuit |
| circuitRef | nvarchar | Reference code for circuit |
| name | nvarchar | Circuit name |
| location | nvarchar | Geographic location |
| countryID | nvarchar | Foreign key to country |
| lat | float | Latitude coordinate |
| lng | float | Longitude coordinate |
| alt | float | Altitude |
| url | nvarchar | Circuit URL reference |

#### **Country Table**

| Column Name | Data Type | Description |
|---|---|---|
| countryID | int | Unique identifier for country |
| country | nvarchar | Country name |

#### **Constructor_Standings Table**

| Column Name | Data Type | Description |
|---|---|---|
| constructorStandingsId | int | Unique identifier |
| raceId | int | Foreign key to race |
| constructorId | int | Foreign key to constructor |
| ConPoints | int | Championship points earned |
| ConPosition | int | Current standings position |
| ConPositionText | nvarchar | Text representation of position |
| ConWins | int | Number of race wins |

#### **Constructor Table**

| Column Name | Data Type | Description |
|---|---|---|
| constructorId | int | Unique identifier |
| constructorRef | nvarchar | Reference code |
| name | nvarchar | Constructor/Team name |
| nationality | nvarchar | Constructor nationality |
| url | nvarchar | Constructor URL reference |

#### **Driver Table**

| Column Name | Data Type | Description |
|---|---|---|
| driverId | int | Unique identifier |
| driverRef | nvarchar | Reference code |
| number | int | Driver race number |
| code | nvarchar | Three-letter driver code |
| forename | nvarchar | Driver first name |
| surname | nvarchar | Driver last name |
| gender | nvarchar | Gender identifier |
| dob | date | Date of birth |
| nationality | nvarchar | Driver nationality |
| address | nvarchar | Permanent address |
| email | nvarchar | Email address |
| url | nvarchar | Driver URL reference |

#### **Race Table**

| Column Name | Data Type | Description |
|---|---|---|
| raceId | int | Unique identifier |
| year | nvarchar | Championship year |
| round | int | Race round number |
| circuitId | int | Foreign key to circuit |
| name | nvarchar | Race name |
| date | date | Race date |
| time | time | Race start time |
| url | nvarchar | Race URL reference |

#### **Results Table**

| Column Name | Data Type | Description |
|---|---|---|
| resultId | int | Unique identifier |
| raceId | int | Foreign key to race |
| driverId | int | Foreign key to driver |
| constructorId | int | Foreign key to constructor |
| number | int | Driver starting number |
| grid | int | Grid position |
| position | int | Finishing position (numeric) |
| positionText | nvarchar | Finishing position (text) |
| positionOrder | int | Position ordering |
| points | int | Championship points awarded |
| laps | int | Number of laps completed |
| milliseconds | int | Race duration in milliseconds |
| fastestLap | int | Fastest lap number |
| rank | int | Fastest lap rank |
| fastestLapTime | time | Fastest lap time |
| fastestLapSpeed | decimal | Fastest lap speed |
| statusId | int | Race status indicator |

---

## Solution Architecture

### Architecture Overview

![Architecture Diagram - Placeholder](</assets/images/sol-architecture-ssis-project.png>)

### Data Pipeline Stages

The solution implements a multi-stage ETL process:

1. **Extraction** → Source Systems
2. **Staging Layer** → Data Cleansing & Validation
3. **Data Profiling** → Quality Assessment
4. **Transformation** → Business Logic & Aggregations
5. **Data Warehouse Loading** → Dimensional Model
6. **BI Layer** → Reports & Analytics

### Staging Layer

The following staging tables are created during the initial ETL phase:

- Circuit_staging
- Constructor_standings_staging
- Driver_staging
- Race_staging
- Results_staging
- Constructor_staging
- Countries_staging

**Profiling Activities:**
- Identify null values in columns
- Detect duplicate records
- Validate data types
- Determine necessary aggregations
- Assess data quality metrics

---

### Dimensional Model Approach

The data warehouse is designed using a **Snowflake Schema** to optimize query performance and storage efficiency.

```
                    ┌─────────────────┐
                    │  FactResults    │
                    │  (Grain: 1 row  │
                    │   per driver    │
                    │   per race)     │
                    └────────┬────────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
    ┌───▼──────┐     ┌──────▼──────┐     ┌──────▼──────┐
    │  DimRace │     │  DimDriver  │     │ DimConstructor
    └───┬──────┘     └─────────────┘     └──────────────┘
        │
    ┌───▼──────────┐
    │ DimCircuit   │
    └───┬──────────┘
        │
    ┌───▼──────────┐
    │ DimCountry   │
    └──────────────┘
```

### Fact & Dimension Tables

#### **FactResults (Fact Table)**

- **Grain**: One record per driver per race
- **Contains**: Race results and performance metrics
- **Foreign Keys**: Links to all dimension tables

#### **Dimension Tables**

| Dimension | Characteristics | Notes |
|---|---|---|
| DimCountry | Static | No references to other tables |
| DimCircuit | Static | References DimCountry (hierarchy) |
| DimRace | Static | References DimCircuit (hierarchy) |
| DimDriver | Slowly Changing | Type 2 - tracks address & email changes |
| DimConstructor | Static | Simple dimension |

### Slowly Changing Dimensions (SCD)

**DimDriver - Type 2 Implementation**

The Driver dimension tracks historical changes for:
- **Address** (permanent address) - Historical attribute
- **Email** (personal email) - Historical attribute
- **Code** (driver race code) - Changing attribute
- **Number** (driver race number) - Changing attribute

---

## ETL Development & Implementation

### ETL Package Structure

Two main SSIS packages orchestrate the ETL workflow:

#### **1. Sources_to_Staging_ETL_Package**

Extracts source data and loads into staging tables.

**Features:**
- Data flow tasks for each source
- Truncate event handlers to clear staging tables before load
- Handles both flat files (TXT) and database tables
- Lookup transformations where necessary

**Staging Tasks:**

![Staging ETL Flow - Placeholder](</assets/images/source-to-staging-flow.png>)

##### **Country Extraction** 
- **Source**: TEXT file
- **Destination**: Country_staging
- **Description**: Extracts country master data from flat file

##### **Circuit Extraction**
- **Source**: Database table
- **Destination**: Circuit_staging
- **Description**: Loads circuit information with geographic coordinates

##### **Constructor Extraction**
- **Source**: TEXT file
- **Destination**: Constructor_staging
- **Description**: Extracts constructor/team master data

##### **Driver Extraction**
- **Source**: Database table
- **Destination**: Driver_staging
- **Description**: Loads complete driver information

##### **Race Extraction**
- **Source**: Database table
- **Destination**: Race_staging
- **Description**: Loads race event details with timestamps

##### **Constructor Standings Extraction**
- **Source**: Database table
- **Destination**: Constructor_standings_staging
- **Description**: Loads championship standings information

##### **Results Extraction**
- **Source**: Database table
- **Destination**: Results_staging
- **Special Feature**: Added lookup column for race dates
- **Description**: Loads race result matrices

---

#### **2. Staging_to_DataWarehouse_ETL_Package**

Transforms staged data and loads into the data warehouse dimensional model.

![Data Warehouse ETL Flow - Placeholder](</assets/images/staging-wh.png>)

**Features:**
- Complex transformations with business logic
- Surrogate key lookups for referential integrity
- Derived columns for calculated fields
- Stored procedure destinations for upsert logic

**Processing Order (Dependency Chain):**

1. **Country Dimension** (First)
   - No transformations required
   - Direct load from staging

2. **Circuit Dimension** (Second)
   - Join with DimCountry for surrogate keys
   - Merge sort join on countryID
   - Map countryKey to Circuit

3. **Race Dimension** (Third)
   - Lookup DimCircuit surrogate keys
   - Join Race_staging with DimCircuit
   - Map circuitKey to Race

4. **Driver Dimension** (Fourth)
   - Replace null values (gender → "N", number → 0, code → first 3 letters of surname)
   - Implement SCD Type 2 logic
   - Handle historical tracking

5. **Constructor Dimension** (Fifth)
   - Transform null constructorRef values
   - Use first 3 letters of constructor name as default
   - Direct load with minimal transformation

6. **Results Fact Table** (Sixth/Last)
   - Join Results_staging and Constructor_standings_staging
   - Lookup all surrogate keys (date, driver, race, constructor)
   - Calculate average lap times
   - Apply derived columns for metrics

---

## ETL Task Transformations

### Transformation and Loading - Country Dimension

**Transformation Type**: Direct Load

```sql
-- No transformations applied
-- Data flows directly from Country_staging to DimCountry
-- Surrogate keys (CountrySK) generated automatically
```

**ETL Task**: Stored Procedure Load
- Procedure: `UpdateDimCountry`
- Action: Upsert (Insert if new, Update if exists)

---

### Transformation and Loading - Circuit Dimension

**Transformation Steps**:

1. **Sort** - Both tables sorted by joining attribute (countryID)
2. **Merge Join** - Inner join between DimCountry and Circuit_staging
   - Join Condition: `DimCountry.alternateCountryID = Circuit_staging.countryID`
3. **Column Selection** - Select circuit fields and countryKey (surrogate key)
4. **Stored Procedure Call** - `UpdateDimCircuit`

**ETL Task Diagram**:

![Circuit Transformation - Placeholder](</assets/images/circuit-dim-load.png>)

---

### Transformation and Loading - Race Dimension

**Transformation Steps**:

1. **Source**: Race_staging table
2. **Lookup DimCircuit**: 
   - Retrieve CircuitSK using race circuitId
   - Join: `Race_staging.circuitId = DimCircuit.alternateCircuitId`
3. **Execute OLEDB Command**: Call `UpdateDimRace` stored procedure
4. **Output**: Populated DimRace dimension

**ETL Task Diagram**:

![Race Transformation - Placeholder](</assets/images/race-table-load.png>)

---

### Transformation and Loading - Driver Dimension

**Transformation Steps**:

1. **Data Cleansing**:
   - Replace null gender values → "N"
   - Replace null number values → 0
   - Replace null code values → First 3 letters of surname

2. **SCD Type 2 Configuration**:
   - Designate historical attributes: address, email
   - Designate changing attributes: code, number
   - Enable effective dating and current record flags

3. **OLEDB Destination**: 
   - Configure dimension change tracking
   - Set primary key: driverId
   - Enable slowly changing dimension logic

**ETL Task Diagram**:

![Driver Transformation - Placeholder](</assets/images/driver-load.png>)

---

### Transformation and Loading - Constructor Dimension

**Transformation Steps**:

1. **Source**: Constructor_staging table
2. **Null Handling**:
   - Transform null `constructorRef` values
   - Use first 3 letters of constructor name as replacement
3. **Stored Procedure**: Call `UpdateDimConstructor`
4. **Output**: Populated DimConstructor dimension

**ETL Task Diagram**:

![Constructor Transformation - Placeholder](</assets/images/constructor-loading.png>)

---

### Transformation and Loading - Results Fact Table

**Transformation Steps**:

1. **Sort**: Both source tables sorted on join attributes
   - `Constructor_standings_staging`: Sort by raceId, constructorId
   - `Results_staging`: Sort by raceId, driverId

2. **Merge Join**: Left outer join
   - Join condition: `Results_staging` LEFT JOIN `Constructor_standings_staging`
   - On: raceId and constructorId

3. **Lookup dateKey**: Retrieve date surrogate key
   - Join on Race date

4. **Lookup driverKey**: Retrieve driver surrogate key
   - Join on driverId

5. **Lookup raceKey**: Retrieve race surrogate key
   - Join on raceId

6. **Lookup constructorKey**: Retrieve constructor surrogate key
   - Join on constructorId

7. **Derived Columns**: Calculate metrics
   - Average lap time = Total milliseconds / Total laps
   - Additional performance metrics

8. **Load to FactResults**: Insert transformed records

**ETL Task Diagram**:

![Results Transformation - Placeholder](</assets/images/result-fact-load.png>)

**Grain**: One record per driver per race

---

## Database Stored Procedures

### UpdateDimCountry

```sql
CREATE PROCEDURE [dbo].[UpdateDimCountry]
@alternateCountryID int,
@country nvarchar(50)
AS
BEGIN
    IF NOT EXISTS (
        SELECT CountrySK 
        FROM dbo.DimCountry 
        WHERE alternateCountryID = @alternateCountryID
    )
    BEGIN
        INSERT INTO dbo.DimCountry
        (alternateCountryID, country, InsertDate, ModifiedDate)
        VALUES (@alternateCountryID, @country, GETDATE(), GETDATE())
    END;
    
    IF EXISTS (
        SELECT CountrySK 
        FROM dbo.DimCountry 
        WHERE alternateCountryID = @alternateCountryID
    )
    BEGIN
        UPDATE dbo.DimCountry
        SET alternateCountryID = @alternateCountryID, 
            country = @country,
            ModifiedDate = GETDATE()
        WHERE alternateCountryID = @alternateCountryID
    END;
END;
```

### UpdateDimCircuit

```sql
CREATE PROCEDURE [dbo].[UpdateDimCircuit]
@alternateCircuitId int,
@circuitRef nvarchar(50),
@name nvarchar(50),
@location nvarchar(50),
@countryKey int,
@lat decimal(5,0),
@lng decimal(5,0),
@alt int
AS
BEGIN
    IF NOT EXISTS (
        SELECT circuitSK 
        FROM dbo.DimCircuit 
        WHERE alternateCircuitId = @alternateCircuitId
    )
    BEGIN
        INSERT INTO dbo.DimCircuit
        (alternateCircuitId, circuitRef, name, location, countryKey, 
         lat, lng, alt, InsertDate, ModifiedDate)
        VALUES (@alternateCircuitId, @circuitRef, @name, @location, @countryKey, 
                @lat, @lng, @alt, GETDATE(), GETDATE())
    END;
    
    IF EXISTS (
        SELECT circuitSK 
        FROM dbo.DimCircuit 
        WHERE alternateCircuitId = @alternateCircuitId
    )
    BEGIN
        UPDATE dbo.DimCircuit
        SET alternateCircuitId = @alternateCircuitId, 
            circuitRef = @circuitRef,
            name = @name, 
            location = @location, 
            countryKey = @countryKey, 
            lat = @lat, 
            lng = @lng, 
            alt = @alt,
            ModifiedDate = GETDATE()
        WHERE alternateCircuitId = @alternateCircuitId
    END;
END;
```

### UpdateDimRace

```sql
CREATE PROCEDURE [dbo].[UpdateDimRace]
@alternateRaceId int,
@year nvarchar(50),
@round int,
@circuitKey int,
@name nvarchar(50),
@date date,
@time time
AS
BEGIN
    IF NOT EXISTS (
        SELECT raceSK 
        FROM dbo.DimRace 
        WHERE alternateRaceId = @alternateRaceId
    )
    BEGIN
        INSERT INTO dbo.DimRace
        (alternateRaceId, year_, round_, circuitKey, name_, date_, time_, 
         InsertDate, ModifiedDate)
        VALUES (@alternateRaceId, @year, @round, @circuitKey, @name, @date, 
                @time, GETDATE(), GETDATE())
    END;
    
    IF EXISTS (
        SELECT raceSK 
        FROM dbo.DimRace 
        WHERE alternateRaceId = @alternateRaceId
    )
    BEGIN
        UPDATE dbo.DimRace
        SET alternateRaceId = @alternateRaceId, 
            year_ = @year, 
            round_ = @round, 
            circuitKey = @circuitKey, 
            name_ = @name, 
            date_ = @date, 
            time_ = @time,
            ModifiedDate = GETDATE()
        WHERE alternateRaceId = @alternateRaceId
    END;
END;
```

### UpdateDimConstructor

```sql
ALTER PROCEDURE [dbo].[UpdateDimConstructor]
@alternateConstructorId int,
@constructorRef nvarchar(50),
@name nvarchar(50),
@nationality nvarchar(50)
AS
BEGIN
    IF NOT EXISTS (
        SELECT constructorSK 
        FROM dbo.DimConstructor 
        WHERE alternateConstructorId = @alternateConstructorId
    )
    BEGIN
        INSERT INTO dbo.DimConstructor
        (alternateConstructorId, constructorRef, name, nationality, 
         InsertDate, ModifiedDate)
        VALUES (@alternateConstructorId, @constructorRef, @name, @nationality, 
                GETDATE(), GETDATE())
    END;
    
    IF EXISTS (
        SELECT constructorSK 
        FROM dbo.DimConstructor 
        WHERE alternateConstructorId = @alternateConstructorId
    )
    BEGIN
        UPDATE dbo.DimConstructor
        SET alternateConstructorId = @alternateConstructorId, 
            constructorRef = @constructorRef, 
            name = @name, 
            nationality = @nationality,
            ModifiedDate = GETDATE()
        WHERE alternateConstructorId = @alternateConstructorId
    END;
END;
```

---

## BI & Analytics Output

After the data warehouse is successfully populated, the following BI deliverables can be generated:

- **OLAP Analysis**: Multi-dimensional analysis on race results and driver performance
- **Reports**: Standard and ad-hoc reports on championship standings, race statistics
- **Data Visualization**: Dashboards showing season trends, driver rankings, constructor performance
- **Data Mining**: Predictive models for race outcomes and driver performance

---

## Key Features & Best Practices

✅ **Two-Layer Architecture**: Staging and Data Warehouse layers minimize impact to production  
✅ **Data Quality**: Profiling and validation gates before warehouse loading  
✅ **Referential Integrity**: Surrogate key mappings maintain data consistency  
✅ **Slowly Changing Dimensions**: Type 2 implementation for historical tracking  
✅ **Stored Procedures**: Upsert logic ensures idempotent loads  
✅ **Event Handlers**: Automated table truncation for repeatable executions  
✅ **Snowflake Schema**: Optimized for query performance and storage efficiency  

---

## Technical Stack

- **ETL Tool**: SQL Server Integration Services (SSIS)
- **Database**: SQL Server
- **Data Source**: Kaggle Formula 1 Championship Dataset
- **Schema Design**: Snowflake (Normalized dimensions)
- **SCD Implementation**: Type 2 (with effective dating)

---
