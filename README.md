# 📊 AtliQ Hardwares: Sales & Product Performance Analysis (MySQL)

> Ten SQL queries that turn AtliQ Hardwares' raw sales, product, and customer tables into decision-ready answers on portfolio growth, channel dependence, seasonality, and discounting.

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Business Problem](#-business-problem)
- [Dataset](#-dataset)
- [Tools & SQL Techniques](#-tools--sql-techniques)
- [Business Questions & SQL Files](#-business-questions--sql-files)
- [Key Insights](#-key-insights)
- [How to Run This Project](#-how-to-run-this-project)
- [Results & Conclusion](#-results--conclusion)
- [Scope & Limitations](#-scope--limitations)
- [Future Work](#-future-work)
- [Author & Contact](#-author--contact)

---

## 📝 Overview

AtliQ Hardwares is a computer hardware company in India with growing international operations. This project uses MySQL to answer ten management questions across **products, markets, customers, channels, and sales trends**.

Each query answers one business question, and each finding is paired with what it means for the business, so the focus stays on **interpretation, not just query output**.

---

## ❗ Business Problem

AtliQ Hardwares lacked structured insights for quick, data-informed decisions. Leadership needed clarity on:

- How the product portfolio is evolving
- Which segments are driving growth
- How sales performance varies over time
- Whether revenue is concentrated across channels, products, or customers
- How discounts are being applied

**Core challenge:** transform raw relational data into decision-ready insights using SQL.

---

## 🔢 Dataset

| Table | Purpose |
|---|---|
| `dim_customer` | Customer, market, region, and channel attributes |
| `dim_product` | Product, variant, segment, and division attributes |
| `fact_sales_monthly` | Monthly sold quantity and fiscal year |
| `fact_gross_price` | Gross price per product by fiscal year |
| `fact_manufacturing_cost` | Manufacturing cost per product |
| `fact_pre_invoice_deductions` | Pre-invoice discount percentage per customer |

> **Fiscal year note:** AtliQ's fiscal year starts in **September** (the queries shift dates by 4 months), so **Fiscal Q1 = Sep–Nov, Q2 = Dec–Feb, Q3 = Mar–May, Q4 = Jun–Aug**.
>
> **"Atliq Exclusive"** is a customer in `dim_customer`. Queries 1 and 7 are about this customer only, not the whole company.

---

## 🛠 Tools & SQL Techniques

- **MySQL**, **GitHub**
- Joins and filtering (`INNER JOIN`, `LEFT JOIN`, `USING`)
- Aggregations: `SUM`, `AVG`, `MIN`, `MAX`, `COUNT(DISTINCT)`
- Conditional aggregation for year-over-year comparison
- CTEs and subqueries
- Window function `DENSE_RANK()` for top-N per group
- Date transformations for monthly and fiscal-quarter analysis
- Percentage-of-total calculations

---

## 🔍 Business Questions & SQL Files

| File | Business question |
|---|---|
| `Mgmt_Request_1.sql` | In which APAC markets does Atliq Exclusive operate? |
| `Mgmt_Request_2.sql` | What is the percentage increase in unique products, 2021 vs 2020? |
| `Mgmt_Request_3.sql` | How many unique products does each segment have? |
| `Mgmt_Request_4.sql` | Which segment gained the most unique products, 2021 vs 2020? |
| `Mgmt_Request_5.sql` | Which products have the highest and lowest manufacturing cost? |
| `Mgmt_Request_6.sql` | Which 5 Indian customers got the highest average pre-invoice discount in FY2021? |
| `Mgmt_Request_7.sql` | What are Atliq Exclusive's monthly gross sales? |
| `Mgmt_Request_8.sql` | Which fiscal quarter of FY2020 had the highest sold quantity? |
| `Mgmt_Request_9.sql` | Which channel brought the most gross sales in FY2021, and what is its share? |
| `Mgmt_Request_10.sql` | What are the top 3 products by sold quantity in each division in FY2021? |

---

## 📊 Key Insights

| # | Query | Finding | What it means |
|---|---|---|---|
| 1 | Q2, Q4 | Unique products with recorded sales grew from **245 (FY2020) to 334 (FY2021), +36.33%**. Biggest gains: **Accessories +34**, Notebook +16, Peripherals +16, Desktop +15. | Growth is skewed toward Accessories rather than spread across the portfolio. |
| 2 | Q3 | Product count by segment: **Notebook 129**, **Accessories 116**, **Peripherals 84**. | The portfolio is concentrated in a few large segments, which raises complexity and dependency in them. |
| 3 | Q9 | In FY2021, **Retailer brought 73.23%** of gross sales (~1,219 mn), Direct 15.47%, Distributor 11.30%. | Revenue leans heavily on one channel, which limits control over pricing and customer relationships. |
| 4 | Q7 | Atliq Exclusive's sales were **near zero in Mar–May 2020** and peaked in **Sep–Nov at ~20 mn per month**. | Sales for this customer are uneven, so demand planning has to allow for seasonality and sudden drops. |
| 5 | Q8 | FY2020 sold quantity by fiscal quarter: **Q1 7.0M**, Q2 6.6M, **Q3 2.0M**, Q4 5.0M units. | Volume is uneven across the year. Q3 (Mar–May) is the weakest, the same window where Atliq Exclusive's sales were near zero. |
| 6 | Q10 | The top 3 products per division (FY2021) range from **~17K to ~700K units** across divisions. | A few products carry very high volumes, so their share of total sales is worth tracking. |
| 7 | Q6 | The top 5 Indian customers by average pre-invoice discount (FY2021) all sit in a tight band: **Flipkart ~30.83%**, Croma, Viveks and Ezone ~30%, Amazon ~29%. | Discounts at the top end are uniformly high. A margin analysis is needed to judge the impact on profit. |
| 8 | Q5 | Manufacturing cost ranges from **0.89 to 240.54**, roughly a **270x spread**. | Product-level margins are likely to differ widely, so cost-to-price analysis is a natural next step. |
| 9 | Q1 | Atliq Exclusive operates across APAC markets including **India, Japan, Indonesia, South Korea, and Australia**. | Multi-market presence leaves room for region-specific strategies. |

---

## ▶️ How to Run This Project

1. **Clone the repository**
   ```bash
   git clone https://github.com/Sahajahanur/Finance-And-Supply-chain-Analytics-by-MySQL.git
   cd Finance-And-Supply-chain-Analytics-by-MySQL
   ```
2. **Load the AtliQ Hardware dataset** into MySQL. The six tables in the [Dataset](#-dataset) section must be available.
3. **Run the queries** `Mgmt_Request_1.sql` to `Mgmt_Request_10.sql` in MySQL Workbench or any SQL client. The question for each is in the comment block at the top of the file.
4. **Compare the outputs** with the [Key Insights](#-key-insights) table.

**Project structure**

```text
Finance-And-Supply-chain-Analytics-by-MySQL/
├── Mgmt_Request_1.sql
├── Mgmt_Request_2.sql
├── Mgmt_Request_3.sql
├── Mgmt_Request_4.sql
├── Mgmt_Request_5.sql
├── Mgmt_Request_6.sql
├── Mgmt_Request_7.sql
├── Mgmt_Request_8.sql
├── Mgmt_Request_9.sql
├── Mgmt_Request_10.sql
└── README.md
```

---

## ✅ Results & Conclusion

AtliQ Hardwares shows **strong growth that is concentrated**: in a few segments (Accessories), in one channel (Retailer), and in a small group of high-volume products. Sales are uneven across months and quarters, and the top customers receive discounts of around 30%.

**Skills demonstrated**

- Translating business problems into SQL queries
- Combining multiple tables to generate insight
- Using CTEs, conditional aggregation, and window functions
- Moving from raw data to business implications

---

## ⚠️ Scope & Limitations

- Descriptive and diagnostic analysis only: no profitability analysis, predictive modeling, or customer segmentation.
- Queries 1 and 7 cover the customer **Atliq Exclusive** only.
- Query 6 covers the **top 5 Indian customers** by average discount, not all customers.
- The findings describe what the data shows. They do not establish why a pattern occurred.

---

## 🚀 Future Work

- Profitability and margin analysis by product
- Channel-wise margin comparison
- Customer segmentation
- Interactive dashboard in Power BI

---

## 👤 Author & Contact

**Sahajahanur Rahman Laskar**

- 📧 Email: connectingsrl@gmail.com
- 💼 LinkedIn: [linkedin.com/in/sahajahanur-laskar](https://www.linkedin.com/in/sahajahanur-laskar/)
- 🐙 GitHub: [github.com/Sahajahanur](https://github.com/Sahajahanur)
- 🌐 Portfolio: [codebasics.io/portfolio/SAHAJAHANUR-LASKAR](https://codebasics.io/portfolio/SAHAJAHANUR-LASKAR)
