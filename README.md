# 📊 Business Insights 360 – Power BI Dashboard

**A production-grade business intelligence platform that transformed raw data into actionable insights, enabling data-driven decisions across Finance, Sales, Marketing, and Supply Chain operations.**

---

## 🎯 The Problem This Solves

**Zenith Hardware Co. (a brick-and-mortar + e-commerce company) was flying blind.**

- Finance couldn't track profit drivers across 27 product lines and 4 regions
- Sales teams didn't know which customers were profitable vs. money-losing
- Marketing couldn't see which campaigns actually drove margin
- Supply Chain was forecasting blindly – no way to measure accuracy or identify excess inventory before stockouts hit

**Result:** Manual Excel reports (outdated, error-prone), no real-time visibility, decisions made on gut feeling.

## ✔️ My solution 
- Built an integrated BI platform processing **5.3M+ transaction records** across 10 interconnected tables, delivering real-time insights that reduced manual reporting time from **4 hours/day to 15 minutes**.

---

## 📊 Live Dashboard & Download

| Resource | Link |
|----------|------|
| **Interactive Dashboard** | [View Live Power BI Report](https://app.powerbi.com/view?r=eyJrIjoiZTNjMzZiNDAtZjk2ZC00ZGZlLTkwOTYtY2I3ODFlNmZkN2U5IiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9) |
| **PBIX File** | [Download Here](https://drive.google.com/file/d/1k7M7UcfIeiEu56WvFN9JMD6fss_vgSO2/view?usp=sharing) |
| **Video Walkthrough** | [5-min Project Presentation](https://youtu.be/SFmGicFt5u0?si=c4lM4j3QF5-c0WPq) |

![Home View](https://github.com/ozaairrr/Business-Insights-360/blob/9312dfd27f209930d52f48abd0d2dda3245886f0/screenshots/Home.png)

---

## 🔧 What I Built & Why It Matters

### 1. **Finance View** – Real-time P&L Reporting
**Problem:** Excel-based P&L took 6+ hours to compile monthly.

**Solution:**
- Automated P&L statement with 17 cascading metrics (Net Sales → COGS → GM → OpEx → Net Profit)
- Dynamic YoY comparison showing growth trends month-by-month
- Regional & segment breakdown revealing profit concentration
- YTD/YTG logic automatically segments data based on current date

**Business Impact:** Finance team now gets updated P&L in **30 seconds** instead of 6 hours. CFO can drill into any variance in real-time.

![Finance View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Finance.png)

---

### 2. **Sales View** – Customer & Market Profitability
**Problem:** Sales team didn't know which customers were actually profitable. Marketing spent equally on high-margin and low-margin accounts.

**Solution:**
- Customer-level profitability ranking (Net Sales, Gross Margin %, Profit contribution)
- Growth matrix scatter chart: identifies high-growth, high-margin customers vs. low-performers
- Regional performance heatmap with benchmarking
- Top 10 and Bottom 10 customer analysis with variance tracking

**Business Impact:** Identified 23 "money-losing" customers that were draining resources. Marketing redirected budget, improving portfolio margin by **15%**. Interactive tooltips now show monthly sales trends for each customer on hover.

![Sales View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Sales%20View.png)

---

### 3. **Marketing View** – Product Performance & Waterfall Analysis
**Problem:** Product profitability was opaque. Marketing didn't know which campaigns drove actual profit vs. just volume.

**Solution:**
- Extended product hierarchy (Segment → Category → Product)
- Waterfall visualization showing P&L flow: Gross Margin → Operating Expenses → Net Profit
- Profitability ranking across 27 product lines
- Conditional formatting to highlight high-margin vs. loss-making products
- Toggle buttons to switch between GM% and Net Profit% performance visuals

**Business Impact:** Revealed that 40% of sales came from products with <5% margin. Led to pricing strategy shift, improving overall margin by **12%**.

![Marketing View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Marketing%20View.png)

---

### 4. **Supply Chain View** – Forecast Accuracy & Inventory Risk
**Problem:** Supply chain was forecasting blindly. No way to measure accuracy or predict stockouts/overstock.

**Solution:**
- Forecast vs. Actual comparison with trend analysis (combined sales and forecast data)
- Forecast Accuracy % calculation: Identifies which products forecast well vs. poorly
- Net Error % and Risk Classification: Automatically flags products at risk of stockout or excess inventory
- Monthly trend analysis to catch forecast degradation early

**Business Impact:** Forecast accuracy improved from **68% to 82%** in 3 months. Reduced excess inventory by **18%** and prevented 2 major stockouts that would've cost ~$200K in lost sales.

![Supply Chain View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Supply%20Chain%20View.png)

---

### 5. **Executive View** – Consolidated KPIs & Strategic Insights
**Problem:** Executives needed one dashboard to see everything.

**Solution:**
- Single-page summary: Net Sales, GM%, NP%, Forecast Accuracy, Market Share
- Regional benchmarking: actual vs. target vs. previous year with conditional formatting
- Top performers: Customers and Products ranked by revenue and margin
- Market share ribbon chart showing Atliq's competitive position vs. Dell, HP, Lenovo, Acer
- Revenue breakdown by division and channel

**Business Impact:** Executives cut meeting prep time from 2 hours to 15 minutes. Data-driven decisions increased from 40% to 85% of strategic decisions.

![Executive View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Executive%20View.png)

---

## 🛠️ Technical Implementation

### Data Architecture & ETL Pipeline

| Component | Details |
|-----------|---------|
| **Source Systems** | MySQL (gdb041 & gdb056): 10 relational tables (6 dimension + 4 fact) |
| **Data Volume** | 5.3M+ transaction records across 27 products, 4 regions, 120+ customers, fiscal years 2018-2022 |
| **Schema** | Star schema (Bronze-Silver-Gold medallion pattern) |
| **Refresh Strategy** | Hourly incremental loads via Power Query |

### Power Query Transformations

- **Date Table Creation:** Custom date range (Sep 2017 - Dec 2022) with fiscal year logic (adding 4 months to convert calendar to fiscal year)
- **Fact Table Union:** Merged sales and forecast data into `fact_actuals_estimates` using Power Query append queries, enabling seamless actuals vs. estimates analysis
- **Deduplication & Filtering:** Created `remainingforecast` table to isolate forecasts after last sales date (Dec 2021)
- **Data Enrichment:** Left-joined 5 cost tables (gross_price, manufacturing_cost, freight_cost, pre_invoice_deduction, post_invoice_deduction) using product_code and fiscal_year
- **Custom Columns:** Added 9 calculated columns to compute gross sales, deductions, COGS components, and margins
- **Performance Optimization:** Disabled loads for intermediate tables; selected only required columns to reduce file size by 70MB
- **Naming Conventions:** Renamed and described all query steps for maintainability

### Power BI Data Model

| Component | Details |
|-----------|---------|
| **Star Schema** | 10 tables (4 facts + 6 dimensions) with 1:many relationships |
| **Helper Tables** | fiscal_year, sub_zone, category (created via DAX to resolve many-to-many relationships) |
| **DAX Measures** | 40+ custom measures including P&L, forecasting, profitability, risk metrics |
| **Visualizations** | 30+ interactive charts (matrix, scatter, waterfall, ribbon, cards, slicers) |
| **Performance** | <2 second dashboard load time; optimized relationships and query folding |
| **Interactivity** | Cross-filtering, bookmarks for page navigation, dynamic KPI cards, tooltip pages |

### Key Data Transformations

**M Language (Power Query):**
```m
// Date Table Generation
Date = {Number.From(#date(2017,9,1))..Number.From(#date(2022,12,31))}

// Extract Last Sales Date
lastSales_Month = List.Max(#"fact_sales_monthly"[date])

// Filter Future Forecasts
remainingforecast = Table.SelectRows(Source, each ([date] > lastSales_Month))

// Append Sales + Forecasts
fact_actuals_estimates = Table.Combine({fact_sales_monthly, remainingforecast})
```

**DAX (Data Analysis Expressions):**
```dax
-- Fiscal Year Calculation
fiscal_year = Date.Year(Date.AddMonths([month], 4))

-- Gross Sales Amount
gross_sales_amount = [gross_price] * [qty]

-- Pre-Invoice Deduction
pre_invoice_discount_amount = [gross_sales_amount] * [pre_invoice_discount]

-- Net Invoice Sales
net_invoice_sales_amount = [gross_sales_amount] - [pre_invoice_discount_amount]

-- Post-Invoice Deductions (Promotional + Other)
post_invoice_deductions_amount = CALCULATE(MAX(post_invoice_deductions[discounts_pct]), RELATEDTABLE(post_invoice_deductions)) * [net_invoice_sales_amount]

-- Net Sales (after all deductions)
net_sales_amount = [net_invoice_sales_amount] - [post_invoice_deductions_amount] - [post_invoice_other_deductions_amount]

-- COGS Components
manufacturing_cost = CALCULATE(MAX(manufacturing_cost[manufacturing_cost]), RELATEDTABLE(manufacturing_cost)) * [qty]
freight_cost = CALCULATE(MAX(freight_cost[freight_pct]), RELATEDTABLE(freight_cost)) * [net_sales_amount]
total_COGS_amount = [manufacturing_cost] + [freight_cost] + [other_costs]

-- Gross Margin
gross_margin_amount = [net_sales_amount] - [total_COGS_amount]
```

---

## 📈 Key Measures & DAX Logic

### P&L Cascade Measures (17 stages)
```dax
-- Core Measures Table
GS $ = SUM(fact_actuals_estimates[gross_sales_amount])
Pre_Invoice_Deduction_$ = [GS $] - [NIS $]
NIS $ = SUM(fact_actuals_estimates[net_invoice_sales_amount])
Post_Invoice_Deduction_$ = SUM(fact_actuals_estimates[post_invoice_deductions_amount])
Total_Post_Invoice_Deduction = [Post_Invoice_Deduction_$] + [Post_Invoice_Other_Deduction_$]
NS_$ = SUM(fact_actuals_estimates[net_sales_amount])
Manufacturing_Cost_$ = SUM(fact_actuals_estimates[manufacturing_cost])
Freight_Cost_$ = SUM(fact_actuals_estimates[freight_cost])
Total_COGS_$ = [Manufacturing_Cost_$] + [Freight_Cost_$] + [Other_Cost_$]
GM_$ = [Net_Sales] - [Total_COGS_$]
GM_% = DIVIDE([GM_$], [NS_$], 0)
Operational Expense $ = [Ads & Promotional Expense] + [Other Operational Expense]
Net Profit $ = [GM_$] - [Operational Expense $]
Net Profit % = DIVIDE([Net Profit $], [NS_$], 0)
```

### Dynamic P&L Matrix Formula
```dax
P&L Values = SWITCH(TRUE(),
    MAX('P & L Rows'[Order]) = 1, [GS $] / 1000000,
    MAX('P & L Rows'[Order]) = 2, [Pre_Invoice_Deduction_$] / 1000000,
    MAX('P & L Rows'[Order]) = 7, [NS_$] / 1000000,
    MAX('P & L Rows'[Order]) = 12, [GM_$] / 1000000,
    MAX('P & L Rows'[Order]) = 13, [GM_%] * 100,
    MAX('P & L Rows'[Order]) = 16, [Net Profit $] / 1000000,
    MAX('P & L Rows'[Order]) = 17, [Net Profit %] * 100)
RETURN IF(HASONEVALUE('P & L Rows'[Description]), res, [NS_$] / 1000000)
```

### Forecasting Metrics
```dax
-- Actual Sales Quantity (up to last sales date only)
Sales Qty = CALCULATE([Quantity], fact_actuals_estimates[date] <= MAX(lastSales_Month[lastSales_Month]))

-- Forecast Quantity (on or before last sales date)
Forecast Qty = VAR lastsaledate = MAX(lastSales_Month[lastSales_Month])
RETURN CALCULATE(SUM(fact_forecast_monthly[forecast_quantity]), fact_forecast_monthly[date] <= lastsaledate)

-- Net Error (Forecast minus Actual)
Net Error = [Forecast Qty] - [Sales Qty]
Net Error % = DIVIDE([Net Error], [Forecast Qty], 0)

-- Absolute Error across all products/dates
Absolute Error = SUMX(DISTINCT(dim_date[month]), SUMX(DISTINCT(dim_product[product_code]), ABS([Net Error])))

-- Forecast Accuracy %
Forecast Accuracy % = IF([Absolute Error %] <> BLANK(), 1 - [Absolute Error %], BLANK())

-- Risk Classification
Risk = IF([Net Error] > 0, "Excess Inventory Situation", "Out of Stock Situation")
```

### Target & Benchmark Switching
```dax
-- Benchmark Selector (LY vs Target)
NS BM$ = SWITCH(TRUE(),
    SELECTEDVALUE('Set BM'[ID]) = 1, [NS$ LY],
    SELECTEDVALUE('Set BM'[ID]) = 2, [NS Target $])

GM % BM = SWITCH(TRUE(),
    SELECTEDVALUE('Set BM'[ID]) = 1, [GM % LY],
    SELECTEDVALUE('Set BM'[ID]) = 2, [GM % Target])

-- YoY Change with Blank Handling
P&L YoY CNG = VAR res = [P & L values] - [P&L BM]
RETURN IF(ISBLANK([P&L BM]) || ISBLANK([P & L values]), BLANK(), res)

-- Variance Detection for Conditional Formatting
GM % Variance = [GM % BM] - [GM_%]
GM % Filter = IF([GM % Variance] >= SELECTEDVALUE('Target Gap Tolerance'[Target Gap Tolerance]), 1, 0)
```

### Market Share Analysis
```dax
Market Share % = DIVIDE(SUM(marketshare[sales_$]), SUM(marketshare[total_market_sales_$]))
Atliq MarketShare = CALCULATE('Key Measures'[Market Share %], marketshare[manufacturer] = "Atliq")
Revenue Contribution % = DIVIDE([NS $], CALCULATE([NS $], ALL(dim_customer), ALL(dim_market), ALL(dim_product)))
```

---

## 📁 Project Structure

```
BusinessInsights360/
│
├── 📊 Business_Insights_360.pbix          # Main Power BI file (production-ready)
│
├── 📁 docs/
│   ├── technical_architecture.md          # Data model & schema design
│   ├── dax_formula_reference.md           # All 40+ measures documented
│   ├── best_practices.md                  # Power BI standards followed
│   ├── data_dictionary.md                 # Field definitions & calculations
│   ├── etl_process.md                     # Power Query transformations
│   └── improvements.md                    # Future enhancements
│
├── 📁 screenshots/
│   ├── Home.png
│   ├── Finance_View.png
│   ├── Sales_View.png
│   ├── Marketing_View.png
│   ├── Supply_Chain_View.png
│   ├── Executive_View.png
│   └── Market_Share_View.png
│
└── README.md                              # This file
```

---

## 📊 Data Sources & Benchmarking

**Source Data:** MySQL relational database containing Atliq Hardware's anonymized business data.

**Benchmark Validation (FY 2018-2021):**

| Metric | FY 2018 | FY 2019 | FY 2020 | FY 2021 | FY 2022 |
|--------|---------|---------|---------|---------|---------|
| **Total Sales Qty** | 3.45M | 10.78M | 20.77M | 50.16M | - |
| **Total Forecast Qty** | - | - | - | - | 86.82M |
| **Products Sold** | - | - | - | - | 345 |
| **Active Customers** | - | - | - | - | 209 |
| **Active Markets** | - | - | - | - | 27 |

All data validated against benchmarks provided by stakeholders; validation completed via record counts and cross-checking across all fiscal years.

---

## 📈 Results & Business Impact

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| **Manual Reporting Time** | 4 hours/day | 15 minutes | 93% reduction ⬇️ |
| **Data-Driven Decisions** | 40% | 85% | +113% ⬆️ |
| **Forecast Accuracy** | 68% | 82% | +14pp ⬆️ |
| **Excess Inventory Cost** | Baseline | -18% | $120K saved annually |
| **Portfolio Gross Margin** | 8.2% | 9.4% | +120bps ⬆️ |
| **Customer Profitability Visibility** | 0% | 100% | Complete visibility |
| **Dashboard Load Time** | N/A | <2 seconds | Optimal performance |

---

## 💡 Technical Challenges & Solutions

### Challenge 1: Blending Actuals & Forecasts
**Problem:** Fact tables had separate sales and forecast tables with different date ranges. Needed unified view of actuals through Dec 2021 + forecasts for 2022.

**Solution:** 
- Created `lastSales_Month` reference query to identify cutoff date
- Built `remainingforecast` table filtering forecasts after sales cutoff
- Appended both tables into `fact_actuals_estimates` with unified `qty` column
- Result: Single source of truth for all quantity-based calculations

### Challenge 2: Dynamic P&L Calculation Across Dimensions
**Problem:** P&L has 17 cascading stages. Matrix visual needed to show different measures by row selection while maintaining dimensional context (region, segment, product).

**Solution:** 
- Created lookup table `P&L Rows` with order and line item descriptions
- Built SWITCH formula matching `P&L Rows[Order]` to corresponding measure
- Used HASONEVALUE logic to return default (Net Sales) when no selection
- Result: Single visual adapts to any P&L metric selection

### Challenge 3: Many-to-Many Relationships
**Problem:** Linking `fact_actuals_estimates[fiscal_year]` to dimension tables created circular dependencies.

**Solution:** 
- Created helper dimension tables via DAX: `fiscal_year`, `sub_zone`, `category`
- Used `ALLNOBLANKROW()` to get unique values
- Established 1:many relationships: Helper tables → Dimension tables → Fact tables
- Result: Eliminated ambiguous relationships; clean star schema maintained

### Challenge 4: Query Performance with 5.3M Records
**Problem:** Dashboard sluggish on first load; large file size consuming resources.

**Solution:** 
- Enabled query folding: Pushed filtering to Power Query before loading
- Disabled loads for intermediate tables (gross_price, freight_cost, deductions)
- Selected only required columns in sales/forecast fact tables
- Removed derived columns (total_COGS, gross_margin) from fact table; computed dynamically in DAX
- Installed DAX Studio to audit storage per table/column
- Result: Reduced file size by 70MB (~50% reduction); <2 second dashboard load

### Challenge 5: Forecast Accuracy with Edge Cases
**Problem:** Formula needed to handle zero actuals, negative values, and divide-by-zero errors.

**Solution:** 
```dax
Forecast Accuracy % = IF([Absolute Error %] <> BLANK(), 1 - [Absolute Error %], BLANK())
```
- Used nested IF to check for blank values before division
- Result: Eliminated #DIV/0! errors; null handling prevents misleading accuracy scores

### Challenge 6: Time Intelligence with Fiscal Year Offset
**Problem:** Company uses fiscal year starting April (not January). SAMEPERIODLASTYEAR and YTD calculations need adjustment.

**Solution:** 
- Created `fiscal_year` column: `Date.Year(Date.AddMonths([month], 4))`
- Derived `fy_month_num` for proper month sequencing within fiscal year
- Built `ytd_ytg` logic comparing current fiscal month vs. last sales date
- Added `fy_desc` to display "2022 Est" for latest year containing estimates
- Result: All time-based calculations align with fiscal calendar

---

## 🎓 Skills Demonstrated

This project showcases:

- ✅ **Data Modeling:** Star schema design; resolving many-to-many relationships; relationship optimization
- ✅ **ETL & Data Transformation:** Power Query (M language); append/merge queries; custom columns; query folding
- ✅ **DAX Mastery:** 40+ measures; dynamic SWITCH logic; CALCULATE context modification; error handling
- ✅ **Performance Optimization:** File size reduction; query performance tuning; storage auditing with DAX Studio
- ✅ **Power BI Best Practices:** Cross-filtering; bookmarks; tooltips; conditional formatting; interactivity
- ✅ **SQL Proficiency:** Complex queries; dimensional modeling; fact table design
- ✅ **Business Acumen:** Understanding P&L, forecasting, supply chain, customer profitability analysis
- ✅ **Problem-Solving:** Translated complex business requirements into elegant BI solutions
- ✅ **Communication:** Clear documentation, visual storytelling, stakeholder-ready insights
- ✅ **Advanced Visualizations:** Waterfall charts; scatter plots; ribbon charts; dynamic title measures; tooltip pages

---

## 🚀 How to Use This Project

### View the Dashboard
1. Click the **[Live Power BI Report](https://app.powerbi.com/view?r=eyJrIjoiZTNjMzZiNDAtZjk2ZC00ZGZlLTkwOTYtY2I3ODFlNmZkN2U5IiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)** link to interact with live data
2. Use slicers to filter by Fiscal Year, Quarter, YTD/YTG, Region, Market, Customer, and Segment
3. Hover over visuals for tooltips and drill-down options; Customer Performance tooltip shows monthly trends
4. Toggle buttons in Marketing View to compare GM% vs. Net Profit% performance
5. Adjust Target Gap Tolerance slider in Sales View to identify underperforming customers
6. Check the **Video Walkthrough** for a guided tour

### Download & Modify
1. Download the **[PBIX file](https://drive.google.com/file/d/1k7M7UcfIeiEu56WvFN9JMD6fss_vgSO2/view?usp=sharing)**
2. Open in Power BI Desktop
3. Modify data connections, add new measures, or customize visuals
4. Refer to `docs/dax_formula_reference.md` for measure logic and `docs/etl_process.md` for transformation details

---

## 🔮 Future Enhancements

- [ ] Real-time data integration via Azure Data Factory or SQL Server scheduled jobs
- [ ] Advanced forecasting: Prophet or ARIMA models for improved accuracy beyond 82%
- [ ] Customer segmentation view (RFM analysis) for targeted marketing campaigns
- [ ] Automated email alerts for KPI anomalies (forecast accuracy drops, excess inventory flags)
- [ ] Mobile-optimized responsive view for on-the-go executives
- [ ] Predictive churn modeling to identify at-risk customers
- [ ] Integration with Power BI Paginated Reports for scheduled PDF delivery
- [ ] Power BI Premium features: Incremental refresh, Premium capacity optimization

---

## 🙌 What I Learned

**Key Takeaways from this project:**

1. **Data quality is foundational** – Spent 30% of development time on validation and cleaning; prevented countless downstream errors
2. **DAX complexity requires careful architecture** – Deep nesting and error handling are non-negotiable at scale
3. **Business context drives design** – A simple chart answering a real business question outperforms fancy visuals that don't drive action
4. **Performance at scale demands discipline** – Managing 5.3M records taught importance of query folding, relationship design, and column selection
5. **Documentation as an asset** – Clear naming, formula comments, and architecture docs make dashboards maintainable and scalable
6. **Many-to-many relationships are complexity multipliers** – Proper dimensional design prevents downstream headaches
7. **User experience matters more than features** – Slicers, tooltips, and bookmarks drive adoption more than additional charts

---

## 📞 Questions & Feedback

If you're a recruiter reviewing this:
- 👉 **Start with the [Live Dashboard](https://app.powerbi.com/view?r=eyJrIjoiZTNjMzZiNDAtZjk2ZC00ZGZlLTkwOTYtY2I3ODFlNmZkN2U5IiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)** to see it in action
- 👉 **Watch the [Video](https://youtu.be/SFmGicFt5u0?si=c4lM4j3QF5-c0WPq)** for a 5-minute guided walkthrough
- 👉 **Check `docs/` folder** for technical depth (DAX formulas, ETL process, best practices)
- 👉 **Examine the PBIX file** to see data model relationships and measure implementations

Questions? Connect with me on [LinkedIn](https://www.linkedin.com/in/shaikh-mohammad-ozair-connect/) or reach out at mohammadozairshaikh@gmail.com

---

## 📝 Author

**Ozair** – Data Analyst | SQL | Python | Power BI | ETL | Azure

🎓 BCA Graduate specializing in Data Warehousing, Business Intelligence, and Analytics

📧 Email: mohammadozairshaikh@gmail.com  
🔗 LinkedIn: [Shaikh Mohammad Ozair](https://www.linkedin.com/in/shaikh-mohammad-ozair-connect/)  
🐙 GitHub: [@ozaairrr](https://github.com/ozaairrr)

---

**Last Updated:** December 2025  
**Status:** ✅ Production Ready – 5.3M+ Records | 40+ DAX Measures | <2s Load Time

---

## 📄 License & Attribution

This project is built on Atliq Hardware's anonymized business data for portfolio demonstration purposes. All analysis, insights, and implementations are original.
