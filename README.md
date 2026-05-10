# 🔥 PySpark & Pandas — COVID-19 Data Analysis

> A hands-on, end-to-end notebook that bridges **Pandas** (in-memory analysis) and **PySpark** (distributed processing) using a real-world COVID-19 dataset.

---

## 📌 Overview

This notebook walks through a complete data workflow — from raw CSV ingestion in Pandas all the way to distributed SQL queries in PySpark — using cumulative COVID-19 statistics (cases, deaths, vaccinations) aggregated by continent.

It is designed for data engineers, analysts, and Python developers who want a practical introduction to the PySpark DataFrame API and Spark SQL without leaving a Jupyter environment.

---

## 📂 Repository Structure

```
pyspark-pandas-covid19-analysis/
│
├── pyspark_pandas_covid19_analysis.ipynb   # Main notebook
└── README.md
```

---

## 🧠 What You Will Learn

| Topic | Details |
|---|---|
| **PySpark vs Pandas** | When to use each tool and their trade-offs |
| **Environment setup** | Installing PySpark, findspark, and Pandas |
| **SparkSession** | Creating and configuring a session with Arrow optimisation |
| **Data ingestion** | Loading a remote CSV with Pandas |
| **Schema definition** | Explicit `StructType` schemas for type-safe Spark DataFrames |
| **DataFrame conversion** | Pandas → Spark with type alignment and null handling |
| **Exploration** | `select`, `filter`, `show`, `printSchema` |
| **Column derivation** | Computing derived metrics with `withColumn` |
| **Aggregation** | `groupBy` + `agg` for continental summaries |
| **UDFs** | Writing and registering Python User-Defined Functions |
| **Spark SQL** | Running SQL queries against temporary views |

---

## 🗂️ Notebook Sections

1. PySpark Overview  
2. Understanding Pandas  
3. Setting Up the Environment  
4. Initializing a Spark Session  
5. Loading Data into Pandas  
6. Exploring the Dataset  
7. Converting a Pandas DataFrame to Spark  
8. Inspecting the Spark DataFrame Schema  
9. Basic Data Exploration  
10. Working with Columns  
11. Grouping and Summarizing  
12. User-Defined Functions (UDFs)  
13. Querying with Spark SQL  
14. Running SQL Queries  

---

## 📊 Dataset

- **Source:** [Our World in Data — COVID-19](https://ourworldindata.org/covid-vaccinations)  
- **Format:** CSV (loaded directly from a remote URL)  
- **Key columns:**

| Column | Description |
|---|---|
| `continent` | Geographic region |
| `total_cases` | Cumulative confirmed COVID-19 cases |
| `total_deaths` | Cumulative confirmed deaths |
| `total_vaccinations` | Total vaccine doses administered |
| `population` | Total population |

---

## ⚙️ Requirements

| Package | Purpose |
|---|---|
| `pyspark` | Distributed data processing |
| `findspark` | Locates the local Spark installation |
| `pandas` | In-memory data manipulation |

Install all dependencies with:

```bash
pip install pyspark findspark pandas
```

> **Java required:** PySpark runs on the JVM. Make sure **Java 8 or 11** is installed and `JAVA_HOME` is set correctly before running the notebook.

---

## 🚀 Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/pyspark-pandas-covid19-analysis.git
cd pyspark-pandas-covid19-analysis

# 2. Install dependencies
pip install pyspark findspark pandas

# 3. Launch Jupyter
jupyter notebook pyspark_pandas_covid19_analysis.ipynb
```

---

## 🔑 Key Concepts at a Glance

```python
# Start a Spark session
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("COVID-19").getOrCreate()

# Load with Pandas, convert to Spark
import pandas as pd
pdf = pd.read_csv("data.csv")
sdf = spark.createDataFrame(pdf)

# Aggregate with PySpark
from pyspark.sql import functions as F
sdf.groupBy("continent").agg(F.sum("total_deaths")).show()

# Query with SQL
sdf.createTempView("data_v")
spark.sql("SELECT continent FROM data_v WHERE total_vaccinations > 1000000").show()
```

---

## 📈 Sample Output

```
+-------------+----------------+
|    continent|total_deaths_sum|
+-------------+----------------+
|         Asia|       1,248,000|
|       Europe|       1,012,500|
|North America|         983,200|
|South America|         752,400|
|       Africa|         258,100|
|      Oceania|          12,600|
+-------------+----------------+
```



---

## 📄 License

This project is released for educational purposes. The COVID-19 dataset is sourced from [Our World in Data](https://ourworldindata.org/) and is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
