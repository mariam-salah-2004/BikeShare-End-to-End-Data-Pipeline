# Azure Data Warehouse Migration: PostgreSQL to Synapse Analytics 🚀

## Project Overview
This project demonstrates an end-to-end data engineering pipeline migrating transactional data from **PostgreSQL** to an analytical **Star Schema** in **Azure Synapse Analytics**. It follows the Medallion Architecture (Bronze to Gold) to transform raw operational data into actionable business insights.

## Architecture & Workflow
1. **Source**: Transactional data (Riders, Payments, Stations, Trips) hosted on Azure Database for PostgreSQL.
2. **Ingestion**: Python scripts (using `psycopg2`) to extract and prepare data as CSVs.
3. **Storage (Staging)**: Azure Data Lake Storage (ADLS Gen2) serving as the Bronze/Landing zone.
4. **Processing (Serverless)**: Created **External Tables** using Synapse Serverless SQL Pool for immediate data exploration without ingestion costs.
5. **Analytics (Dedicated SQL Pool)**: Performed final ELT transformations to populate a high-performance Star Schema.

## Technical Implementation
- **Data Modeling**: Implemented a Star Schema with 2 Fact tables and 4 Dimension tables.
- **Optimization**: 
    - Used `CLUSTERED COLUMNSTORE INDEX` for efficient analytical query performance.
    - Applied `HASH` distribution on primary keys (e.g., `trip_id`, `payment_id`) to optimize parallel processing and joins.
- **Complex Transformations**: 
    - Calculated `duration_trip` using `DATEDIFF`.
    - Derived `rider_age` from birthdates using T-SQL logic.
    - Built a comprehensive `Calendar` dimension from scratch for time-series analysis.

## Tech Stack
* **Cloud**: Azure Synapse Analytics, ADLS Gen2.
* **Database**: PostgreSQL, Dedicated SQL Pool.
* **Languages**: SQL (T-SQL), Python.
* **Tools**: VS Code, Azure Storage Explorer.
