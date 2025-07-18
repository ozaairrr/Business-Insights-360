## 📊 DAX Formula Reference

A comprehensive list of DAX formulas used throughout the **Business Insights 360** project.
- 📈 Financial Metrics & Profitability  
- 📦 Forecasting & Inventory  
- ⚠️ Risk Identification  
- 📊 Dynamic P&L Reporting  
- 🎯 Benchmark Switching  
- 📌 Revenue Contribution  
- 🏷️ Tooltip / Title Logic  

---

### 📈 Financial Metrics & Profitability


- Net Sales
```DAX
[NS_$] = [NIS $] - [Post_Invoice_Deduction_$] - [Post_Invoice_Other_Deduction_$]
```
- Gross Margin
```DAX
[GM_$] = [NS_$] - [Total COGS_$]
[GM_%] = DIVIDE([GM_$], [NS_$], 0)
[GM/Unit] = DIVIDE([GM_$], [Total Quantity], 0)
```
- Operational Expenses
```DAX
[Ads & Promotional Expense] = SUM(fact_actuals_estimates[ad_promotions])
[Other Operational Expense] = SUM(fact_actuals_estimates[other_operational_expense])
[Operational Expense $] = ([Ads & Promotional Expense] + [Other Operational Expense]) * -1
```
- Net Profit
```DAX
[Net Profit $] = [GM_$] + [Operational Expense $]
[Net Profit %] = DIVIDE([Net Profit $], [NS_$], 0)
```

---

### 📦 Forecasting & Inventory


- Sales Quantity
```DAX
[Sales Qty] = CALCULATE([Quantity], fact_actuals_estimates[date] <= MAX(lastSales_Month[lastSales_Month]))
```
- Forecast Quantity
```DAX
[Forecast Qty] = VAR lastsaledate = MAX(lastSales_Month[lastSales_Month])RETURN CALCULATE(SUM(fact_forecast_monthly[forecast_quantity]), fact_forecast_monthly[date] <= lastsaledate)
```
- Errors & Accuracy
```DAX
[Net Error] = [Forecast Qty] - [Sales Qty]
```
```DAX
[Net Error %] = DIVIDE([Net Error], [Forecast Qty], 0)
[Absolute Error] = 
SUMX(
    DISTINCT(dim_date[month]),
    SUMX(
        DISTINCT(dim_product[product_code]),  
        ABS([Net Error])
    )
)
```
```DAX
[Absolute Error %] = DIVIDE([Absolute Error], [Forecast Qty], 0)
[Forecast Accuracy %] = IF([Absolute Error %] <> BLANK(), 1 - [Absolute Error %], BLANK())
```
- Year-over-Year Accuracy
```DAX
[Forecast Accuracy % LY] = CALCULATE([Forecast Accuracy %], SAMEPERIODLASTYEAR(dim_date[date]))
```

---

### 📅 Time Intelligence


- YTD vs YTG
```DA
[ytd_ytg] = 
VAR LASTSALESDATE = MAX(lastSales_Month[lastSales_Month])
VAR FYMONTHNUM = MONTH(DATE(YEAR(LASTSALESDATE), MONTH(LASTSALESDATE) + 4, 1))
RETURN IF(dim_date[fy_month_num] > FYMONTHNUM, "YTG", "YTD")
```

---

### ⚠️ Risk Identification


- Inventory Risk
```DAX
[Risk] = IF([Net Error] > 0, "Excess Inventory Situation", "Out of Stock Situation")
```

---

### 📊 Dynamic P&L Reporting

```DAX
P & L values = 
VAR res = SWITCH(
    TRUE(),
    MAX('P & L Rows'[Order]) = 1, [GS $] / 1000000,
    MAX('P & L Rows'[Order]) = 2, [Pre_Invoice_Deduction_$] / 1000000,
    MAX('P & L Rows'[Order]) = 3, [NIS $] / 1000000,
    MAX('P & L Rows'[Order]) = 4, [Post_Invoice_Deduction_$] / 1000000,
    MAX('P & L Rows'[Order]) = 5, [Post_Invoice_Other_Deduction_$] / 1000000,
    MAX('P & L Rows'[Order]) = 6, [Post_Invoice_Deduction_$] / 1000000 + [Post_Invoice_Other_Deduction_$] / 1000000,
    MAX('P & L Rows'[Order]) = 7, [NS_$] / 1000000,
    MAX('P & L Rows'[Order]) = 8, [Manufacturing_Cost_$] / 1000000,
    MAX('P & L Rows'[Order]) = 9, [Freight_Cost_$] / 1000000,
    MAX('P & L Rows'[Order]) = 10, [Other_Cost_$] / 1000000,
    MAX('P & L Rows'[Order]) = 11, [Total_COGS_$] / 1000000,
    MAX('P & L Rows'[Order]) = 12, [GM_$] / 1000000,
    MAX('P & L Rows'[Order]) = 13, [GM_%] * 100,
    MAX('P & L Rows'[Order]) = 14, [GM/Unit],
    MAX('P & L Rows'[Order]) = 15, [Operational Expense $]/1000000,
    MAX('P & L Rows'[Order]) = 16, [Net Profit $]/1000000,
    MAX('P & L Rows'[Order]) = 17, [Net Profit %]*100
)
RETURN
IF(HASONEVALUE('P & L Rows'[Description]), res, [NS_$]/1000000)

```
### 📌 Revenue Contribution
```DAX
[RC %] = DIVIDE([NS_$], CALCULATE([NS_$], ALL(dim_customer)), 0)
```
---
### 🏷️ Tooltip / Title Logic
```DAX
Sales Trend Title = "Monthly Trend: " & SELECTEDVALUE(dim_customer[customer_name], "All Customers")
```
---

📝 *This file serves as a quick reference guide for advanced calculations and business logic implemented in Power BI using DAX.*

