## 🗃️ Dataset Overview

This project utilizes **10 structured tables** from two databases (`gdb041`, `gdb056`), consisting of **over 5 million rows** in total.

| Database | Table Name               | Rows      | Description                          |
|----------|--------------------------|-----------|--------------------------------------|
| gdb041   | dim_customer             | 209       | Customer dimension                   |
| gdb041   | dim_market               | 27        | Market/region dimension              |
| gdb041   | dim_product              | 397       | Product dimension                    |
| gdb041   | fact_forecast_monthly   | 1,885,941 | Monthly-level forecast facts         |
| gdb041   | fact_sales_monthly      | 1,425,706 | Monthly-level actual sales facts     |
| gdb056   | freight_cost            | 135       | Freight cost per product/month       |
| gdb056   | gross_price             | 1,197     | Product-wise gross prices            |
| gdb056   | manufacturing_cost      | 1,197     | Product-wise manufacturing costs     |
| gdb056   | post_invoice_deductions | 2,063,076 | All post-invoice deduction records   |
| gdb056   | pre_invoice_deductions  | 1,045     | All pre-invoice deduction records    |

📂 [Click here to view and download the full dataset ➜](https://drive.google.com/drive/folders/1KzTnRwW2htA8kWJdZNgxXU07UiNzuVuV?usp=sharing)
---

📌 **Total Rows**: ~**5.38 million**  
📂 **Tables Used**: 10  
🔄 **Data Model**: Snowflake Schema with `fact` and `dimension` separation  

