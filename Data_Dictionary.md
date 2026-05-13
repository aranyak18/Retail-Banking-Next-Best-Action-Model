# Data Dictionary

This document defines the core tables and engineered columns within the unified Star Schema. 

## Dimension Tables

| Table Name | Primary Key | Description | Granularity |
| :--- | :--- | :--- | :--- |
| `Dim_Customer` | `CustomerKey` | Unified master dimension containing both Retail and SME clients. Stripped of all transactional facts. | 1 Row = 1 Unique Customer |
| `Dim_Branch` | `Branch Code` | Conformed dimension bridging RM performance and Sales data. | 1 Row = 1 Unique Branch |
| `Dim_Date` | `DateKey` | Standard continuous calendar table marked as a Date Table for Time Intelligence DAX. | 1 Row = 1 Day |
| `Dim_Product` | `Product ID` | Master list of all banking products offered. | 1 Row = 1 Product |

## Fact Tables

| Table Name | Foreign Keys | Description | Granularity |
| :--- | :--- | :--- | :--- |
| `Fact_Sales_Holdings` | `CustomerKey`, `Branch Code`, `DateKey`, `Product ID` | Contains current balances, average monthly balances, and revenue generated per account. | 1 Row = 1 Account/Holding |
| `Fact_RM_Performance` | `Branch Code` | Tracks monthly sales targets and achieved sales per Relationship Manager. Contains a degenerate dimension (`RM ID`). | 1 Row = 1 RM's Monthly Target |
| `Fact_Insurance` | `CustomerKey`, `Product ID` | Registry of all active insurance policies, premiums, and claim statuses. | 1 Row = 1 Policy |

## Engineered / Custom Columns

| Column Name | Table | M-Code Logic / Description |
| :--- | :--- | :--- |
| `Annual_Financial_Capacity` | `Dim_Customer` | `if [Annual Income] <> null then [Annual Income] else [Annual Turnover]`. Merges disjointed retail income and SME turnover into a single quantifiable capacity metric for cross-sell filtering. |
| `CustomerKey` | `Dim_Customer` | Standardized nomenclature. Renamed and merged from `Customer ID` (Retail) and `Merchant ID` (SME). |