## 🔧 Business Insights 360 — Project Enhancements & Fixes
- This document outlines key improvements, fixes, and new features added to the original Power BI project "Business Insights 360". These updates refine performance, add new functionality, and increase realism based on stakeholder needs.
---
## 📊 Market Share Integration
### 1. Added Market Share Excel Data:
	• Data includes total market sales and manufacturer-level sales for brands like Atliq, Dell, HP, Lenovo, Acer, etc.
	• Data is available by fiscal year and sub-zone.
### 2. Cleaned & Normalized Data:
	• Corrected misspelled manufacturer names: e.g., dale → Dell, illovo → Lenovo, pacer → Acer, etc.
### 3. Resolved Many-to-Many Issues:
	• Created helper table sub_zone = ALLNOBLANKROW(dim_market[sub_zone])
	• Linked dim_market[sub_zone] → sub_zone[sub_zone] → marketshare[sub_zone]
	• Repeated same process for category via new category table
### 4. Built Market Share View:
	• Matrix visual with category on rows, fy_desc & manufacturer on columns, and value as:
Market Share % = DIVIDE(SUM(marketshare[sales_$]), SUM(marketshare[total_market_sales_$]))
	• Converted matrix to Ribbon chart to show manufacturer growth over time
	• Key Insight: Dell dominated overall; Atliq grew strongly post-2021 in SE (16%) and India (13%)

## ⚙️ Forecast Logic & Formula Fixes
### 5. Fixed Forecast Quantity Measure:
 ```DAX
Forecast Qty =
VAR lastsaledate = MAX(lastSales_Month[lastSales_Month])
RETURN
CALCULATE(SUM(fact_forecast_monthly[forecast_quantity]), fact_forecast_monthly[date] <= lastsaledate)
 ```
### 6. Fixed Chart Visibility Issues:
	• Line + column visuals no longer show future forecast values beyond Dec 2022
### 7. Renamed Measures for Clarity:
	• Renamed Net Error % to Absolute Error % to reflect correct metric

📈 KPI Enhancements
### 8. GM % in Performance Charts:
	• Replaced GM $ with GM % in matrix visuals on both Sales View and Marketing View
### 9. Added Footer Info on Home Page:
	• let Source = #table(type table[Last Refreshed Date = datetime], {{DateTime.LocalNow()}}) in Source
	• Added: "Sales data loaded until: [Date]", "All values in $ and Millions"

🎯 Targets & Benchmark Slicers
### 10. Integrated New Target Data:
	• Monthly targets for NS, GM, NP by market
### 11. Model Adjustments:
	• Linked targets[month] ↔ dim_date[date]
	• Linked targets[market] ↔ dim_market[market]
### 12. Created Target Measures:
NS Target $
GM Target
NP Target
### 13. Replaced KPI Target Values:
	• Updated Net Sales, GM %, NP % KPIs to use respective Target values
	• Noted missing data pre-2022 causes LY fields to return BLANK
### 14. Created Benchmark Slicer Table:
	• Set BM with values: 1 = vs LY, 2 = vs Target
### 15. SWITCH-Based Dynamic Measures:
 ```DAX
NS BM $ = SWITCH(TRUE(), SELECTEDVALUE('Set BM'[ID])=1, [NS$ LY], SELECTEDVALUE('Set BM'[ID])=2, [NS Target])
GM % BM = SWITCH(TRUE(), ..., [GM % LY], ..., [GM % Target])
NP % BM = SWITCH(TRUE(), ..., [NP % LY], ..., [NP % Target])
 ```
### 16. Rebuilt P&L Target Logic:
 ```DAX
P&L Target = ... (returns dynamic rows based on selected P&L Row order)
P&L BM = SWITCH(TRUE(), ..., [P&L LY], ..., [P&L Target])
 ```
### 17. Adjusted P&L Comparison Measures:
 ```DAX
P&L YoY CNG = VAR res = [P & L values] - [P&L BM] RETURN IF(..., res)
 ```
📉 Underperforming Customer Highlight Logic
### 18. Created Parameter Slider:
	• Slicer named Target Gap Tolerance (e.g., 10% GM % threshold)
### 19. Created Filtering Logic:
 ```DAX
GM % Variance = [GM % BM] - [GM_%]
GM % Filter = IF([GM % Variance] >= SELECTEDVALUE('Target Gap Tolerance'[Target Gap Tolerance]), 1, 0)
 ```
### 20. Applied Visual Level Filter:
	• Performance matrix shows only customers failing GM % target beyond selected threshold

🧠 UX Enhancements
### 21. Added Dynamic Visual Toggle (Marketing View):
	• Used bookmarks + buttons to toggle between GM % vs NS and NP % vs NS visuals
### 22. Sales Trend Tooltip:
	• Created new page for customer-level tooltip
	• Shows NS $ and GM % trends by month on hover using line chart
 ```DAX
Sales Trend Title = "NS & GM % For: " & SELECTEDVALUE(dim_customer[customer])
 ```
📌 Note
For details on Executive View and new Market Share visuals, refer to the main README or Executive Dashboard section.

📎 Next Steps
	• Continue improving benchmark logic with dynamic toggles for all KPI visuals
	• Add detailed commentary in tooltips for context
	• Clean up model further by removing unused relationships

> ### ✅ Improvements like these reflect deep dashboard understanding, stakeholder empathy, and real-world data modeling skills.
- Feel free to ⭐️ the main project repo or check out the live demo!

- 🔗 [Main Repo: Business Insights 360](https://github.com/ozaairrr/Business-Insights-360)

- 📊 [Live Dashboard: Business Insights 360 (Power BI Service)](https://app.powerbi.com/view?r=eyJrIjoiNzZmZWExNTctNTI4YS00MjAzLWEyNGUtYzNlMjczZWI0ODlhIiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)


