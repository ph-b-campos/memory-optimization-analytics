# 💾 HR Analytics Memory Optimization

**Executive Summary:**
In this Data Engineering , I optimized the memory footprint of a large customer dataset for an online data science training provider. By strictly defining data types—downcasting numerics, mapping booleans, and structuring ordinal/nominal categories—I successfully reduced the dataframe's memory usage by **over 96.5%** (from 2.0+ MB to ~69.5 KB). This is a crucial step to ensure scalable, faster data loading, and efficient model training pipelines in cloud environments.

---

## 1. The Business Problem

A common bottleneck when deploying Machine Learning models to generate business value is the sheer volume of data. Inefficiently stored datasets can significantly slow down I/O operations, inflate cloud computing costs, and cause Out-Of-Memory (OOM) crashes during model training.

*Training Data Ltd.* needs to clean up and filter one of their largest customer datasets to feed a predictive model. To create a proof-of-concept for a more efficient storage solution, I was tasked with profiling, cleaning, and optimizing the `customer_train.csv` subset.

## 2. Optimization Strategy & Feature Engineering

To achieve maximum memory efficiency without losing any information, I applied a rigorous data typing strategy:

* **Binary Features to Booleans:** Mapped text-based binary columns (e.g., `job_change` and `relevant_experience`) into 1-bit `bool` arrays, reducing their specific memory footprint by ~87%.
* **Downcasting Numerical Variables:** Analyzed the min/max limits of numerical data. Downcasted 64-bit integers and floats to `int32` and `float16` where appropriate, cutting numerical memory allocation by 58%.
* **Structuring Categorical Data:** Converted repetitive string `object` types to `category` types. Crucially, I applied **ordinal structures** to variables like `experience`, `education_level`, and `company_size`. This not only saves RAM but ensures future ML algorithms inherently understand the hierarchical relationship of these features (e.g., Masters > Graduate).
* **Business Rule Filtering:** Applied final filtering masks to target highly experienced candidates (10+ years of experience in companies with 1,000+ employees) as requested by the HR team.

## 3. Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)

> 💡 **The step-by-step memory profiling, before/after comparisons, and the exact code implementations are documented directly inside the Jupyter Notebook.**
