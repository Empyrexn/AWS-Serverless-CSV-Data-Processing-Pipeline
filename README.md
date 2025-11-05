# Serverless CSV Data Processing Pipeline on AWS

> **Disclaimer:**  
> This project was built as part of a cloud data engineering learning environment for demonstrating serverless data pipelines on AWS.  
> All datasets used do not contain any sensitive or proprietary information.

---

## Overview

This project implements a **serverless data pipeline** on **Amazon Web Services (AWS)** for automated ingestion, transformation, and visualization of CSV data files.  

When a CSV file is uploaded to a raw data S3 bucket, the pipeline is automatically triggered to clean, transform, and visualize the data using AWS-native services such as **Lambda**, **Glue**, and **QuickSight**.  

The entire process eliminates the need for traditional servers or manual ETL workflows, showcasing a scalable, event-driven architecture.

---

## Architecture Diagram

![Data Pipeline Architecture](https://github.com/user-attachments/assets/e871d639-3eda-4170-b7c8-9911dfbfb7d6)

*Figure 1: Serverless data pipeline integrating S3, Lambda, Glue, and QuickSight.*

### Workflow Summary

1. **Data Ingestion:**  
   CSV files are uploaded to the **`csv-raw-data`** S3 bucket, initiating the pipeline.

2. **Lambda Preprocessing:**  
   An **AWS Lambda function** is triggered to clean and preprocess data (e.g., filtering, reformatting).  
   Processed data is stored in **`csv-processed-data`** bucket.

3. **Schema Detection:**  
   An **AWS Glue Crawler** scans processed data to infer schema and updates the **Glue Data Catalog**.

4. **Transformation and Loading:**  
   An **AWS Glue Job** performs detailed ETL — transforming and writing final data to the **`csv-final-data`** bucket.

5. **Visualization:**  
   **Amazon QuickSight** connects to the transformed dataset for **interactive dashboards** and **data visualization**.

---

## Key Components 🔧

### 1. Amazon S3
- **Role:** Central data lake for storing raw, processed, and final CSV data.
- **Buckets Used:**
  - `csv-raw-data` → Raw uploaded files.
  - `csv-processed-data` → Cleaned/intermediate data.
  - `csv-final-data` → Transformed, analytics-ready data.
- **Features:** Event notifications trigger Lambda upon new uploads.

---

### 2. AWS Lambda
- **Role:** Serverless compute function for preprocessing data automatically upon upload.
- **Functionality:**
  - Filters, validates, and standardizes CSV files.
  - Moves cleaned output to `csv-processed-data` bucket.
- **Trigger:** S3 event from `csv-raw-data`.
- **Security:** IAM Role grants limited permissions to S3 buckets.

---

### 3. AWS Glue
- **Role:** Managed ETL (Extract, Transform, Load) service for large-scale data processing.
- **Components:**
  - **Glue Crawler:** Detects schema of processed data.
  - **Glue Data Catalog:** Central metadata repository for table definitions.
  - **Glue Job:** Executes transformation logic (joins, type casting, aggregation, etc.).
- **Output:** Writes analytics-ready data to `csv-final-data`.

---

### 4. Amazon QuickSight
- **Role:** Business intelligence and data visualization tool.
- **Functionality:**
  - Connects to AWS Glue Data Catalog or S3 datasets.
  - Builds interactive dashboards and charts.
  - Supports real-time updates as data pipelines refresh.
- **Example Use Case:**  
  Visualize KPIs such as sales by region, user trends, or error logs.

---

### 5. AWS IAM
- **Role:** Secure access control across AWS resources.
- **Functionality:**
  - Assigns least-privilege permissions to Lambda, Glue, and QuickSight.
  - Enforces encryption and access logging for compliance.

---

## Pipeline Flow

1. **Upload CSV → S3:**  
   User uploads CSV into `csv-raw-data` bucket.

2. **Trigger → Lambda:**  
   S3 event triggers Lambda to preprocess the file.

3. **Lambda → Processed S3:**  
   Cleaned CSV stored in `csv-processed-data`.

4. **Glue Crawler → Data Catalog:**  
   Crawler scans data and infers schema.

5. **Glue Job → Transformation:**  
   Job performs ETL and saves output in `csv-final-data`.

6. **QuickSight → Dashboard:**  
   QuickSight reads from final data and generates live visual dashboards.

---

## Objectives

- **Automation:** Fully serverless and event-driven data pipeline.
- **Scalability:** S3 and Glue scale seamlessly with data volume.
- **Maintainability:** No manual servers, simple to extend for multiple datasets.
- **Security:** IAM roles ensure fine-grained access and data encryption.
- **Analytics:** Real-time dashboards for insights using Amazon QuickSight.

---

## Security Considerations

- **IAM Policies:** Granular permissions for Lambda, Glue, and S3.
- **Encryption:** S3 buckets use SSE (Server-Side Encryption) for data at rest.
- **Data Privacy:** All datasets anonymized or publicly available.
- **Auditability:** S3 access logs and CloudTrail for operational visibility.

---

## Steps to Reproduce

1. **Setup AWS Environment**
   - Create S3 buckets:  
     `csv-raw-data`, `csv-processed-data`, `csv-final-data`
   - Configure IAM roles and policies for Lambda, Glue, and QuickSight.

2. **Deploy Lambda Function**
   - Write preprocessing logic (e.g., filtering nulls, formatting dates).
   - Configure event trigger on `csv-raw-data` S3 bucket.

3. **Create AWS Glue Resources**
   - Run **Glue Crawler** on `csv-processed-data`.
   - Build a **Glue Job** for transformations and output to `csv-final-data`.

4. **Visualize in QuickSight**
   - Connect QuickSight to Glue Data Catalog or S3 dataset.
   - Create interactive dashboards and charts.


## Conclusion

This project demonstrates a **fully serverless, automated, and scalable data processing pipeline** on AWS.  
By leveraging **S3**, **Lambda**, **Glue**, and **QuickSight**, it achieves efficient **data ingestion**, **transformation**, and **visualization** — all without managing infrastructure.

![image](https://github.com/user-attachments/assets/93bc0a32-ca03-45ba-b4fd-39d28cf45241)

![image](https://github.com/user-attachments/assets/1d2c492c-8c32-4418-8da7-567c40541d38)
