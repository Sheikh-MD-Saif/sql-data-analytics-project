# 📊 SQL Data Analytics Project

> End-to-end exploratory and advanced analytics on a sales data warehouse using **T-SQL (SQL Server)**, from database exploration to reusable customer and product reporting views.

![SQL Server](https://img.shields.io/badge/SQL%20Server-T--SQL-CC2927?logo=microsoftsqlserver&logoColor=white)
![Status](https://img.shields.io/badge/status-complete-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)

## 📌 Overview

This project analyses a star-schema sales data warehouse (`gold` layer) containing **60,398 sales lines**, **18,484 customers** and **295 products**. It walks through a structured analytics workflow: **Exploratory Data Analysis (EDA)** to understand the data, then **advanced analytics** to uncover trends, segments and performance drivers, and finally **reporting views** that package the results for BI tools.


## 🧱 Data Model

Star schema in the `gold` schema of the `DataWarehouseAnalytics` database:

| Table | Type | Grain | Rows |
|---|---|---|---|
| `gold.fact_sales` | Fact | One row per order line | 60,398 |
| `gold.dim_customers` | Dimension | One row per customer | 18,484 |
| `gold.dim_products` | Dimension | One row per product | 295 |

`fact_sales.customer_key` → `dim_customers.customer_key` and `fact_sales.product_key` → `dim_products.product_key`.

## 🔍 What's Covered

| # | Script | Topic | Key techniques |
|---|---|---|---|
| 00 | `00_init_database.sql` | Database, schema & data load | `CREATE`, `BULK INSERT` |
| 01 | `01_database_exploration.sql` | Tables and column metadata | `INFORMATION_SCHEMA` |
| 02 | `02_dimensions_exploration.sql` | Explore dimension values | `DISTINCT` |
| 03 | `03_date_range_exploration.sql` | Data time span, customer ages | `MIN/MAX`, `DATEDIFF` |
| 04 | `04_measures_exploration.sql` | Headline business KPIs | `SUM`, `COUNT`, `UNION ALL` |
| 05 | `05_magnitude_analysis.sql` | Totals by dimension | `GROUP BY`, joins |
| 06 | `06_ranking_analysis.sql` | Top / bottom N | `TOP`, `RANK()` |
| 07 | `07_change_over_time_analysis.sql` | Monthly trends | `DATETRUNC`, `FORMAT` |
| 08 | `08_cumulative_analysis.sql` | Running totals, moving averages | `SUM() OVER` |
| 09 | `09_performance_analysis.sql` | YoY and vs-average comparison | `LAG()`, CTEs, `CASE` |
| 10 | `10_data_segmentation.sql` | Cost ranges, VIP / Regular / New customers | `CASE`, CTEs |
| 11 | `11_part_to_whole_analysis.sql` | Category share of total sales | window totals |
| 12 | `12_report_customers.sql` | **View** `gold.report_customers` | CTEs, KPIs |
| 13 | `13_report_products.sql` | **View** `gold.report_products` | CTEs, KPIs |

## 📈 Headline Findings

- **Total sales: 29,356,250** across **27,659 orders** and **60,423 units**.
- **Bikes drive the business**: 96.5% of revenue (Accessories 2.4%, Clothing 1.2%).
- **Top products** are the *Mountain-200* bikes (e.g. Mountain-200 Black-46 at ~1.37M).
- **Top markets**: United States (~9.16M) and Australia (~9.06M) account for over 60% of sales.
- **Sales peaked in 2013** (~16.3M, more than double 2012). Order data spans Dec 2010 to Jan 2014; 2010 and 2014 are partial years.
- 19 sales rows have no order date and are excluded from time-based analyses.

> Figures computed directly from the CSVs in `datasets/flat-files/`.

## 🚀 Getting Started

**Requirements:** SQL Server 2022+ (uses `DATETRUNC`) and SSMS or Azure Data Studio.

1. Clone the repo:
   ```bash
   git clone https://github.com/<your-username>/sql-data-analytics-project.git
   ```
2. Open `scripts/00_init_database.sql` and update the `BULK INSERT` file paths to your local clone location.
3. Run `00_init_database.sql`. **Warning:** it drops and recreates `DataWarehouseAnalytics`.
4. Run scripts `01` to `13` in order.

Alternative: restore `datasets/DataWarehouseAnalytics.bak` in SSMS instead of step 3.

## 📁 Repository Structure

```
├── datasets/
│   ├── flat-files/          # dim_customers.csv, dim_products.csv, fact_sales.csv
│   └── DataWarehouseAnalytics.bak
├── scripts/                 # 00-13 numbered SQL scripts
├── LICENSE
└── README.md
```


## 🙏 Credits

Built following the *SQL Data Analytics* tutorial by **Baraa Khatib Salkini ([Data With Baraa](https://www.youtube.com/@datawithbaraa))**. Dataset is from that course; Analysis extensions are my own.

## 🛡️ License

MIT. See [LICENSE](LICENSE).

## 👤 Author

**Sheikh Mohammad Saif**: [LinkedIn] https://www.linkedin.com/in/sheikhsaif04 · [GitHub] https://github.com/Sheikh-MD-Saif · sheikhsaif09@gmail.com
