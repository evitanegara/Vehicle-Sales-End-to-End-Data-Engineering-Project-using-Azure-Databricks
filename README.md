#  Vehicle Sales End-to-End Data Engineering Project using Azure & Databricks

## Project Background
This project showcases the design and implementation of a scalable, modern data engineering solution built entirely on the Microsoft Azure ecosystem. The goal is to process, transform, and analyze vehicle sales data efficiently, from raw ingestion to an analytics ready model andenabling data-driven decision making for sales performance insights.

The project demonstrates how to:
- Automate data ingestion and incremental updates.
- Apply the Medallion Architecture (Bronze → Silver → Gold) for data transformation.
- Design a star schema for optimized analytics.
- Build an integrated reporting layer using Power BI.

## End-to-End Architecture

The entire pipeline is designed to process and transform vehicle sales data in a modern cloud environment using Azure services.  
It follows a clear flow from raw data ingestion to business-ready analytics.

### Architecture Flow
GitHub → Azure Data Factory → Azure SQL Database → Azure Data Lake Gen2 → Azure Databricks → Power BI

### Component Overview

| Stage | Azure Service | Description |
|--------|----------------|-------------|
| Ingestion | Azure Data Factory | Orchestrates data extraction and pipeline automation. |
| Staging | Azure SQL Database | Stores raw data and manages watermark logic for incremental loads. |
| Storage | Azure Data Lake Gen2 | Acts as the main data repository, structured in Bronze, Silver, and Gold zones. |
| Transformation | Azure Databricks | Cleans, enriches, and models data using Delta Lake. |
| Visualization | Power BI | Connects to the Gold layer for reporting and interactive dashboards. |

# Azure Data Factory (ADF) Pipeline

The Azure Data Factory pipeline (adf-vehicle-ita) automates data ingestion and orchestrates each step of the process.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e47fc2aa-dbb6-4711-9771-c4f4f217464b" alt="ADF Pipeline Screenshot" width="800"/>
</p>

### Pipeline Flow
1. Lookup (last_load): retrieves the previous successful load date  
2. Lookup (current_load): identifies the latest batch of data  
3. Copy Activity: ingests incremental vehicle sales data from GitHub into Azure SQL Database, then to the Bronze container  
4. Stored Procedure: updates the watermark table after successful load  
5. Notebook Activity: triggers the Databricks Silver_Notebook for further processing

### Features
- Incremental data loading using watermark logic  
- End-to-end pipeline automation  
- Integration between SQL, Data Lake, and Databricks  

---

## Azure Data Lake Structure

The Azure Data Lake (vehicleitadatalake) serves as the core data storage layer, following the Medallion Architecture for structured organization.

| Layer | Container | Description |
|--------|------------|-------------|
| Bronze | bronze | Raw data ingested directly from the source |
| Silver | silver | Cleaned, validated, and transformed data |
| Gold | gold | Aggregated and modeled data for analytics |
| Logs / Metastore | $logs, unitymetastore | Stores logs and Delta metadata for Databricks |

---

## Azure Databricks Workflow

The Azure Databricks workspace (vehicledatabrick) handles all data transformations using Delta Lake for reliability and ACID compliance.

<p align="center">
  <img src="https://github.com/user-attachments/assets/fcf06c07-a83b-44cc-8476-2bd75bcf6262" alt="Databricks Workflow Screenshot" width="800"/>
</p>

### Transformation Flow

Bronze → Silver:
- Remove duplicates and null values  
- Standardize column formats and naming conventions  
- Validate data consistency and structure
  
Silver → Gold:
- Build Fact_Sales table with all sales transactions  
- Create Dim_Branch, Dim_Dealer, Dim_Model, and Dim_Date tables  
- Join and enrich data for analytics and reporting  

## Data Model – Star Schema

The final Gold layer is organized using a star schema design to optimize query performance and simplify reporting in Power BI.

| Table | Type | Description |
|--------|------|-------------|
| Fact_Sales | Fact | Contains all vehicle sales transactions with metrics like units sold, price, and branch |
| Dim_Branch | Dimension | Branch information such as branch name, region, and location |
| Dim_Dealer | Dimension | Dealer details including ID, name, and associated branch |
| Dim_Model | Dimension | Vehicle model details such as make, type, and category |
| Dim_Date | Dimension | Calendar dimension supporting time-based analysis |

## Power BI Visualization

The Gold layer is connected to Power BI, enabling interactive visualizations and data analysis.

Key insights available in Power BI include:
- Total vehicle sales by branch and dealer  
- Monthly and yearly sales trends  
- Top-performing vehicle models  
- Regional and branch-level performance  
- Dealer contribution and efficiency analysis  

## Key Learnings

- Built a complete data engineering pipeline with Azure Data Factory  
- Implemented the Medallion Architecture for structured data processing  
- Applied Delta Lake for versioning and ACID compliance  
- Created a dimensional model to support business analytics  
- Connected Power BI to Databricks for real-time insights  
- Applied Azure best practices for scalability, governance, and performance  

## Technology Stack

| Category | Tools / Services |
|-----------|------------------|
| Cloud Platform | Microsoft Azure |
| Orchestration | Azure Data Factory (V2) |
| Storage | Azure Data Lake Gen2 |
| Processing | Azure Databricks (Delta Lake) |
| Database | Azure SQL Database |
| Visualization | Power BI |
| Version Control | GitHub |
| File Format | Delta, Parquet, CSV |


## Contact
For questions or collaboration:
Email: evitanegara@gmail.com  
LinkedIn: https://www.linkedin.com/in/evitanegara/  


---



