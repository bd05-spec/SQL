# Bank Customer & Card Portfolio Analysis

> **Question:** How is the observed cardholder portfolio distributed across customer segments, balances, credit limits, and utilization levels?

This Microsoft SQL Server project contains a **1,627-row, 13-column** customer dataset and a set of queries for portfolio profiling. It calculates baseline customer and credit measures, compares customer segments, and highlights high-utilization and long-tenure accounts for further review.

> **Scope clarification:** The CSV contains a `churn` field, but the current SQL script does not calculate churn counts or churn rates by segment. Despite the project folder's "Bank churn" name, its present queries focus on descriptive customer/card analytics-not on explaining or predicting churn.

## Analysis map

```mermaid
flowchart LR
    A[bank_churn_data.csv<br/>1,627 records] --> B[Load as<br/>bank_churn_data]
    B --> C[Portfolio KPIs<br/>customers  |  age  |  limits  |  utilization]
    C --> D[Segment comparisons<br/>card  |  income  |  marital  |  age]
    D --> E[Account review<br/>high utilization  |  low balance-to-limit]
    E --> F[Tenure and dependent<br/>summaries]
```

## What the SQL examines

- Total customer count, average utilization ratio, average credit limit, and average age.
- Customer counts by card category and marital status.
- Average balance and dependent count by income band.
- Customer distribution by age groups (18-25, 26-35, 36-45, 46-55, and 56+).
- Top accounts by utilization, longest relationship length, and a low-balance-to-credit-limit comparison.
- A rule-based utilization label: **High Risk** above 0.80, **Moderate Risk** from 0.50 through 0.80, and **Low Risk** below 0.50. This thresholding is a screening convention in the script, not a validated risk model.

## Files in this project

| File | What it is for |
| --- | --- |
| [`Bank Churn Analysis.sql`](<./Bank Churn Analysis.sql>) | SQL Server queries for summary KPIs, segment comparisons, age bands, utilization screening, and long-tenure account lists. It selects the `Bank Churn DB` database and expects a table named `bank_churn_data` to already exist. |
| [`bank_churn_data.csv`](<./bank_churn_data.csv>) | The 1,627-row source table extract with customer/card category, churn flag, income, marital/education fields, balance, credit limit, age, dependents, months on book, and utilization ratio. |

## Run in SQL Server

1. Create or select a development database named `Bank Churn DB`, or change the `USE` statement.
2. Import the CSV into a table named `bank_churn_data`, mapping the CSV headers to compatible SQL columns and data types.
3. Run the script in SQL Server Management Studio or another SQL Server client.
4. Review the returned result sets; several queries return customer-level identifiers.

The script does not include a `CREATE TABLE` or CSV import step. Use a non-production database and protect customer-level data appropriately.

## Limitations

- There is no explicit churn analysis in the current script, even though `churn` is present in the data. A next step would be to compare churn counts/rates across tenure, utilization, card category, or customer segments using a documented denominator.
- Utilization thresholds are rules of thumb in this analysis; they are not fitted or validated against outcomes.
- The SQL does not document source provenance, snapshot date, or a formal data dictionary.
- Customer-level top-10 output should be treated as sensitive and should not be redistributed without appropriate permission.
