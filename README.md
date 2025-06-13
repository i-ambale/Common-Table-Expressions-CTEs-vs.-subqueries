# 📘 README: Comparing Common Table Expressions (CTEs) and Subqueries in SQL

## 🧠 Project Title
**CTEs vs Subqueries: A Practical SQL Comparison with the** `united_nations` **Database**

## 📝 Description
This notebook compares two powerful SQL techniques: **Common Table Expressions (CTEs)** and **subqueries**, using real-world data from the `united_nations` database. The focus is on simplifying complex queries, improving readability, and making performance-conscious choices in query design.

The case study identifies **Sub-Saharan African countries** with underdeveloped economies that are likely to **struggle with access to clean water**.
|  ⚠️ This notebook must be run **locally** (e.g., in Jupyter or VS Code) as it requires a connection to your local **MySQL database**. It will **not run on Google Colab**.

## 🎯 Learning Objectives
By working through this notebook, you will learn to:

  - Understand the conceptual and functional **differences between CTEs and subqueries**
  
  - Decide when to use CTEs for **better query readability and modularity**
  
  - Write complex SQL queries using **both techniques**
  
  - Optimize your SQL code by replacing **nested subqueries** with **CTEs**

## 🧩 Tools and Requirements
###⚙️ Environment
- MySQL Workbench + MySQL Server (running locally)

- Jupyter Notebook or VS Code

- Python libraries:

  - `pymysql`
  
  - `sqlalchemy`
  
  - `pandas`
  
  - `jupyter`

### 💾 Database Schema
Database: `united_nations`

Tables used:

  - `Access_to_Basic_Services`
  
  - `Economic_Indicators`
  
  - `Geographic_Locations`

## 📊 Sample Use Case
We analyze countries in **Sub-Saharan Africa** that:

  - Had **low access** to managed drinking water in 2020
  
  - Had a **GDP below their regional average**

The same query is built in two ways:

  1. Using **subqueries** in `WHERE` or `FROM` clauses
  
  2. Refactored using **TEs** for clarity and efficiency

## 🧱 Code Structure
```
.
├── ctes_vs_subqueries.ipynb     # Main SQL tutorial notebook
├── README.md                    # Project guide and instructions
├── sql/                         # Optional: raw .sql scripts
├── data/                        # Optional: CSVs for initial data seeding
└── images/                      # Optional: diagrams or query visualizations
```

## 🚀 How to Use
1. Clone this repository to your local machine.

2. Set up your local MySQL server and load the `united_nations` database with the required tables.

3. Update the connection string in the notebook:
    ```
    mysql+pymysql://root:<your_password>@localhost:3306/united_nations
    ```
4. Run the notebook cells step-by-step to compare and explore queries.

## 🔍 Example SQL Snippet (Using a CTE)
```
WITH Regional_GDP AS (
    SELECT
        Country_name,
        Region,
        Est_gdp_in_billions,
        AVG(Est_gdp_in_billions) OVER (PARTITION BY Region) AS Avg_GDP
    FROM Economic_Indicators
    WHERE Time_period = 2020
)

SELECT
    a.Country_name,
    a.Pct_managed_drinking_water_services,
    r.Est_gdp_in_billions,
    r.Avg_GDP
FROM Access_to_Basic_Services a
JOIN Regional_GDP r ON a.Country_name = r.Country_name
WHERE a.Region = 'Sub-Saharan Africa'
  AND a.Pct_managed_drinking_water_services < 60
  AND r.Est_gdp_in_billions < r.Avg_GDP;
```
## 🧠 Conclusion
This notebook helps you develop the **critical thinking needed to choose the best SQL pattern** for a given situation. Whether it's **performance optimization**, **readability**, or **modularization**, mastering both CTEs and subqueries is a key part of becoming a proficient SQL user.

## 📧 Contact
Author: Ibrahim Ambale

📍 Nairobi, Kenya

🔗 LinkedIn: [Ibrahim Ambale]([linkedin.com/in/ibrahim-ambale](https://www.linkedin.com/in/ibrahim-ambale/))
