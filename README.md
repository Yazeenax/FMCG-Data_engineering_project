# End-to-End FMCG Data Engineering Pipeline Using AWS S3 and Databricks

## Project Overview

This project demonstrates the implementation of an end-to-end Data Engineering pipeline for an FMCG business scenario involving parent-child company data integration.

The project focuses on rebuilding the data pipeline for Sports Bar, a sports nutrition bar manufacturing company, which experienced pipeline failures resulting in the loss of approximately five months of historical data from its analytics environment.

Using AWS S3 and Databricks, the pipeline was rebuilt to support historical data recovery, incremental processing, data transformation, and integration with the parent company's existing Gold-layer datasets.

The solution follows the Medallion Architecture (Bronze, Silver, and Gold) and uses Delta Lake for reliable data processing and consolidated analytics.

## Business Problem

The parent company, Atlon (also referred to as Atlicon), already had an established Data Engineering and analytics environment.

However, its child company, Sports Bar, lacked a reliable and standardized data pipeline.

Due to pipeline failures:

- Approximately five months of historical data were lost from the analytics environment.
- Reliable downstream data processing was disrupted.
- The child company's analytical data needed to be recovered and integrated with the parent company's existing datasets.

### Business Objectives

- Rebuild the child company's data processing pipeline.
- Recover and backfill approximately five months of historical data.
- Implement incremental processing for incoming Fact Orders data.
- Establish Bronze, Silver, and Gold processing layers.
- Integrate the child company's Gold-layer data with the parent company's existing Gold-layer tables.
- Enable consolidated business reporting and conversational analytics.

## Technology Stack

| Technology | Purpose |
|---|---|
| AWS S3 | Cloud storage and data landing |
| Azure Databricks | Data engineering and processing |
| PySpark | Data transformation |
| Delta Lake | Reliable data storage and MERGE operations |
| SQL | Data querying and transformations |
| Databricks Workflows / Jobs | Pipeline orchestration |
| Databricks Widgets | Runtime parameterization |
| Databricks Utilities Notebook | Centralized configuration |
| Databricks Dashboards | Business analytics and visualization |
| Databricks AI/BI Genie | Conversational analytics |

## Solution Architecture

The project uses AWS S3 as the data landing and storage environment, while Azure Databricks handles data ingestion, transformation, and processing.

The solution follows the Medallion Architecture:

**AWS S3 → Bronze → Silver → Gold → Parent Company Gold Integration → Analytics**

The pipeline processes four major data domains:

- Customers
- Products
- Gross Price
- Fact Orders

Each domain has its own processing requirements and transformation logic.

<!-- Architecture diagram will be added here -->

## Medallion Architecture

### 1. Bronze Layer

The Bronze layer ingests raw source data from AWS S3.

Key responsibilities:

- Ingest raw source data.
- Preserve source information and ingestion metadata.
- Apply appropriate write strategies for full-load and staging processes.
- Store ingested data in Delta tables.

### 2. Silver Layer

The Silver layer performs data cleaning and business-specific transformations.

Key responsibilities:

- Handle duplicate records and data-quality issues.
- Standardize columns and data types.
- Correct relevant data inconsistencies.
- Prepare reliable datasets for downstream processing.

### 3. Gold Layer

The Gold layer prepares analytics-ready datasets.

Key responsibilities:

- Select business-relevant columns.
- Prepare datasets for business reporting.
- Integrate Sports Bar's Gold-layer data with the parent company's existing Gold tables using Delta Lake MERGE / UPSERT operations.
- Support consolidated analytics.

## Data Domains and Processing Notebooks

The project contains separate processing notebooks for the following business domains:

| Data Domain | Processing Layers |
|---|---|
| Customers | Bronze, Silver, Gold |
| Products | Bronze, Silver, Gold |
| Gross Price | Bronze, Silver, Gold |
| Fact Orders | Bronze, Silver, Gold, Incremental Processing |

A centralized Utilities notebook manages shared configuration, including catalog and schema information.

Databricks Widgets accept runtime parameters, making the notebooks configurable and reusable.

## Historical Data Backfill

One of the major requirements was recovering approximately five months of historical Sports Bar data.

The historical datasets were processed through the full-load pipeline.

The recovered data was processed through the required Bronze, Silver, and Gold layers to restore the analytical datasets.

## Incremental Fact Orders Processing

A separate incremental processing workflow was implemented for Fact Orders.

The workflow follows these steps:

1. New incoming order files are placed in the AWS S3 Landing folder.
2. Azure Databricks reads the newly arrived data.
3. The current incoming batch is written into a Delta staging table.
4. The staging table uses overwrite to replace the previous batch when appropriate.
5. The incoming data is processed through the downstream pipeline.
6. Successfully processed source files are moved from the Landing folder to the Processed folder.

This workflow helps prevent successfully processed source files from being repeatedly processed.

**Important:** Overwrite replaces the contents of the destination table. It does not independently perform incremental filtering or deduplication.

## Parent-Child Company Data Integration

The project integrates Sports Bar's Gold-layer datasets with the parent company's existing Gold-layer tables.

Delta Lake MERGE / UPSERT operations are used to support:

- Updating matching records.
- Inserting new records.

The objective is to establish consolidated analytical datasets for unified reporting across the parent and child companies.

## Databricks Widgets and Utilities

Databricks Widgets are used to accept runtime parameters, making the processing notebooks configurable and reusable.

A centralized Utilities notebook manages shared configuration, including catalog and schema information.

This approach helps maintain consistency across the processing notebooks.

## Workflow Orchestration

Databricks Workflows / Jobs are used to execute and orchestrate the processing pipelines.

The project includes:

- Historical full-load execution.
- Incremental Fact Orders processing.
- Downstream data processing.
- Validation of successful execution and file movement.

## Business Analytics

### Databricks Dashboards

Business dashboards were developed to present analytical insights based on the processed project datasets.

<!-- Add dashboard screenshots here -->

### Databricks AI/BI Genie

A Databricks AI/BI Genie agent was created to enable conversational analytics.

Users can interact with the analytical data by asking business-related questions using natural language.

<!-- Add Genie screenshots here -->

## Project Validation and Results

The end-to-end project was successfully implemented and tested.

Validation activities included:

- Successful execution of processing notebooks.
- Historical full-load processing.
- Incremental Fact Orders processing.
- Creation and upload of sample incremental data for January 1, 2026.
- Successful Databricks Job / Workflow execution.
- Verification of expected file movement from Landing to Processed.
- Completion of parent-child Gold-layer integration.
- Creation of business dashboards and an AI/BI Genie agent.

## Repository Structure

```text
fmcg-data-engineering-pipeline/
│
├── README.md
├── .gitignore
│
├── docs/
│   ├── architecture.md
│   ├── medallion-architecture.md
│   ├── historical-backfill.md
│   ├── incremental-loading.md
│   ├── parent-child-integration.md
│   └── workflow-orchestration.md
│
├── notebooks/
│   ├── utilities/
│   ├── customers/
│   ├── products/
│   ├── gross_price/
│   └── fact_orders/
│
├── architecture/
│   ├── end_to_end_architecture.png
│   ├── medallion_architecture.png
│   ├── incremental_workflow.png
│   └── company_integration.png
│
├── screenshots/
│   ├── pipeline_execution/
│   ├── dashboards/
│   ├── genie_agent/
│   └── data_validation/
│
├── sample_data/
│   ├── customers/
│   ├── products/
│   ├── gross_price/
│   └── fact_orders/
│
└── workflows/
    └── job_execution.md
```

## Setup and Execution

This repository documents the implementation of the completed Data Engineering project.

Execution requires access to the appropriate AWS S3 resources and Azure Databricks environment.

Before running the notebooks:

1. Configure the required AWS S3 access securely.
2. Configure the Databricks environment.
3. Set the appropriate catalog and schema parameters.
4. Configure notebook runtime parameters through Databricks Widgets.
5. Execute the relevant processing notebooks and workflows in the required sequence.

Detailed configuration and execution instructions will be added based on the sanitized notebook implementation.

## Skills Demonstrated

- End-to-end Data Engineering pipeline development
- AWS S3 data landing and storage
- Azure Databricks
- PySpark transformations
- SQL
- Delta Lake
- Medallion Architecture
- Historical data backfill
- Incremental data processing
- Delta Lake MERGE / UPSERT
- Data quality and cleansing
- Databricks Widgets
- Databricks Workflows / Jobs
- Parent-child data integration
- Business dashboards
- Conversational analytics using Databricks AI/BI Genie

## Future Improvements

Potential areas for future enhancement include:

- Enhanced automated data-quality validation.
- More comprehensive pipeline monitoring and alerting.
- Improved failure recovery and retry mechanisms.
- Automated deployment practices.
- Additional analytical datasets and business insights.

---

**Project Status:** Completed and successfully tested.

**Domain:** FMCG / Sports Nutrition Manufacturing

**Architecture:** AWS S3 + Databricks + Medallion Architecture
