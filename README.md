# SaaS Product Analytics Pipeline
End-to-end ETL and analytics pipeline for SaaS products, processing user events and subscriptions to generate key metrics like churn, revenue, and feature adoption. <br>
Note: This notebook is designed to run on **Databricks**, which includes PySpark, Delta Lake, Spark SQL, and standard Python libraries (pandas, numpy, matplotlib). No additional package installation is required.

## Table of Contents 
1. Project Overview
2. Dataset
3. ETL Pipeline Architecture
4. Metrics Calculated
5. Example Insights
6. Revenue and Churn Analysis
7. Tech Stack
8. Project Structure
9. Future Improvements

## Project Overview 
This project builds a complete SaaS product analytics pipeline using Databricks and PySpark. It processes user events, subscription information, and feature usage to generate actionable SaaS metrics.
The goal is to provide insights into customer behavior, revenue trends, churn patterns, and feature adoption, which can guide business and product decisions.

Note: Certain code snippets and documentation were assisted with AI tools to streamline development, while all data analysis logic, metric calculations, and business insights were designed and validated manually.

## Dataset/Data Source
The pipeline uses two main tables:
Events: 
| Column Name | Description |
|-------------|------------|
| user_id     | Unique identifier for the user |
| event_date | Timestamp of the product interaction |
| event_type        | Feature used (feature_A, feature_B, feature_C) |

Subscriptions: 
| Column Name          | Description                                               |
|---------------------|-----------------------------------------------------------|
| user_id             | Unique identifier for each user                            |
| signup_date         | Date the user registered                                    |
| country             | User location                                              |
| plan                | Subscription tier: Free, Basic, or Pro                     |
| subscription_status | Status of the subscription: Paid or Free                   |
| revenue             | Monthly subscription revenue                                |
| churn_date          | Date the subscription ended (if churned)                  |

**Data Source**
This dataset is released under the [MIT License](https://www.kaggle.com/datasets/philbertchan/saas-product-dashboard-mau-feature-usage-mrr?select=subscriptions.csv) and used here for educational and portfolio purposes. It has been adapted for this project to demonstrate churn analysis, revenue metrics, and feature adoption insights.

## ETL Pipeline Architecture
The pipeline follows a Bronze → Silver → Gold design pattern:

**1. Bronze Layer (Raw Data)**
- Raw ingestion from CSV or database tables
- Minimal transformations

**2. Silver Layer (Cleaned Data)**
- Data cleaning and normalization
- Deduplication and type conversions
- Joining related tables for enriched dataset

**3. Gold Layer (Analytics / Metrics)**
- Calculated tables for churn rate, revenue, revenue churn, feature adoption, and engagement metrics
- Aggregation by plan, country, and cohort
  
**Pipeline Diagram:** <br>
Raw Data <br>
   ↓ <br>
Bronze Layer (Raw Tables) <br>
   ↓ <br>
Silver Layer (Cleaned / Transformed Data) <br>
   ↓ <br>
Gold Layer (Analytics Metrics)

## Metrics Calculated
1. Monthly Active Users (MAU)
2. Feature Adoption Analysis
3. Feature Usage vs Retention
4. Churn Rate Analysis
5. Revenue Analysis (MRR)

## Example Insights: 
Feature Adoption Analysis and Feature Usage vs Retention: 
* Users engaging with Feature B exhibit the lowest churn rate (25.81%), suggesting it plays a key role in product retention. In contrast, Feature A users show the highest churn (28.09%), indicating potential opportunities to improve feature value or onboarding.
Churn Rate Analysis
* UK Pro has the highest churn rate (50%) but contributes only 3.85% to total churn, as the segment is small. USA Basic and India Free show high churn rate and high churn contribution, making them critical for retention efforts.
* Both Pro ($750) and Basic ($740) contribute similarly to total revenue, meaning both tiers require retention focus. Free plan is excluded from revenue analysis as it generates no revenue.
* Canada ($560) generates the most revenue, followed by USA ($380), India ($290), and UK ($260). While Canada is strong, India and UK have growth potential, indicating opportunities to increase revenue.
* First 3 months were stable ($440 → $520 → $400).Month 4 dropped to $130, suggesting potential seasonality, churn spikes, or marketing gaps that need investigation.

## Tech Stack 
* **Databricks –** Cloud platform for notebooks, cluster management, and scalable Spark execution
* **PySpark –** ETL, data transformations, and analytics computations
* **Spark SQL –** SQL-based querying of structured data within Spark
* **Schema Catalog –** Managing table schemas and metadata for reliable analytics
* **Delta Tables / Volume –** Storage and organization of raw (Bronze), cleaned (Silver), and metrics (Gold) data
* **Notebooks –** Single notebook structure implementing end-to-end ETL pipeline and analytics
