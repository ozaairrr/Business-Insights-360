<h1 align="center">📊 Business Insights 360-Powerbi Project</h1>

A powerful business intelligence dashboard built using **Power BI**, enabling a 360° view into Finance, Sales, Marketing, and Supply Chain operations.

This dashboard helps decision-makers and analysts identify trends, improve profitability, forecast accurately, and analyze performance across various dimensions like product, market, region, and customer.

--- 
## 📈 Live Dashboard Demo

> 📊 [View Interactive Power BI Report](https://app.powerbi.com/view?r=eyJrIjoiZTNjMzZiNDAtZjk2ZC00ZGZlLTkwOTYtY2I3ODFlNmZkN2U5IiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)

> 📦 [Download Full PBIX File → Click here](https://drive.google.com/file/d/1k7M7UcfIeiEu56WvFN9JMD6fss_vgSO2/view?usp=sharing).

> 📽️ [Project Presentation](https://youtu.be/SFmGicFt5u0?si=c4lM4j3QF5-c0WPq)


---

![Home View](https://github.com/ozaairrr/Business-Insights-360/blob/9312dfd27f209930d52f48abd0d2dda3245886f0/screenshots/Home.png) 

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

![Finance View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Finance.png)

---

### 🔹 Sales View
- Customer-wise Net Sales, Gross Margin, GM%
- Scatter chart showing region-wise profitability matrix
- Market and product-level performance comparison
- Unit economics breakdown visualized via donut charts

![Sales View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Sales%20View.png)

---

### 🔹 Marketing View
- Extended product hierarchy (Segment > Category > Product)
- Net Profit and Net Profit % visualizations
- Waterfall chart showing P&L movement from GM to Net Profit
- Updated logic: Operational Expenses shown as negative contributions

![Marketing View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Marketing%20View.png)

---

### 🔹 Supply Chain View
- Forecast vs Actuals sales quantity
- Net Error and Forecast Accuracy % per month
- Risk profiling: Out-of-stock vs Excess Inventory situations
- Customer & Product forecast performance evaluation

![Supply Chain View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Supply%20Chain%20View.png)

---
### 🔹 Executive View

- 📊 Consolidated KPIs: Net Sales, GM %, NP %, Forecast Accuracy, Market Share  
- 🌍 Regional snapshot with benchmark comparisons & conditional formatting  
- 🏆 Top performers: Customers & Products ranked by revenue and GM %  
 

![Executive View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Executive%20View.png)

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

> 👉 [See full list of best practices here](docs/best-practices.md)

---

## 🔍 Key Metrics & DAX Logic

- 📊 **Net Profit $** = Gross Margin + Operational Expense (negative sign handled in formula)  
- 🎯 **Forecast Accuracy %** = 1 – Absolute Error  
- 🚨 **Risk Classification** = Excess Inventory / Out of Stock based on Net Error  
- 🧠 **Dynamic P&L**: SWITCH logic to drive matrix values across 17 P&L stages  
- 📅 **YTD vs YTG Logic**: Dynamically classifies months into “Year-To-Date” or “Year-To-Go” using latest sales date  
- 🔀 **Benchmark Switching**: GM % & NP % switch between LY vs Target based on slicer selection  

> 👉 [Explore full DAX logic here ➜](https://github.com/ozaairrr/Business-Insights-360/blob/7f271a6882e71b8cf74dd1bdf3a9d84ba679cea8/docs/dax_formula_reference.md)

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
|   ├── improvements.md
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

> 🔗 [Click here to view full dataset breakdown ➜](https://drive.google.com/drive/folders/1KzTnRwW2htA8kWJdZNgxXU07UiNzuVuV?usp=sharing)

---

📦 Download the Full PBIX File  
> 👉 [Click here to access the dashboard PBIX file](https://drive.google.com/file/d/1k7M7UcfIeiEu56WvFN9JMD6fss_vgSO2/view?usp=sharing)  

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

**Ozair** – Aspiring Data Analyst  
>📧 Contact: [LinkedIn](https://www.linkedin.com/in/shaikh-mohammad-ozair-connect/)

🎓 BCA Graduate | Specializing in Data Warehousing, Python, SQL, Azure and Power BI

---

## 📝 Notes

> This README is structured for GitHub and meant for recruiters, collaborators, or viewers assessing the quality, business relevance, and technical implementation of this Power BI dashboard project.

