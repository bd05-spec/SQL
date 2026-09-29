# Merchant Interchange Finance Analysis

> **Question:** How are settlement volume and interchange revenue distributed across merchants, cards, acquirer networks, products, and reporting periods?

The project contains a sample of **600 transaction-summary records** and a Microsoft SQL Server script that takes the data from quality checks into a star-schema-style model. The final queries compare merchant settlement volume, calculate interchange revenue as a share of settlement, rank merchants, and inspect month-over-month changes.

## From sample data to business questions

```mermaid
flowchart LR
    A[600-row interchange sample] --> B[Quality checks<br/>nulls  |  dates  |  duplicates  |  amounts]
    B --> C[Trim source text]
    C --> D[Build dimensions<br/>date  |  merchant  |  card  |  acquirer  |  category]
    D --> E[Load Fact_Interchange<br/>volume  |  revenue  |  transaction count]
    E --> F[Rank, rate, share<br/>and compare reporting months]
```

### Questions answered by the SQL

- Which ten merchants have the highest settlement/interchange volume?
- What is each merchant's interchange revenue relative to settlement amount?
- How much of total volume is represented by the largest merchant?
- How do merchants rank by volume?
- How do current- and previous-month merchant ranks, revenue, and share compare?

The script also checks for nulls, repeated interchange IDs, duplicate rows, invalid reporting dates, negative monetary values, missing merchant names, and non-positive transaction counts.

## Files in this project

| File | What it is for |
| --- | --- |
| [`SQLQuery Final.sql`](<./SQLQuery Final.sql>) | Main SQL Server script: data checks, source-text trimming, creation/loading of five dimensions and `Fact_Interchange`, then merchant volume/rate/share/rank analyses. |
| [`Sample Interchange Dataset.csv`](<./Sample Interchange Dataset.csv>) | 600 sample rows with `InterChangeID`, `ReportingDate`, card and acquirer attributes, merchant, usage/product type, settlement amount, interchange revenue, and transaction count. |
| [`SQL Queries Final Doc.docx`](<./SQL Queries Final Doc.docx>) | Companion written query/documentation file. |
| [`SQL queries.pdf`](<./SQL queries.pdf>) | PDF companion to the interchange SQL materials. |

## Run safely

Use Microsoft SQL Server. First create a development database and load the CSV into a table named **`Sample Interchange Dataset`** with compatible data types. Review the script before running it: its text-trimming section updates the loaded source table, its `CREATE TABLE` statements are not guarded for repeat execution, and the standalone line `Card Number Table` is not valid T-SQL as written. Remove/comment that heading or correct it before running the schema section. Run against a disposable copy until table definitions, date conversion, keys, and duplicate assumptions have been checked.

## Assumptions to review

- The model makes `InterChangeID` the fact-table primary key; verify that it is unique in the loaded sample before building the fact table.
- Merchant interchange rate is calculated as summed interchange revenue divided by summed settlement amount. It is a ratio of aggregates, not an average of row-level rates.
- The source is described as sample data; no production coverage, currency, or time window is asserted here.
- Rankings and month comparisons describe this dataset and do not establish why a merchant's volume or rate changed.
