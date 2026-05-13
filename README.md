# Retail-Banking-Next-Best-Action-Model
Enterprise Power BI data model utilizing a Multi-Fact Star Schema and advanced DAX to drive Next-Best-Action cross-selling and RM performance analytics.


# Retail Banking: Next Best Action & Performance Model

## Project Overview
This project is an enterprise-grade Business Intelligence solution designed to solve a core retail banking challenge: **Targeted Prospecting and Cross-Selling (Next Best Action)**. 

Rather than relying on flat, siloed data files, this project demonstrates a rigorous ETL pipeline and Data Modeling architecture to unify Retail and SME customer data. The resulting dashboard provides Branch Managers and Relationship Managers (RMs) with automated, dynamically ranked call lists based on financial capacity and existing product holdings.

### Core Business Objectives
1. **Identify Untapped Prospects:** Isolate high-net-worth/high-capacity customers who strictly lack specific product categories (e.g., Insurance).
2. **Dynamic Prioritization:** Algorithmically rank prospects to tell RMs exactly *who* to call first to maximize conversion probability.
3. **Performance Benchmarking:** Track and rank individual RM target achievement within specific branch contexts.

---

## 🏗️ Technical Architecture

### 1. Data Modeling (Multi-Fact Star Schema)
The foundation of this model strictly adheres to dimensional modeling best practices to ensure DAX efficiency and eliminate ambiguous filter contexts.
* **Unified Customer Dimension:** Appended disjointed Retail (Savings) and SME (Current) data sets into a single `Dim_Customer` master table.
* **Conformed Dimensions:** Implemented a standalone `Dim_Branch` to act as a bridging filter between two distinct fact tables with different minimum grains (Branch-level sales vs. RM-level targets).
* **Fact Tables:** Isolated measurable events into `Fact_Sales_Holdings`, `Fact_RM_Performance`, and `Fact_Insurance`.

### 2. Advanced DAX Implementation
Bypassed basic aggregations in favor of complex evaluation context modifiers:
* **Virtual Table Iteration:** Utilized `RANKX` over `FILTER(ALLSELECTED())` to dynamically score customers for cross-selling without permanently altering the physical data model.
* **Cross-Table Logic:** Leveraged `ISEMPTY()` and `CALCULATETABLE()` to identify customers in the Sales Fact table who strictly do not exist in the Insurance Fact table.
* **Time Intelligence:** Implemented standard YTD cumulative metrics using `DATESYTD`.

### 3. UI/UX Design Principles
Designed for executive cognitive clarity.
* **Strict Corporate Palette:** Utilized a strategic FinTech hex-code theme to reduce eye strain and highlight actionable alerts.
* **Information Hierarchy:** Follows a strict Top-Down flow (Global KPIs -> Analytical Context -> Actionable Granular Matrix).
* **Advanced Navigation:** Integrated custom Report Page Tooltips to provide instant RM performance breakdowns upon hovering over branch-level visuals.

---

## 📊 Dashboard Previews
*(Screenshots to be added upon final release)*
* [Insert Screenshot of Main Cross-Sell Dashboard]
* [Insert Screenshot of Custom Hover Tooltip]
