# SaaS-Executive-Finance-Dashboard
Interactive two-page Power BI executive application analyzing SaaS financial metrics (MRR, Churn, and Overhead Expense Allocations) using star-schema modeling and advanced filter-aware DAX code.
# SaaS Executive Financial Performance Dashboard

An end-to-end business intelligence application developed in Power BI Desktop to analyze enterprise SaaS recurring revenue vectors, churn dynamics, and proportional operational cost frameworks.

## 📊 Dashboard Architecture & Preview
![SaaS Executive Dashboard Preview](dashboard-preview.png)

*A full, high-fidelity presentation deck detailing both executive summary and granular transactional tables is available in the [Project Presentation PDF](./Power_BI_Export_Portfolio_Guide.pdf) file.*

## 🛠️ Key Technical Implementations
* **Star-Schema Relational Modeling:** Built a clean relational data model linking independent transactional tables (`Fact_Subscriptions` & `Fact_Expenses`) through a custom dynamic DAX `Calendar` dimension table featuring bidirectional cross-filtering mechanics.
* **Advanced DAX Metrics:** Engineered filter-aware calculations for dynamic Time-Intelligence Monthly Recurring Revenue (MRR), conditional Churn Rate tracking, and a dynamic overhead allocation matrix utilizing `DIVIDE` and `ALL` functions to prevent zero-revenue errors.
* **User-Centric Application Layout:** Deployed synchronized cross-page button navigators, customized conditional data matrices, and an integrated automated filter-reset macro action button.

## 🧮 Core DAX Architecture Snippets

### Dynamic Expense Revenue-Share Allocation
```dax
Dynamic Expense Allocation = 
VAR TotalCompanyMRR = CALCULATE([MRR], ALL(dim_customers[Segment]))
VAR SegmentRevenueShare = DIVIDE([MRR], TotalCompanyMRR, 0)
VAR TotalExpenses = SUM(Fact_Expenses[Amount])
RETURN
IF(
    ISBLANK([MRR]) || [MRR] = 0,
    0,
    TotalExpenses * SegmentRevenueShare
)
