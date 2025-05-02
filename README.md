# LMS Data Pipeline: Azure Data Lake to Microsoft Fabric

#### (⚠️ This notebook is designed to run in Microsoft Fabric or Azure Synapse Analytics using PySpark. GitHub may not render interactive elements properly. Please export the notebook as HTML to share results or run it directly in the Fabric environment.)

GitHub may not render interactive elements properly. Please export the notebook as HTML to share results or run it directly in the Fabric environment.


### Overview

This project demonstrates an end-to-end data pipeline for processing daily LMS data using Microsoft Fabric, with layered architecture (Bronze, Silver, Gold), upsert logic, and complete orchestration.

### Data Source
- LMS data files arrive daily in Azure Data Lake Storage (ADLS).
- Files are placed in the raw folder within a designated container.

### Bronze Layer (Raw to Landing)
- Each incoming file is stamped with a Processed Date column.
- A Fabric notebook reads data from the raw folder and moves it to the landing folder within ADLS.
- This processed data forms the Bronze layer in Fabric, and is ingested into a Bronze Lakehouse.

### Silver Layer (Landing to Structured Table)
- A second notebook moves data from the landing zone in ADLS to a structured table in the Silver Lakehouse.
- This table is cleaned and standardized for further transformations.

### Gold Layer (Business Logic and Enrichment)
- A third notebook applies business transformations:
- Calculates duration taken by each student to complete a course.
- Computes average marks.
- Flags whether the student completed the course within 90 days.
- The transformed data is saved in the Gold Lakehouse.

### Semantic Model
- A semantic model is created on top of the Gold layer using a notebook.
- The model includes:
- - Student Dimension
- - Course Dimension
- Fact Table (student-course performance metrics)

### Reporting
- A Power BI report is built using the semantic model, enabling rich insights on course completion, student performance, and trends.

### Orchestration
- A Data Factory pipeline orchestrates the full flow:
- Raw ingestion → Bronze → Silver → Gold → Semantic Model → Report
- Ensures data is processed and refreshed end-to-end automatically.

### Technologies Used
- Azure Data Lake Storage (Gen2)
- Microsoft Fabric (Lakehouse, Notebooks, Semantic Models)
- PySpark (for transformations)
- Power BI
- Data Factory (for orchestration)
