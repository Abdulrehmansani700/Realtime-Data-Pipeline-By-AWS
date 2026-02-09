# 🏠 Real-Time Real Estate Data Pipeline: AWS, Airflow & Snowflake

This project implements a fully automated, production-grade data pipeline for **Real Estate (Redfin) data**. It leverages **Apache Airflow** for orchestration, **Python** for ETL, and **Snowflake** as the centralized data warehouse to enable real-time analytics.

---

## 🏗️ The Architecture Flow
The pipeline follows a sophisticated multi-stage process:
1. **Extraction:** Python scripts (orchestrated by Airflow on EC2) extract raw data from Redfin.
2. **Landing (S3):** Raw data is stored in the **Primary S3 Bucket**.
3. **Transformation:** A second Python process pulls raw data, cleans/transforms it, and pushes it to a **Transformed S3 Bucket**.
4. **Automated Loading:** S3 triggers **Snowpipe** to automatically ingest data into Snowflake.
5. **Insights:** Final data is visualized using **Power BI / AWS QuickSight**.

---

## 🛠️ Tech Stack & Tools
* **Orchestration:** Apache Airflow (Running on AWS EC2)
* **Languages:** Python (Pandas for Transformation), SQL
* **Cloud Infrastructure:** AWS (S3, EC2, IAM)
* **Data Warehouse:** Snowflake (EDW)
* **BI Tool:** Power BI / AWS QuickSight

---

## 🎯 Key Learning Milestones
- [x] **Automation with Airflow:** Setting up DAGs to automate extraction and load cycles.
- [x] **Cloud Compute:** Deploying and managing the pipeline on **AWS EC2**.
- [x] **Serverless Ingestion:** Implementing **Snowpipe** for event-driven data loading.
- [x] **Scalable Storage:** Architecting a multi-bucket strategy (Raw vs. Transformed).
- [x] **Business Intelligence:** Turning raw real estate metrics into visual dashboards.

---

## 💻 Technical Implementation Snippets

### 1. Airflow DAG Logic (Conceptual)
```python
with DAG('redfin_analytics_pipeline', start_date=datetime(2026, 2, 9)) as dag:
    extract_redfin_data = PythonOperator(task_id='extract', python_callable=extract_data)
    transform_redfin_data = PythonOperator(task_id='transform', python_callable=transform_data)
    
    extract_redfin_data >> transform_redfin_data
