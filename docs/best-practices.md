
## 🚀 Best Practices Followed

---

### ✅ 1. Modular & Scalable DAX Measures

- Centralized all business logic in a clean **“Key Measures” table**.
- Avoided redundant expressions by building on **foundational measures** like `[Net Sales $]`, `[GM_$]`, etc.
- Followed strict **naming conventions**:
  - `snake_case` for raw columns (e.g., `net_sales_amount`)
  - `PascalCase` or descriptive naming for measures (e.g., `Total_COGS_$`)

---

### ✅ 2. Optimized Data Model & File Size

- **Reduced `.pbix` size by ~70MB** by removing unnecessary columns like `gross_price`, `pre_invoice_discount_amount`, etc.
- Used **DAX Studio** to audit column sizes and remove high-cardinality fields.
- Converted static calculated columns into **on-demand DAX measures**, improving model refresh and UI responsiveness.

---

### ✅ 3. Smart Use of Relationships

- Applied **star schema** principles to separate dimension and fact tables for optimal query performance.
- Used `RELATEDTABLE()` in calculated columns only where absolutely necessary.
- Filter propagation and context transitions handled via **explicit relationships** and **CALCULATE logic**.

---

### ✅ 4. Dynamic Visuals & UX Enhancements

- Implemented dynamic measure switching using:
  ```DAX
  P&L Final Value = SWITCH(TRUE(), ...)
  ```
- Created dynamic chart titles like:
```DAX
DAXPerformance Visual Title = 'Key Measures'[Selected P&L Row] & " Performance Over Time"
```
### ✅ 5. Forecasting & Error Analytics
- Designed error analysis KPIs such as:
  -Forecast Accuracy %, Net Error %, Absolute Error, Risk Classification
- Built logic for "Out of Stock" vs "Excess Inventory" detection using:
```DAX
Risk = IF([Net Error]>0, "Excess Inventory", "Out of Stock")
```
### ✅ 6. Page-Level Customization
-Each report page (Finance, Sales, Marketing, Supply Chain) designed with specific metrics and visuals, making storytelling intuitive.
-Visuals re-used smartly across pages via page duplication, reducing design effort and maintaining consistency.

### ✅ 7. Professional Presentation
-Published to Power BI Service (cloud) and synced slicers across pages.
-All visuals titled, slicers aligned, KPIs shown using cards, and tooltips enabled on charts.
-Used area line charts, matrix tables, clustered charts, and waterfall visuals for analytical depth.

