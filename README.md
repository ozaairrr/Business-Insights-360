<h1 align="center">📊 Business Insights 360-Powerbi Project</h1>

A powerful business intelligence dashboard built using **Power BI**, enabling a 360° view into Finance, Sales, Marketing, and Supply Chain operations.

This dashboard helps decision-makers and analysts identify trends, improve profitability, forecast accurately, and analyze performance across various dimensions like product, market, region, and customer.

---
## 📈 Live Dashboard Demo

> 📊 **[👉 View Interactive Power BI Report](https://app.powerbi.com/view?r=eyJrIjoiNzZmZWExNTctNTI4YS00MjAzLWEyNGUtYzNlMjczZWI0ODlhIiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)**  
Explore the complete financial, marketing, sales, and supply chain insights in real-time.

---

![Home View](https://github.com/ozaairrr/Business-Insights-360/blob/2b6e0dae6face216abc712533394655dd0605d00/screenshots/Home.png?raw=true) 

---

## 📊 Overview

**Business Insights 360** is a multi-page Power BI report featuring:

- **Finance View**: Complete Profit & Loss (P&L) reporting with YoY change analysis
- **Sales View**: Customer & market performance, growth matrix, unit economics
- **Marketing View**: Product category breakdown with profit metrics & waterfall visuals
- **Supply Chain View**: Forecast accuracy, net error metrics, and inventory risk profiling
- **Executive View**: (Placeholder for top-level KPIs and summary)
- **Support & Info Pages**: Guide users through understanding and using the dashboard

---

## 🚀 Key Features

### 🔹 Finance View
- Profit & Loss statement table with dynamic Year, Quarter, and YTD/YTG filters
- Trend line charts for net sales performance
- Donut charts for Net Sales vs Deductions & COGS analysis
- Matrix views by Region and Segment to analyze revenue and profit breakdown

![Finance View](https://github.com/ozaairrr/Business-Insights-360/blob/2b6e0dae6face216abc712533394655dd0605d00/screenshots/Finance%20View.png?raw=true)

---

### 🔹 Sales View
- Customer-wise Net Sales, Gross Margin, GM%
- Scatter chart showing region-wise profitability matrix
- Market and product-level performance comparison
- Unit economics breakdown visualized via donut charts

![Sales View](https://github.com/ozaairrr/Business-Insights-360/blob/2b6e0dae6face216abc712533394655dd0605d00/screenshots/Sales%20View.png?raw=true)

---

### 🔹 Marketing View
- Extended product hierarchy (Segment > Category > Product)
- Net Profit and Net Profit % visualizations
- Waterfall chart showing P&L movement from GM to Net Profit
- Updated logic: Operational Expenses shown as negative contributions

![Marketing View](https://github.com/ozaairrr/Business-Insights-360/blob/2b6e0dae6face216abc712533394655dd0605d00/screenshots/Marketing%20View.png?raw=true)

---

### 🔹 Supply Chain View
- Forecast vs Actuals sales quantity
- Net Error and Forecast Accuracy % per month
- Risk profiling: Out-of-stock vs Excess Inventory situations
- Customer & Product forecast performance evaluation

![Supply Chain View](https://github.com/ozaairrr/Business-Insights-360/blob/2b6e0dae6face216abc712533394655dd0605d00/screenshots/Supply%20Chain%20View.png?raw=true)

---
### 🔹 Executive View
- High-level KPIs summarizing Net Sales, GM %, Net Profit %, Forecast Accuracy, and Market Share  
- Revenue distribution analysis by Division and Channel using donut charts  
- Regional summary table showing Sub-Zone-wise metrics (NS $, GM %, RC %, NP %, Net Error, Risk, Market Share %) with conditional formatting  
- Benchmark comparison of GM % vs Target using down arrows for underperformance  
- Multi-metric performance trend chart combining NS $, GM %, NP %, and Market Share %  
- Market Share evolution over time (ribbon chart) for top manufacturers  
- Top 5 Customers and Products by Revenue with GM % and RC %  
- Interactive filtering, bookmarks, and selective visual interaction applied  

![Executive View](https://github.com/ozaairrr/Business-Insights-360/blob/417577f0b6aa243e4d079a874842ece6bb2c0806/screenshots/Executive%20View.png)

## 🛠️ Technical Stack

| Component              | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| **Power BI Desktop**   | Core dashboard building and DAX calculations                                |
| **Power BI Service**   | Published and shared dashboard on the web                                   |
| **Power Query**        | Data transformation and ETL logic                                           |
| **DAX Measures**       | All KPIs and metrics including P&L, Forecast Accuracy, Net Error etc.       |
| **Excel**              | Used as source for Operational Expense % and Forecast values                |
| **SQL Database**       | Primary source for fact and dimension data                                  |

---

## ✅ Best Practices Followed

A few highlights from the many professional standards followed in this report:

- 📦 Centralized and modular **Key Measures** table.
- 📉 Smart forecasting logic using **Forecast Accuracy %**, **Net Error %**, and **Risk Classification**.
- 🧠 Clean and optimized **star schema data model** with minimized column bloat.
- 🧮 Dynamic titles, measure switching, and visual adaptability via DAX logic.
- 📊 Interactive page design: Finance, Sales, Marketing, and Supply Chain.
- 🚀 Lightweight `.pbix` file via data cleanup and memory audits.

👉 [See full list of best practices here](docs/best-practices.md)

---

## 🔍 Metrics & Measures

### Key DAX Measures:

- **[Net Profit $]** = `[GM_$] + [Operational Expense $]`
- **[Operational Expense $]** = `([Ads & Promo Exp] + [Other Op Exp]) * -1`
- **[Forecast Accuracy %]** = `1 - Absolute Error %`
- **[Risk]** = `IF([Net Error]>0, "Excess Inventory", "Out of Stock")`
- **P&L values logic**: Dynamic measure using SWITCH based on P&L Row table

## 🧠 Advanced DAX Formulas (Showcase)

These highlight the depth of logic and complexity handled in this project⤵️:

### Dynamic Profit & Loss Reporting
```DAX
P&L values = 
VAR res = 
    SWITCH(
        TRUE(),
        MAX('P & L Rows'[Order]) = 1, [GS $] / 1000000,
        MAX('P & L Rows'[Order]) = 2, [Pre_Invoice_Deduction_$] / 1000000,
        MAX('P & L Rows'[Order]) = 3, [NIS $] / 1000000,
        ...
        MAX('P & L Rows'[Order]) = 17, [Net Profit %] * 100
    )
RETURN
IF(HASONEVALUE('P & L Rows'[Description]), res, [NS_$] / 1000000)
```
### Year-To-Date vs Year-To-Go Logic
```DAX
ytd_ytg = 
VAR LASTSALESDATE = MAX(lastSales_Month[lastSales_Month])
VAR FYMONTHNUM = MONTH(DATE(YEAR(LASTSALESDATE), MONTH(LASTSALESDATE) + 4, 1))
RETURN
IF(dim_date[fy_month_num] > FYMONTHNUM, "YTG", "YTD")
```
🔧 For a full breakdown of DAX measures and formulas used in this project — including Forecast Accuracy, Dynamic P&L logic, Risk flags, and more — check out:

👉 [`DAX Formula Reference`](https://github.com/ozaairrr/Business-Insights-360/blob/97ee5d44cc3b238d71a317a1b341c03a2ed68c66/docs/datasource_breakdown.md)

---

## 📁 Project Structure

```plaintext
BusinessInsights360/
│
├── 📊 Power BI (.pbix File)
├── 📁 docs
|   ├── best-practices.md
|   ├── dax_formula_reference.md
|   ├── data_source_breakdown.md
├── 📁 screenshots/
│   ├── Home.png
│   ├── Finance View.png
│   ├── Sales View.png
│   ├── Marketing View.png
│   └── Supply Chain View.png
├── README.md
```
---
## 📊 Data Sources

This report is powered by 10 relational tables (dimensional + fact) containing over **5.3 million records**, modeled in a star schema.

🔗 [Click here to view full dataset breakdown ➜](datasets.md)
---

## 📈 Use Cases

- Evaluate **customer profitability** and growth
- Identify **underperforming products** or markets
- Detect **supply chain inefficiencies** and reduce forecast errors
- Understand the financial impact of **promotional expenses**
- Enable **executives and analysts** to make informed decisions quickly

---

## 📌 Conclusion

This Power BI project demonstrates:
- Deep understanding of DAX and Power BI visual capabilities
- Analytical thinking and business acumen across departments
- A complete, production-grade dashboard ready for business presentation

---

## 🙌 Author

**Ozair** – Aspiring Data Engineer & Analyst  
📧 Contact: [LinkedIn](https://www.linkedin.com/in/shaikh-mohammad-ozair-connect/)

🎓 BCA Graduate | Specializing in Data Warehousing, Python, SQL, Azure and Power BI

---

## 📝 Notes

> This README is structured for GitHub and meant for recruiters, collaborators, or viewers assessing the quality, business relevance, and technical implementation of this Power BI dashboard project.

