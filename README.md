# SQL Analytics Projects

This repository contains three Microsoft SQL Server projects. They demonstrate querying and validating source data, building useful aggregates, and shaping operational datasets into analysis-ready tables.

## Projects

### Bank Churn

Use customer and card-account attributes to examine portfolio composition and potential utilization risk. The queries calculate customer, age, credit-limit, and utilization measures; compare customers by card category, income, and marital status; segment by age; and inspect high-utilization and long-tenure customers.

- [Analysis queries](<Bank churn/Bank Churn Analysis.sql>)
- [Bank churn dataset](<Bank churn/bank_churn_data.csv>)

The script expects a SQL Server database named `Bank Churn DB` and a table named `bank_churn_data` to exist. Load the CSV and create the table with compatible column names before running the queries.

### Merchant Interchange Finance Report

Prepare transaction-level interchange data for finance analysis. The script checks for nulls, duplicates, invalid dates, negative amounts, missing merchant names, and unusual transaction counts, then creates date, merchant, card, acquirer, and category dimensions from the source dataset.

- [SQL script](<Merchant Interchange Finance Report/SQLQuery Final.sql>)
- [Sample interchange dataset](<Merchant Interchange Finance Report/Sample Interchange Dataset.csv>)

The CSV columns include reporting date, merchant, card/network/product attributes, settlement amount, interchange revenue, and transaction count.

### Swiggy Orders

Clean and organize food-delivery order data for multidimensional analysis. The SQL checks nulls, blanks, types, and duplicate rows, then creates date, location, restaurant, category, and dish dimensions plus a `fact_swiggy_orders` fact table.

- [SQL script](<Swiggy Project/Swiggy_SQL.sql>)
- [Swiggy dataset](<Swiggy Project/Swiggy_Data.csv>)

The script expects the CSV to be loaded into a SQL Server table named `swiggy_data` before it is run.

## Running the projects

Use Microsoft SQL Server and SQL Server Management Studio (or another compatible SQL client). Load each CSV into the source table expected by its script, review the database/table names at the top of the file, and execute the validation and modeling steps in order. The scripts are learning and portfolio artifacts; inspect their definitions and test in a non-production database before adapting them to real systems.
