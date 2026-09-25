# NYC Taxi Fare Prediction — A Big Data Pipeline with PySpark & Spark MLlib
Big data pipeline predicting NYC taxi fares from 5 years (2020–2024) of trip data using PySpark and Spark MLlib Built with **Spark**, this project covers the full data lifecycle: ingestion, distributed cleaning, storage, exploratory analysis, feature engineering, and predictive modeling.

## Overview

The goal of this project is to analyze large-scale NYC taxi trip data and build a regression model that predicts the fare amount of a trip based on features such as pickup/drop-off location, trip distance, duration, and time of day.

The pipeline was designed to work at scale using PySpark, since the combined dataset spans **120 monthly files** across 5 years for two taxi types (Yellow and Green).

## Pipeline

| Stage | What was done |
|---|---|
| **1. Data Ingestion** | Downloaded official NYC TLC Yellow & Green taxi trip records (Parquet, Jan 2020 – Dec 2024) and converted them to CSV using PySpark. |
| **2. Data Cleaning** | Standardized timestamp formats, removed nulls/invalid records (zero distance, non-positive fares, dropoff-before-pickup, unrealistic passenger counts) using the PySpark DataFrame API. |
| **3. Storage** | Persisted cleaned datasets into SQLite (`nyc_yellow_taxi.db`, `nyc_green_taxi.db`) as a durable checkpoint before analysis. |
| **4. Exploratory Data Analysis** | Used PySpark SQL and the DataFrame API to explore pickup hotspots, hourly/weekly/seasonal demand trends, fare-vs-distance relationships, and payment method distribution. |
| **5. Feature Engineering** | Extracted time-based features (hour, day of week, month), computed trip duration, created distance bins, and one-hot encoded categorical variables. |
| **6. Modeling** | Trained and evaluated three Spark MLlib regressors — Linear Regression, Decision Tree, and Random Forest — using RMSE, MAE, and R². |
| **7. Visualization** | Plotted Actual vs. Predicted fare amounts to visually assess model performance. |

## Results

| Taxi Type | Best Model | RMSE | R² |
|---|---|---|---|
| Yellow | Random Forest | 9.79 | 0.704 |
| Green | Random Forest | 7.80 | 0.695 |

Random Forest consistently outperformed Linear Regression and Decision Tree on both datasets, capturing non-linear relationships between trip features and fare amount more effectively.

## Tools 

- **Python 3**
- **Spark** (PySpark — Spark SQL & Spark MLlib)
- **SQLite**
- **Pandas**
- **Matplotlib / Seaborn**
- **Jupyter Notebook**

## Dataset

[NYC TLC Trip Record Data](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) — official Yellow and Green Taxi trip records published by the NYC Taxi & Limousine Commission.

> Raw data files are **not included** in this repository due to their size (120 monthly files, several GB total). 

## How to Run

**Clone the repository**
```bash
git clone https://github.com/ecmelsk/nyc-taxi-fare-prediction-pyspark.git
cd nyc-taxi-fare-prediction-pyspark
```
