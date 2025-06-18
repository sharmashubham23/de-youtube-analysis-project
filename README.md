# AWS YouTube Trending Data Engineering Project

## 🌟 Project Overview

This repository showcases an **end-to-end data engineering pipeline** built on **Amazon Web Services (AWS)**. The project focuses on collecting, processing, storing, and analyzing YouTube trending video data from Kaggle. It demonstrates a robust, serverless-first approach to transforming raw, semi-structured (JSON) and structured (CSV) data into an analytics-ready format (Apache Parquet) within a scalable data lake.

The ultimate goal is to provide actionable insights into YouTube content trends, viewer engagement, and regional popularity through an interactive dashboard, highlighting a complete data journey from raw ingestion to powerful visualization.

## 🚀 Architecture

The pipeline follows a modern data lake architecture, leveraging key AWS services for each stage:

1.  **Data Ingestion (Source: Kaggle Dataset):** Raw JSON and CSV files are uploaded to an **Amazon S3 Raw Data Zone**.
2.  **Event-Driven ETL (for JSON):**
    * New JSON file uploads to S3 trigger an **AWS Lambda function**.
    * This Lambda function, utilizing `awswrangler` and `pandas`, reads the JSON, flattens its nested structure, and writes the transformed data as **Parquet** to the **S3 Cleaned Data Zone**.
    * It simultaneously registers/updates the schema in the **AWS Glue Data Catalog**.
3.  **Batch ETL (for CSV):**
    * An **AWS Glue ETL job** (Apache Spark) reads CSV files from the S3 Raw Data Zone.
    * It performs transformations (e.g., filtering by region, data type handling) and writes the cleaned data as **partitioned Parquet files** to the S3 Cleaned Data Zone.
    * This job also manages schema and partition updates in the **AWS Glue Data Catalog**.
4.  **Data Cataloging:** **AWS Glue Crawlers** are initially used to discover schemas of both raw and cleaned data, maintaining a central metadata repository in the Glue Data Catalog.
5.  **Querying:** **Amazon Athena** connects to the Glue Data Catalog, allowing for powerful, serverless SQL queries directly on the Parquet data in S3.
6.  **Visualization:** **Amazon QuickSight** integrates with Athena to create an interactive dashboard, enabling business users to explore insights from the cleaned and curated data.

## ✨ Key Features & Technologies

* **Scalable Data Lake:** Implemented on **Amazon S3** with distinct Raw and Cleaned data zones.
* **Hybrid ETL Strategy:**
    * **AWS Lambda:** For event-driven, near real-time processing of smaller, incoming JSON files.
    * **AWS Glue ETL:** For robust, scalable batch processing of larger CSV datasets using Apache Spark.
* **Metadata Management:** Centralized **AWS Glue Data Catalog** for unified schema discovery and management.
* **Optimized Data Formats:** Conversion to **Apache Parquet** for columnar storage, significantly enhancing query performance and cost efficiency.
* **Data Partitioning:** Strategic partitioning of data by `region` in S3 for accelerated query execution in Athena.
* **Serverless Architecture:** Leveraging Lambda, Glue, and Athena for reduced operational overhead and a pay-per-use cost model.
* **Interactive BI Dashboard:** Data visualization using **Amazon QuickSight** for insightful analytics.
* **Core Languages & Libraries:** Python (`awswrangler`, `pandas`, `pyspark`), SQL.

The general workflow involves:
1.  Setting up AWS accounts and securing IAM roles with appropriate permissions.
2.  Creating S3 buckets for raw and cleaned data.
3.  Downloading the YouTube dataset from Kaggle and uploading it to the raw S3 bucket.
4.  Configuring AWS Glue Crawlers to catalog raw data.
5.  Developing and deploying the AWS Lambda function with necessary layers and S3 event triggers.
6.  Creating and running the AWS Glue ETL job for batch transformations.
7.  Setting up Amazon QuickSight permissions and building the interactive dashboard.

## 🎓 Skills Demonstrated

This project is a testament to practical skills in:

* **Cloud Data Engineering:** Designing, building, and deploying robust data pipelines on AWS.
* **Data Lake Management:** Implementing data zoning and optimization techniques (Parquet, partitioning).
* **Serverless Technologies:** Expertise in AWS Lambda, AWS Glue, and Amazon Athena.
* **ETL Development:** Proficiency in Python with `pandas`, `awswrangler`, and PySpark.
* **Data Modeling & Cataloging:** Managing schemas and metadata with AWS Glue Data Catalog.
* **Data Visualization & BI:** Creating impactful dashboards with Amazon QuickSight.
* **AWS Services Integration:** Seamlessly connecting various AWS services to form a cohesive pipeline.
* **Troubleshooting & Optimization:** Identifying and resolving common data pipeline issues (e.g., performance bottlenecks, permissions).

## 💡 Future Enhancements

* Automate raw data ingestion (e.g., via AWS DataSync or custom API integration).
* Implement advanced data quality checks and anomaly detection within the ETL process.
* Orchestrate the entire pipeline using **AWS Step Functions** or **Glue Workflows**.
* Incorporate **AWS Glue DataBrew** for visual data preparation.
* Develop **CI/CD pipelines** for automated deployment of infrastructure and code.
* Integrate additional data sources for richer analysis.

