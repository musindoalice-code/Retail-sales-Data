# Retail-sales-Data
<img width="1200" height="260" alt="image" src="https://github.com/user-attachments/assets/f9581dbd-6611-4176-81a8-aea583fcc090" />

  <!-- bar chart icon -->
  <g transform="translate(940,60)">
    <rect x="0" y="110" width="34" height="60" rx="4" fill="url(#barGrad)"/>
    <rect x="46" y="70" width="34" height="100" rx="4" fill="url(#barGrad)" opacity="0.9"/>
    <rect x="92" y="30" width="34" height="140" rx="4" fill="url(#barGrad)" opacity="0.75"/>
    <rect x="138" y="90" width="34" height="80" rx="4" fill="url(#barGrad)" opacity="0.6"/>
  </g>

  <!-- database / SQL icon -->
  <g transform="translate(70,85)" fill="none" stroke="#7dd3fc" stroke-width="4">
    <ellipse cx="45" cy="15" rx="45" ry="15"/>
    <path d="M0,15 L0,75 A45,15 0 0,0 90,75 L90,15"/>
    <path d="M0,45 A45,15 0 0,0 90,45"/>
  </g>

  <text x="200" y="110" font-family="Verdana, Arial, sans-serif" font-size="46" font-weight="bold" fill="#f8fafc">
    Retail Sales Data Analysis
  </text>
  <text x="200" y="150" font-family="Verdana, Arial, sans-serif" font-size="20" fill="#94a3b8">
    SQL-Based Exploratory Data Analysis &amp; Data Quality Audit
  </text>

  <text x="200" y="195" font-family="Verdana, Arial, sans-serif" font-size="15" fill="#38bdf8">
    1,000 Transactions  •  Data Cleaning  •  Summary Statistics  •  Duplicate &amp; Anomaly Checks
  </text>
</svg>
<p align="center">
  <img src="assets/banner.svg" alt="Retail Sales Data Analysis Banner" width="100%">
</p>

<h1 align="center">Retail Sales Data Analysis (SQL)</h1>

<p align="center">
  Exploratory data analysis and data quality auditing of a retail sales dataset, performed entirely in SQL.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/SQL-Analysis-blue" alt="SQL">
  <img src="https://img.shields.io/badge/Rows-1%2C000-informational" alt="Rows">
  <img src="https://img.shields.io/badge/Status-Complete-success" alt="Status">
</p>

---

## 📋 Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Tools Used](#tools-used)
- [SQL Analysis](#sql-analysis)
  - [1. Data Preview](#1-data-preview)
  - [2. Summary Statistics](#2-summary-statistics)
  - [3. Duplicate Customer Check](#3-duplicate-customer-check)
  - [4. Full Row Duplicate Check](#4-full-row-duplicate-check)
  - [5. Age Range Validation](#5-age-range-validation)
  - [6. Negative Quantity Check](#6-negative-quantity-check)
  - [7. Negative Sales Check](#7-negative-sales-check)
  - [8. Missing Value Audit](#8-missing-value-audit)
  - [9. Combined Data Quality Report](#9-combined-data-quality-report)
- [Key Insights](#key-insights)
- [Project Structure](#project-structure)
- [License](#license)

## Overview

This project analyzes a retail sales dataset of **1,000 transactions** using pure SQL — no Python or external BI tools. The queries were run against a table (`workspace.default.retail_sales_data`) and cover everything from a first data preview through summary statistics and a full data quality audit (duplicates, missing values, and invalid/outlier records).

## Dataset

The dataset (`retail_sales_data`) contains the following columns:

| Column | Description | Type |
|---|---|---|
| `Transaction ID` | Unique identifier for each transaction | String/Int |
| `Date` | Date of the transaction | Date (YYYY-MM-DD) |
| `Customer ID` | Unique identifier for each customer | String |
| `Gender` | Customer's gender | Categorical |
| `Age` | Customer's age | Integer |
| `Product Category` | Category of the purchased product (e.g., Beauty, Clothing, Electronics) | Categorical |
| `Quantity` | Number of units purchased | Integer |
| `Price per Unit` | Price of a single unit | Numeric |
| `Total Amount` | Total transaction value (`Quantity` × `Price per Unit`) | Numeric |

**Rows:** 1,000
**Table:** `` `workspace`.`default`.`retail_sales_data` ``

## Tools Used

- **SQL** (Databricks SQL / Spark SQL syntax)
- Databricks Workspace for querying and data exploration

## SQL Analysis

All queries below are in [`queries/analysis.sql`](queries/analysis.sql).

### 1. Data Preview

A full look at the raw table before any analysis.

```sql
SELECT * 
FROM `workspace`.`default`.`retail_sales_data`;
```

### 2. Summary Statistics

Generates core descriptive statistics across customers, product quantity, pricing, and total sales — including averages, minimums, maximums, and the overall revenue total.

```sql
SELECT
    COUNT(*) AS total_records,
    AVG(`Age`) AS average_age,
    MIN(`Age`) AS minimum_age,
    MAX(`Age`) AS maximum_age,
    AVG(`Quantity`) AS average_quantity,
    MIN(`Quantity`) AS minimum_quantity,
    MAX(`Quantity`) AS maximum_quantity,
    AVG(`Price per Unit`) AS average_price_per_unit,
    MIN(`Price per Unit`) AS minimum_price_per_unit,
    MAX(`Price per Unit`) AS maximum_price_per_unit,
    AVG(`Total Amount`) AS average_total_amount,
    MIN(`Total Amount`) AS minimum_total_amount,
    MAX(`Total Amount`) AS maximum_total_amount,
    SUM(`Total Amount`) AS total_sales
FROM `workspace`.`default`.`retail_sales_data`;
```

### 3. Duplicate Customer Check

Flags any `Customer ID` that appears more than once, to understand repeat customers vs. potential ID duplication issues.

```sql
SELECT
    `Customer ID`,
    COUNT(*) AS record_count
FROM `workspace`.`default`.`retail_sales_data`
GROUP BY `Customer ID`
HAVING COUNT(*) > 1
ORDER BY record_count DESC;
```

### 4. Full Row Duplicate Check

Identifies fully duplicated transaction records across all key fields.

```sql
SELECT
    `Transaction ID`,
    `Date`,
    `Customer ID`,
    `Gender`,
    `Age`,
    `Product Category`,
    `Quantity`,
    `Price per Unit`,
    `Total Amount`,
    COUNT(*) AS duplicate_count
FROM `workspace`.`default`.`retail_sales_data`
GROUP BY `Transaction ID`, `Date`, `Customer ID`, `Gender`, `Age`, `Product Category`, `Quantity`, `Price per Unit`, `Total Amount`
HAVING COUNT(*) > 1
ORDER BY duplicate_count DESC;
```

### 5. Age Range Validation

Checks for implausible ages (negative or over 100) that may indicate data entry errors.

```sql
SELECT *
FROM `workspace`.`default`.`retail_sales_data`
WHERE `Age` < 0
   OR `Age` > 100
ORDER BY `Age`;
```

### 6. Negative Quantity Check

Flags any transactions with a negative quantity, which shouldn't be possible in a standard sales record.

```sql
SELECT *
FROM `workspace`.`default`.`retail_sales_data`
WHERE `Quantity` < 0
ORDER BY `Quantity`;
```

### 7. Negative Sales Check

Flags any transactions with a negative total amount.

```sql
SELECT *
FROM `workspace`.`default`.`retail_sales_data`
WHERE `Total Amount` < 0
ORDER BY `Total Amount`;
```

### 8. Missing Value Audit

Counts missing (NULL) values across the key columns.

```sql
SELECT
    COUNT(*) AS total_records,
    COUNT(*) - COUNT(`Customer ID`) AS missing_customer_id,
    COUNT(*) - COUNT(`Age`) AS missing_age,
    COUNT(*) - COUNT(`Product Category`) AS missing_product_category,
    COUNT(*) - COUNT(`Quantity`) AS missing_quantity,
    COUNT(*) - COUNT(`Price per Unit`) AS missing_price_per_unit,
    COUNT(*) - COUNT(`Total Amount`) AS missing_total_amount
FROM `workspace`.`default`.`retail_sales_data`;
```

### 9. Combined Data Quality Report

A single consolidated query combining missing value counts with anomaly checks (invalid ages, negative quantities, negative prices, negative sales) for a full data quality snapshot in one result set.

```sql
SELECT
    COUNT(*) AS total_records,
    COUNT(*) - COUNT(`Customer ID`) AS missing_customer_id,
    COUNT(*) - COUNT(`Age`) AS missing_age,
    COUNT(*) - COUNT(`Product Category`) AS missing_product_category,
    COUNT(*) - COUNT(`Quantity`) AS missing_quantity,
    COUNT(*) - COUNT(`Price per Unit`) AS missing_price_per_unit,
    COUNT(*) - COUNT(`Total Amount`) AS missing_total_amount,
    SUM(CASE WHEN `Age` < 0 OR `Age` > 100 THEN 1 ELSE 0 END) AS unusual_age_records,
    SUM(CASE WHEN `Quantity` < 0 THEN 1 ELSE 0 END) AS negative_quantity_records,
    SUM(CASE WHEN `Price per Unit` < 0 THEN 1 ELSE 0 END) AS negative_price_records,
    SUM(CASE WHEN `Total Amount` < 0 THEN 1 ELSE 0 END) AS negative_sales_records
FROM `workspace`.`default`.`retail_sales_data`;
```

## Key Insights

> Replace these placeholders with your actual query results once you've run the analysis.

- **Total records:** 1,000
- **Average customer age:** _fill in from Query 2_
- **Average transaction value:** _fill in from Query 2_
- **Total revenue:** _fill in from Query 2_
- **Duplicate customers found:** _fill in from Query 3_
- **Duplicate transactions found:** _fill in from Query 4_
- **Data quality issues (missing/invalid values):** _fill in from Query 9_

## Project Structure

```
retail-sales-analysis/
├── assets/
│   └── banner.svg
├── queries/
│   └── analysis.sql
├── data/
│   └── retail_sales_data.csv
└── README.md
```

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
