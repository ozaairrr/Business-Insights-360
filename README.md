# 📊 Business Insights 360 – Power BI Dashboard

**A production-grade business intelligence platform that enables comprehensive analysis across Finance, Sales, Marketing, and Supply Chain operations.**

---

## 🎯 The Challenge This Project Solves

**Business Context:**
Zenith Hardware Co. (brick-and-mortar + e-commerce) operates across multiple regions and product categories with complex cost structures. The company needed a unified view across:
- Finance: P&L analysis across 27 product lines and regions
- Sales: Customer and market performance visibility
- Marketing: Product profitability and campaign impact
- Supply Chain: Forecast accuracy and inventory risk

**The Solution:** Built a comprehensive BI platform processing 5.3M+ transaction records, enabling real-time analysis through interactive dashboards.

---

## 📊 Live Dashboard & Download

| Resource | Link |
|----------|------|
| **Interactive Dashboard** | [View Live Power BI Report](https://app.powerbi.com/view?r=eyJrIjoiZTNjMzZiNDAtZjk2ZC00ZGZlLTkwOTYtY2I3ODFlNmZkN2U5IiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9) |
| **PBIX File** | [Download Here](https://drive.google.com/file/d/1k7M7UcfIeiEu56WvFN9JMD6fss_vgSO2/view?usp=sharing) |
| **Video Walkthrough** | [5-min Project Presentation](https://youtu.be/SFmGicFt5u0?si=c4lM4j3QF5-c0WPq) |

![Home View](https://github.com/ozaairrr/Business-Insights-360/blob/9312dfd27f209930d52f48abd0d2dda3245886f0/screenshots/Home.png)

---

## 🔧 What I Built & How It Works

### 1. **Finance View** – Comprehensive P&L Analysis
**Features:**
- Automated P&L statement with 17 cascading metrics (Gross Sales → COGS → Gross Margin → Operating Expense → Net Profit)
- Year-over-Year comparison tracking growth trends by month
- Dimensional breakdown by Region and Segment
- YTD/YTG (Year-To-Date / Year-To-Go) categorization based on latest sales date
- Dynamic filtering with Fiscal Year, Quarter, and time period selection

**What it enables:** Finance teams can drill into any variance instantly instead of spending hours compiling manual reports.

![Finance View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Finance.png)

---

### 2. **Sales View** – Customer & Market Performance
**Features:**
- Customer-level profitability analysis (Net Sales, Gross Margin, GM%)
- Growth matrix scatter chart mapping customers by profitability vs. sales volume
- Market performance comparison with regional hierarchies
- Top/Bottom performer identification
- Interactive slicers: Region, Market, Customer filters

**What it enables:** Sales teams can identify which customer segments are most valuable and where to focus growth efforts.

![Sales View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Sales%20View.png)

---

### 3. **Marketing View** – Product Performance Analysis
**Features:**
- Product hierarchy visualization (Segment → Category → Product)
- Waterfall chart showing profit progression from Gross Margin through Operating Expenses to Net Profit
- Product-level profitability matrix with conditional formatting
- Toggle buttons to switch between GM% and Net Profit% analysis
- Visual filtering to highlight underperforming products

**What it enables:** Marketing teams understand which products drive margin vs. which are volume-only plays.

![Marketing View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Marketing%20View.png)

---

### 4. **Supply Chain View** – Forecast Tracking & Risk Analysis
**Features:**
- Actual vs. Forecast quantity comparison with monthly trend line
- Forecast Accuracy % metric showing prediction reliability per customer/product
- Net Error and Absolute Error calculations
- Risk Classification: Automatically flags "Excess Inventory" vs "Out of Stock" situations
- Customer and Product-level forecast performance tables

**What it enables:** Supply Chain teams measure forecasting accuracy and proactively identify inventory risks before they become problems.

![Supply Chain View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Supply%20Chain%20View.png)

---

### 5. **Executive View** – Strategic KPI Dashboard
**Features:**
- Key metrics summary: Net Sales, Gross Margin %, Net Profit %, Forecast Accuracy, Market Share
- Regional benchmarking with conditional formatting (green/red indicators)
- Top 5 Customers and Products ranked by revenue and margin contribution
- Market share ribbon chart showing Atliq's competitive position vs. Dell, HP, Lenovo, Acer
- Year-over-Year variance tracking

**What it enables:** Executives see health of business at a glance with drill-down capability for deeper analysis.

![Executive View](https://github.com/ozaairrr/Business-Insights-360/blob/33c540fa68995026fe3af94184b310fe139c7670/screenshots/Executive%20View.png)

---

## 🛠️ Technical Implementation

### Data Architecture

| Component | Details |
|-----------|---------|
| **Source Systems** | MySQL Database (2 schemas: gdb041 with 5 dimension/fact tables, gdb056 with 5 cost tables) |
| **Data Volume** | 5.3M+ transaction records spanning fiscal years 2018-2022 |
| **Dimensional Coverage** | 345 products, 209 customers, 27 markets/zones |
| **Data Schema** | Star schema with 10 interconnected tables (6 dimension + 4 fact) |
| **Refresh Strategy** | Hourly incremental loads via Power Query |

### Power Query ETL Transformations

**Date Table Creation:**
- Custom date range (Sep 2017 - Dec 2022) with continuous dates required for DAX time intelligence
- Fiscal year offset: `Date.Year(Date.AddMonths([month], 4))` to align with company's April-start fiscal calendar
- Quarterly and monthly rollups for hierarchical filtering

**Blending Actuals & Forecasts:**
- Created `lastSales_Month` query to identify data cutoff (Dec 1, 2021)
- Built `remainingforecast` table filtering forecasts after sales cutoff
- Appended sales and forecast tables into unified `fact_actuals_estimates` for seamless analysis
- Unified quantity column combines actual sales through Dec 2021 and forecasts for 2022

**Multi-Table Integration:**
- Performed left joins with 5 cost tables (gross_price, manufacturing_cost, freight_cost, pre_invoice_deduction, post_invoice_deduction) on product_code and fiscal_year
- Merged operational expense percentages (Ads, Promotions, Other) from Excel import
- Linked target data by date and market to support benchmark comparison

**Performance Optimization:**
- Disabled loads for 4 intermediate tables (gross_price, freight_cost, etc.) to reduce file bloat
- Selected only required columns in fact tables (date, product_code, customer_code, quantities)
- Removed derived columns from fact table; computed dynamically in DAX instead
- Result: **70MB file size reduction** while maintaining full analytical capability

**Quality Assurance:**
- Renamed and documented all query steps for maintainability
- Grouped related tables into logical sections
- Validated data against Project Owner benchmarks across all fiscal years

### Power BI Data Model

| Component | Specification |
|-----------|---------------|
| **Relationships** | 15 active relationships in star schema configuration |
| **Helper Tables** | Created DAX tables (fiscal_year, sub_zone, category) to resolve many-to-many relationships |
| **DAX Measures** | 40+ custom measures including P&L cascade, forecasting metrics, variance calculations |
| **Interactivity** | Cross-filtering, bookmarks for page navigation, tooltip pages with dynamic titles |
| **Performance** | Dashboard loads in <2 seconds with full filtering capability |

### Key Data Transformations in DAX

**P&L Cascade (17 metrics):**
```dax
-- Core Measures Table
GS $ = SUM(fact_actuals_estimates[gross_sales_amount])
Pre_Invoice_Deduction_$ = [GS $] - [NIS $]
NIS $ = SUM(fact_actuals_estimates[net_invoice_sales_amount])
Post_Invoice_Deduction_$ = SUM(fact_actuals_estimates[post_invoice_deductions_amount])
NS_$ = SUM(fact_actuals_estimates[net_sales_amount])
Total_COGS_$ = [Manufacturing_Cost_$] + [Freight_Cost_$] + [Other_Cost_$]
GM_$ = [Net_Sales] - [Total_COGS_$]
GM_% = DIVIDE([GM_$], [NS_$], 0)
Net Profit $ = [GM_$] - [Operational Expense $]
Net Profit % = DIVIDE([Net Profit $], [NS_$], 0)
```

**Dynamic P&L Display (Single Measure, Multiple Metrics):**
```dax
P&L Values = 
VAR res = SWITCH(TRUE(),
    MAX('P & L Rows'[Order]) = 1, [GS $] / 1000000,
    MAX('P & L Rows'[Order]) = 7, [NS_$] / 1000000,
    MAX('P & L Rows'[Order]) = 12, [GM_$] / 1000000,
    MAX('P & L Rows'[Order]) = 13, [GM_%] * 100,
    MAX('P & L Rows'[Order]) = 16, [Net Profit $] / 1000000)
RETURN IF(HASONEVALUE('P & L Rows'[Description]), res, [NS_$] / 1000000)
```

**Forecast Accuracy Metrics:**
```dax
-- Actual Sales Quantity (through last sales date only)
Sales Qty = CALCULATE([Quantity], 
    fact_actuals_estimates[date] <= MAX(lastSales_Month[lastSales_Month]))

-- Forecast Quantity (on or before last sales date)
Forecast Qty = VAR lastsaledate = MAX(lastSales_Month[lastSales_Month])
    RETURN CALCULATE(SUM(fact_forecast_monthly[forecast_quantity]), 
        fact_forecast_monthly[date] <= lastsaledate)

-- Net Error (Forecast - Actual)
Net Error = [Forecast Qty] - [Sales Qty]
Net Error % = DIVIDE([Net Error], [Forecast Qty], 0)

-- Forecast Accuracy %
Forecast Accuracy % = IF([Absolute Error %] <> BLANK(), 
    1 - [Absolute Error %], BLANK())

-- Risk Classification
Risk = IF([Net Error] > 0, "Excess Inventory Situation", "Out of Stock Situation")
```

**Fiscal Year Time Intelligence:**
```dax
-- YTD vs YTG Categorization
ytd_ytg = 
VAR LASTSALESDATE = MAX(fact_sales_monthly[date])
VAR FYMONTHNUM = MONTH(DATE(YEAR(LASTSALESDATE), MONTH(LASTSALESDATE) + 4, 1))
RETURN IF(dim_date[fy_month_num] > FYMONTHNUM, "YTG", "YTD")

-- Year-over-Year Comparison with Blank Handling
P&L YoY CNG = 
VAR res = [P & L values] - [P&L BM]
RETURN IF(ISBLANK([P&L BM]) || ISBLANK([P & L values]), BLANK(), res)
```

**Target Benchmarking:**
```dax
-- Benchmark Selector (Previous Year vs Target)
NS BM$ = SWITCH(TRUE(),
    SELECTEDVALUE('Set BM'[ID]) = 1, [NS$ LY],
    SELECTEDVALUE('Set BM'[ID]) = 2, [NS Target $])

-- Variance Detection for Conditional Formatting
GM % Variance = [GM % BM] - [GM_%]
GM % Filter = IF([GM % Variance] >= SELECTEDVALUE('Target Gap Tolerance'[Target Gap Tolerance]), 1, 0)
```

**Market Share Analysis:**
```dax
Market Share % = DIVIDE(SUM(marketshare[sales_$]), 
    SUM(marketshare[total_market_sales_$]))

Atliq MarketShare = CALCULATE([Market Share %], 
    marketshare[manufacturer] = "Atliq")
```

---

## 📊 Data Quality & Validation

**Benchmark Validation Against Project Owner Requirements:**

All data cross-checked using record counts and aggregations across fiscal years:

| Metric | FY 2018 | FY 2019 | FY 2020 | FY 2021 | FY 2022 |
|--------|---------|---------|---------|---------|---------|
| **Total Sales Qty** | 3.45M ✓ | 10.78M ✓ | 20.77M ✓ | 50.16M ✓ | - |
| **Total Forecast Qty** | - | - | - | - | 86.82M ✓ |
| **Products Tracked** | - | - | - | - | 345 ✓ |
| **Active Customers** | - | - | - | - | 209 ✓ |
| **Markets/Zones** | - | - | - | - | 27 ✓ |

✅ Validation methodology: Record counts on all dimension and fact table columns matched PO benchmarks for accuracy verification.

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

## 📈 Technical Achievements

| Achievement | Evidence |
|-------------|----------|
| **Data Processing Scale** | 5.3M+ transaction records processed and modeled |
| **File Size Optimization** | 70MB reduction through selective column loading and DAX-based calculations |
| **Dashboard Performance** | <2 second load time on full dataset with multi-table filtering |
| **Dynamic Calculations** | 40+ DAX measures enabling real-time P&L and forecasting analysis without materialized columns |
| **Multi-View Architecture** | 6 specialized analytical dashboards (Finance, Sales, Marketing, Supply Chain, Executive, Market Share) |
| **Data Integration** | Successfully blended 10 data sources including sales, forecasts, costs, and targets |
| **Forecast Framework** | Implemented accuracy metrics and risk classification for inventory management |
| **Time Intelligence** | Fiscal year offset calculations enabling accurate YTD/YTG and year-over-year analysis |
| **Quality Assurance** | Data validated against Project Owner benchmarks; cross-checked across all fiscal years |
| **Interactivity** | Cross-filtering, bookmarks, tooltips, dynamic titles, conditional formatting, parameter sliders |

---

## 🎓 Skills Demonstrated

This project showcases:

- ✅ **Data Modeling:** Star schema design; resolving many-to-many relationships; dimensional hierarchy management
- ✅ **ETL & Data Transformation:** Power Query (M language); append/merge queries; column selection for performance; query folding
- ✅ **DAX Mastery:** 40+ custom measures; dynamic SWITCH logic; CALCULATE context modification; error handling; time intelligence
- ✅ **Performance Optimization:** Query optimization; file size reduction through selective column loading; storage analysis
- ✅ **Power BI Best Practices:** Cross-filtering; bookmarks; tooltip pages; conditional formatting; dynamic calculations
- ✅ **SQL & Database Design:** Complex queries; fact/dimension table structure; data validation
- ✅ **Problem-Solving:** Blending different data sources; handling fiscal year calendars; creating helper tables for relationship resolution
- ✅ **Data Quality:** Validation procedures; benchmark testing; data consistency verification
- ✅ **Advanced Visualizations:** Waterfall charts, scatter plots, ribbon charts, dynamic titles, tooltip dashboards
- ✅ **Communication:** Clear documentation, technical architecture documentation, formula explanations

---

## 🚀 How to Use This Project

### View the Dashboard
1. Click the **[Live Power BI Report](https://app.powerbi.com/view?r=eyJrIjoiZTNjMzZiNDAtZjk2ZC00ZGZlLTkwOTYtY2I3ODFlNmZkN2U5IiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)** link to interact with live data
2. Use slicers to filter by Fiscal Year, Quarter, YTD/YTG period
3. Select Region, Market, Customer, and Product for dimensional analysis
4. Hover over visuals for interactive tooltips
5. Use toggle buttons in Marketing View to compare different metrics
6. Adjust Target Gap Tolerance slider in Sales View to identify variance levels
7. Check the **Video Walkthrough** for a guided tour

### Download & Modify
1. Download the **[PBIX file](https://drive.google.com/file/d/1k7M7UcfIeiEu56WvFN9JMD6fss_vgSO2/view?usp=sharing)**
2. Open in Power BI Desktop
3. Modify data connections to point to your own sources
4. Add new measures by referencing the Key Measures table structure
5. Customize visuals while maintaining dimensional relationships
6. Refer to `docs/dax_formula_reference.md` for measure logic and `docs/etl_process.md` for transformation details

---

## 🔮 Future Enhancements

- [ ] Real-time data integration via Azure Data Factory or SQL scheduled jobs
- [ ] Advanced forecasting models (Prophet/ARIMA) for improved prediction accuracy
- [ ] Customer segmentation analysis (RFM scoring)
- [ ] Automated alerts for KPI anomalies and threshold breaches
- [ ] Mobile-responsive view optimization for executives
- [ ] Predictive churn modeling and customer lifetime value analysis
- [ ] Power BI Premium features: Incremental refresh, Premium capacity optimization
- [ ] Integration with Power BI Paginated Reports for scheduled PDF delivery

---

## 🙌 What I Learned from This Project

**Key Technical Insights:**

1. **Data quality is the foundation** – Spent significant time on validation and cleaning; this prevents countless downstream errors
2. **DAX complexity requires careful architecture** – Complex nested formulas need robust error handling and performance considerations
3. **Business context drives design decisions** – Understanding the actual use case (YTD/YTG logic, fiscal year offset) is crucial for building relevant models
4. **Performance optimization is iterative** – File size reduction required multiple passes: column selection, removing derived columns, optimizing relationships
5. **Many-to-many relationships are complexity multipliers** – Proper dimensional design with helper tables prevents downstream issues
6. **Documentation is a strategic asset** – Clear formula naming and architecture documentation make dashboards maintainable and scalable
7. **User experience matters more than features** – Well-designed slicers and tooltips drive adoption more than additional charts

---

## 📞 Questions & Feedback

If you're reviewing this project:
- 👉 **Start with the [Live Dashboard](https://app.powerbi.com/view?r=eyJrIjoiZTNjMzZiNDAtZjk2ZC00ZGZlLTkwOTYtY2I3ODFlNmZkN2U5IiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)** to see it in action
- 👉 **Watch the [Video](https://youtu.be/SFmGicFt5u0?si=c4lM4j3QF5-c0WPq)** for a guided walkthrough
- 👉 **Check `docs/` folder** for technical depth (DAX formulas, ETL details, best practices)
- 👉 **Review the PBIX file** to examine data model relationships and measure implementations

Questions? Connect on [LinkedIn](https://www.linkedin.com/in/shaikh-mohammad-ozair-connect/) or email mohammadozairshaikh@gmail.com

---

## 📝 Author

**Ozair** – Data Analyst | SQL | Python | Power BI | ETL | Azure

🎓 BCA Graduate specializing in Data Warehousing, Business Intelligence, and Analytics

📧 Email: mohammadozairshaikh@gmail.com  
🔗 LinkedIn: [Shaikh Mohammad Ozair](https://www.linkedin.com/in/shaikh-mohammad-ozair-connect/)  
🐙 GitHub: [@ozaairrr](https://github.com/ozaairrr)

---

**Last Updated:** December 2025  
**Status:** ✅ Production Ready  
**Data Scope:** 5.3M+ Records | FY 2018-2022 | 10 Tables | 40+ Measures

---

## 📄 License & Attribution

This project is built on Atliq Hardware's anonymized business data for portfolio demonstration purposes. All analysis, technical implementation, and data architecture are original work.
