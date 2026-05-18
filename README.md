# 🍕 Pizza Sales Analysis — SQL & Power BI Dashboard

> **End-to-end data analytics project** analysing 48,000+ pizza sales records using SQL for data extraction and validation, and Power BI for interactive dashboard design.

---

##  Project Overview

This project simulates a real-world business analytics engagement where a pizza restaurant client needed a data-driven solution to understand sales performance, customer ordering patterns, and product strategy.

The project follows a **two-phase approach:**
- **Phase 1 SQL:** Write and validate all KPI queries in MS SQL Server
- **Phase 2 Power BI:** Build an interactive dashboard and cross-validate every metric against SQL outputs to guarantee data accuracy

This two-way validation methodology ensures that every number displayed on the dashboard is proven correct — a standard practice in professional data analytics.

---

##  Business Problem

The client (a pizza restaurant owner) needed answers to the following business questions:

| Business Question | Analysis Type |
|---|---|
| What is the total revenue, and how much is each order worth on average? | KPI Metrics |
| Which days and months drive the most orders? | Trend Analysis |
| Which pizza categories and sizes are most popular? | Sales Breakdown |
| Which pizzas should we promote — and which should we cut? | Product Performance |

---

##  Dashboard Preview

### Page 1 — Home (KPI Overview & Trends) 
<img width="1182" height="737" alt="home" src="https://github.com/user-attachments/assets/5596e6e2-7ae1-4bc4-b420-d24deb33982b" />


### Page 2 — Best & Worst Sellers
<img width="1207" height="737" alt="best_worst" src="https://github.com/user-attachments/assets/8be21021-9b47-46d8-8290-14b9b5be11bc" />


---

##  Key Business Insights

### Revenue & Scale
- The business generated **$817,860 in total revenue** across **21,350 orders** in 2015
- Customers spend an average of **$38.31 per order** and order **2.32 pizzas per order** — indicating strong upsell potential through meal bundles or combo deals
- **50,000 pizzas** were sold in total across the year

### Peak Trading Periods
- **Friday is the single busiest day**, followed closely by Thursday and Saturday — together these three days account for a disproportionate share of weekly revenue
- **July is the peak month** with 1,935 orders, while **August sees a sharp 14% drop** to 1,661 — a pattern that signals seasonal sensitivity and an opportunity for targeted August promotions
- **Weekend demand is consistently higher** than midweek — staffing, inventory, and marketing spend should be weighted accordingly

### Product Strategy
- The **Classic category drives the most revenue and volume** — it is the anchor of the menu and should be protected from cost-cutting decisions
- **Large size pizzas dominate at ~46% of all sales** — the business is effectively a large-pizza business; promotions on smaller sizes could open an underserved revenue segment
- **Thai Chicken Pizza** is the single highest revenue-generating product (~$43K), despite not leading on quantity — confirming it commands a premium price point worth protecting
- **Classic Deluxe Pizza** leads in both quantity sold and total orders, making it the most operationally critical SKU for supply chain planning

### Menu Rationalisation Opportunity
- **Brie Carre Pizza** consistently ranks last across all three metrics: Revenue (~$12K), Quantity (490 units), and Total Orders (480) — a strong candidate for menu discontinuation or reformulation
- The bottom 5 pizzas by revenue all fall below $16K, versus $43K for the top performer — a significant long tail that may not justify menu complexity and operational overhead
- Focusing marketing investment on the **top 5 products could disproportionately lift overall revenue** following the 80/20 principle

---

##  Tools & Technologies

| Tool | Purpose |
|---|---|
| **MS SQL Server** | Data import, storage, and KPI query development |
| **SQL (T-SQL)** | Data extraction, aggregation, filtering, and validation |
| **Power BI Desktop** | Interactive dashboard design and visualisation |
| **Power Query (M)** | Data cleaning and transformation |
| **DAX** | Calculated measures and KPIs |

---

##  Dataset

- **Source:** Pizza Sales CSV (flat file)
- **Size:** 48,620 rows × 12 columns
- **Period:** Full year 2015 (1 Jan – 31 Dec)
- **Grain:** One row per pizza sold (not per order)

| Column | Description |
|---|---|
| `pizza_id` | Unique identifier per pizza sold |
| `order_id` | Order identifier (repeats across pizzas in same order) |
| `quantity` | Number of that pizza in the order |
| `order_date` | Date of order |
| `order_time` | Time of order |
| `unit_price` | Price per individual pizza |
| `total_price` | Unit price × quantity |
| `pizza_size` | S / M / L / XL / XXL |
| `pizza_category` | Classic / Supreme / Chicken / Veggie |
| `pizza_ingredients` | Toppings list |
| `pizza_name` | Full pizza name |

---

##  SQL Analysis 

The project includes SQL queries covering:
- KPI Metrics
- Trend Analysis
- Sales Breakdown
- Best & Worst Sellers
All queries are stored in [Pizza.Sale.SQL.Queries.docx](https://github.com/user-attachments/files/27937598/Pizza.Sale.SQL.Queries.docx)


---

##  Data Cleaning Steps

All cleaning was performed in **Power Query** before dashboard construction:

| Issue | Action Taken |
|---|---|
| Pizza size abbreviations (S, M, L, XL, XXL) | Replaced with full labels: Regular, Medium, Large, X-Large, XX-Large |
| No day name column | Extracted day name from `order_date` using Power Query Date functions |
| Day sort order (alphabetical by default) | Created `day_number` conditional column (Sun=1 through Sat=7) and used as sort key |
| Month sort order (alphabetical by default) | Extracted `month_number` and used as sort key for correct Jan–Dec ordering |

---

##  DAX Measures

```dax
Total Revenue      = SUM(pizza_sales[total_price])
Total Orders       = DISTINCTCOUNT(pizza_sales[order_id])
Total Pizzas Sold  = SUM(pizza_sales[quantity])
Avg Order Value    = [Total Revenue] / [Total Orders]
Avg Pizzas/Order   = [Total Pizzas Sold] / [Total Orders]
```

---

##  SQL vs Power BI Validation

Every KPI was cross-validated between SQL output and Power BI to confirm data accuracy:

| KPI | SQL Result | Power BI Result | 
|---|---|---|
| Total Revenue | $817,860 | $817.86K | 
| Avg Order Value | $38.30 | $38.31 | 
| Total Pizzas Sold | 49,574 | 49,574 | 
| Total Orders | 21,350 | 21,350 | 
| Avg Pizzas/Order | 2.32 | 2.32 | 

---

##  Repository Structure

```
## Repository Structure

```text
pizza-sales-analysis/
│
├── README.md
├── Pizza.Sale.SQL.Queries.docx
├── pizza_sales.csv
├── pizza_sales_dashboard.pbix
├── home.png
└── best_worst.png
```

---

##  How to Run This Project

| File | What it shows |
|---|---|
| `pizza_sales_dashboard.pbix` | Open in Power BI Desktop to interact with the full dashboard |
| `SQL/pizza_sales_queries.sql` | All queries with comments — open in SSMS or any SQL editor |
| `KPI_Documentation/` | Query screenshots showing SQL outputs matching Power BI |
| `pizza_sales.csv` | Raw dataset — 48,620 rows, importable into any SQL database |

---

##  Dashboard Features

- 5 KPI cards showing live totals with custom icons
- Interactive slicers filter by Pizza Category and Date Range
- Cross-filtering clicking any chart filters the entire dashboard
- Navigation buttons switch between Home and Best/Worst Sellers pages
- Conditional formatting bar colours scale dynamically with values
- Two-page layout overview dashboard + product performance deep-dive

---

##  Author

**Aswini Karoth Sadanandan**
MSc Business Analytics | Maynooth University, Ireland (2024 -2025)
📧 imaswiniks@gmail.com
[LinkedIn](https://www.linkedin.com/in/aswinikarothsadanandan) | [GitHub](https://github.com/aswiniks-data)




