#  NYC Taxi Data Engineering Project

Overview:
This project demonstrates an end-to-end data engineering pipeline using Azure Data Factory, Azure Data Lake, and Databricks, designed to extract, transform, and load (ETL) NYC Taxi trip data from a public API into a scalable analytics-ready format.
The solution follows a medallion architecture (Bronze → Silver → Gold) to ensure data quality, reusability, and performance for advanced analytics and Power BI visualization.
 Architecture


 
        ┌──────────────────────────┐
        │      NYC Taxi API        │
        └────────────┬─────────────┘
                     │
                     ▼
            ┌────────────────┐
            │  Azure Data     │
            │   Factory       │
            │ (Data Ingestion)│
            └────────┬────────┘
                     │
                     ▼
        ┌──────────────────────────┐
        │     Azure Data Lake      │
        │  ┌─────────┬─────────┐   │
        │  │ Bronze  │ Silver  │   │
        │  │  (Raw)  │ (Clean) │   │
        │  └─────────┴─────────┘   │
        └──────────┬───────────────┘
                   │
                   ▼
        ┌──────────────────────────┐
        │       Databricks         │
        │ (Transformation & Delta) │
        └──────────┬───────────────┘
                   │
                   ▼
        ┌──────────────────────────┐
        │         Gold Layer       │
        │ (Aggregated Analytics)   │
        └──────────┬───────────────┘
                   │
                   ▼
        ┌──────────────────────────┐
        │         Power BI         │
        │ (Dashboard & Insights)   │
        └──────────────────────────┘


## Tech Stack

### Layer	Tool	Purpose

Ingestion	Azure Data Factory: Extract data from NYC Taxi API

Storage	Azure Data Lake Gen2:	Store raw, clean, and curated data

Processing	Databricks (PySpark):	Data cleaning, transformation & aggregation
Format	Parquet & Delta	Optimized file formats for analytics

Visualization:	Power BI	Business insights & dashboards
Security	Azure Entra ID (Service Principal)	Secure data access via OAuth

## Medallion Architecture

#### Layer	Description	Example

🥉 Bronze	Raw data ingested from NYC API stored in original format.	bronze/trip2024/

🥈 Silver	Cleaned, validated, and structured data.	silver/trip2024data/

🥇 Gold	Aggregated business-level tables for analytics.	gold/trip_summary/

## 📊 Key Transformations

Converted timestamps (lpep_pickup_datetime, lpep_dropoff_datetime)
Handled missing and invalid data (e.g., passenger_count > 0)
Extracted trip year and month for trend analysis
Joined reference datasets (trip_type, trip_zone)
Aggregated data for average fare, trip count, and total revenue by zone
Business Impact

#### Data Reliability:
Ensures data consistency through multi-layered validation and schema enforcement.
Performance Optimization:
Delta Lake storage enables fast queries and time-travel features for version control.

#### Business Insights:
Gold-layer datasets power interactive Power BI dashboards to analyze:
Top pickup zones by revenue
Monthly trip trends
Average fare by borough
Vendor performance metrics


#### Tools & Technologies
Azure Data Factory — Data orchestration and ingestion

Azure Data Lake Gen2 — Data storage (Bronze, Silver, Gold)

Azure Databricks (PySpark) — Data processing and Delta Lake management

Azure Entra ID — Secure authentication via Service Principal

Power BI — Visualization and reporting

Outcome
Automated ETL pipeline from API → Data Lake → Gold Layer
End-to-end data lineage and traceability
Query-ready Delta tables for analytics
Dynamic ADF pipeline handling multiple months automatically
Power BI dashboard providing actionable insights
