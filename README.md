# Retail Banking: Next Best Action Dashboard

## Project Overview
This project is a Power BI dashboard designed to solve a practical problem I dealt with in retail banking: figuring out exactly who to call for cross-selling. 

Instead of relying on flat, disconnected data exports, I built a data model that combines Retail and SME customer data. The end result is a dashboard that gives Branch Managers and Relationship Managers (RMs) a dynamically ranked call list based on a customer's financial capacity and what products they already hold.

### Core Business Goals
1. **Find Untapped Prospects:** Identify high-capacity customers who do not currently hold specific products (like Insurance).
2. **Prioritize Leads:** Rank these prospects so RMs know exactly who to contact first to maximize conversion chances.
3. **Track RM Performance:** Monitor how individual RMs are performing against their monthly sales targets.

---

## 🏗️ How It Was Built

### 1. Data Modeling (Multi-Fact Star Schema)
I structured the backend to follow dimensional modeling best practices so the DAX measures run efficiently.
* **Unified Customer Dimension:** I used Power Query to append separate Retail (Savings) and SME (Current) datasets into a single `Dim_Customer` master table.
* **Resolving Granularity:** I built a `Dim_Branch` table to act as a bridge. This handles the mismatch between data recorded at the branch level (sales) and data recorded at the RM level (targets).
* **Fact Tables:** Divided the measurable data into `Fact_Sales_Holdings`, `Fact_RM_Performance`, and `Fact_Insurance`.

### 2. DAX Logic
I used DAX to handle the dynamic filtering and ranking rather than hardcoding columns.
* **Dynamic Ranking:** Used `RANKX` inside a `FILTER(ALLSELECTED())` table to rank customers for cross-selling on the fly, which updates automatically when slicers are changed.
* **Cross-Table Filtering:** Used `ISEMPTY()` and `CALCULATETABLE()` to specifically isolate customers in the sales table who do not have a record in the insurance table.
* **Time Intelligence:** Standard YTD calculations for revenue tracking.

### 3. Dashboard Design
I focused on keeping the interface clean and strictly objective so users can find the data they need immediately.
* **Clean Layout:** Removed default visual borders and used a simple, consistent color palette to avoid distractions.
* **Top-Down Flow:** The page flows from high-level KPIs at the top, down to the granular, actionable call list at the bottom.
* **Custom Tooltips:** Added a Report Page Tooltip. When a user hovers over a specific branch on the bar chart, a secondary visual pops up showing the performance of the RMs within that branch, keeping the main page uncluttered.

---

## 📊 Dashboard Previews

### Next-Best-Action Primary Interface
![Main Dashboard](Main_Dashboard.png)

### Dynamic RM Performance Tooltip
![Custom Tooltip](Custom_Tooltip.png)
