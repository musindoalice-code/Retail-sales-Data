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

<h1 align="center">Retail Sales Data Analysis 


<p align="center">
  <img src="https://img.shields.io/badge/SQL-Analysis-blue" alt="SQL">
  <img src="https://img.shields.io/badge/Rows-1%2C000-informational" alt="Rows">
  <img src="https://img.shields.io/badge/Status-Complete-success" alt="Status">
</p>

---
# Retail Data Agent Task

**BrightLearn — Retail Data Agent Task**

## Project Objective

The goal of this project was to build a natural-language data agent over a retail sales dataset — allowing business questions to be asked in plain English and answered directly from the underlying data, without writing manual queries each time.

## Tools Used

- **Databricks** — data platform and workspace
- **Databricks Genie Space** — AI/BI natural language data agent
- SQL (for underlying data exploration and validation)

## Dataset Overview

The agent was built on a retail sales transaction dataset containing **1,000 records**, with the following fields:

| Column | Description |
|---|---|
| Transaction ID | Unique identifier for each transaction |
| Date | Date of the transaction |
| Customer ID | Unique identifier for each customer |
| Gender | Customer's gender |
| Age | Customer's age |
| Product Category | Category of the purchased product (e.g. Beauty, Clothing, Electronics) |
| Quantity | Number of units purchased |
| Price per Unit | Price of a single unit |
| Total Amount | Total transaction value (Quantity × Price per Unit) |

## Steps Followed

1. Loaded and reviewed the retail sales dataset in Databricks
2. Explored the data using SQL to understand structure, ranges, and data quality
3. Created a Genie Space and connected it to the dataset
4. Configured the agent's instructions so it could correctly interpret business questions against the schema
5. Tested the agent with a series of sample business questions
6. Reviewed the agent's generated insights and validated them against the underlying data
7. Documented findings and packaged the project for submission

## Agent Instructions

> _Add the actual instructions/context you configured in your Genie Space here — e.g. which tables it should reference, any business definitions you gave it (such as how "premium product" or "one-time buyer" is defined), and any specific formatting or behavior you asked it to follow._

## Sample Questions Tested

- **"What are the top 10 performing products in [period]?"**

  The agent identified that premium products and high-value customers drive a disproportionate share of revenue, weekend traffic shows a clear multiplier effect on basket size, and category performance is relatively balanced, providing natural diversification.

- _Add any additional questions you tested here._

## Key Insights

**Strengths identified:**
- Premium products and high-value customers drive disproportionate revenue
- Weekend traffic and larger basket sizes show clear revenue multipliers
- Balanced category performance provides diversification

**Critical risks identified:**
- Zero customer retention — 100% of buyers in the analyzed window were one-time buyers
- Heavy concentration risk — roughly 20% of customers account for 63% of revenue
- Extreme revenue volatility — a 125% monthly swing observed
- 60% of transactions are low-value (≤R50 items)

**Recommended immediate actions:**
1. Launch a retention program targeting the top 20% of premium customers
2. Implement basket size incentives (e.g. 3–4 unit bundles)
3. Expand premium product lines, which currently represent 54% of revenue
4. Stabilize Q3 performance with targeted September promotions
5. Optimize Saturday operations, the highest-revenue day

## Conclusion

The Genie Space agent successfully translated natural-language business questions into accurate, data-grounded answers, surfacing both growth opportunities (premium products, weekend traffic) and risks (customer retention, revenue concentration) that would otherwise require manual SQL analysis to uncover. This demonstrates the value of a conversational data agent for making retail performance insights accessible to non-technical stakeholders.

---

*Submitted as part of the BrightLearn Retail Data Agent Task.*

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
