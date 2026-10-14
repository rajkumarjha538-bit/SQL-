
# 🍕 Pizza Hut Sales Data Analysis (SQL Project)

A data-driven sales performance analysis project analyzing transactional records from Pizza Hut (2015 dataset) using SQL to extract key business insights, revenue drivers, menu efficiency, and operational trends[cite: 26].

---

## 📌 Executive Summary

Over the 2015 trading period, Pizza Hut processed **21,350 unique orders** comprising **49,574 pizzas sold**, generating a **Total Revenue of $817,860.05** with an **Average Order Value (AOV) of $38.31**[cite: 26].

* **Total Revenue:** $817,860.05[cite: 26]
* **Total Orders:** 21,350[cite: 26]
* **Total Units Sold:** 49,574[cite: 26]
* **Average Order Value (AOV):** $38.31[cite: 26]
* **Daily Average Output:** ~137 pizzas/day[cite: 26]

---

## 📂 Relational Database Architecture

The project utilizes a 4-table relational database model connected through primary and foreign key constraints[cite: 26]:

1. **`orders.csv` (21,350 rows):** Stores order timestamps (`order_id`, `date`, `time`)[cite: 26].
2. **`order_details.csv` (48,620 rows):** Contains line items per order (`order_details_id`, `order_id`, `pizza_id`, `quantity`)[cite: 26].
3. **`pizzas.csv` (96 rows):** SKU menu variants (`pizza_id`, `pizza_type_id`, `size`, `price`)[cite: 26].
4. **`pizza_types.csv` (32 rows):** Recipe and menu metadata (`pizza_type_id`, `name`, `category`, `ingredients`)[cite: 26].

---

## 📊 Key Findings & Business Insights

### 1. Revenue & Volume by Category
* **Classic Category:** Top revenue driver at **$220,053.10** (14,888 units sold)[cite: 26].
* **Supreme Category:** **$208,197.00** revenue (11,987 units)[cite: 26].
* **Chicken Category:** **$195,919.50** revenue (11,050 units) — Highest yield per unit sold[cite: 26].
* **Veggie Category:** **$193,690.45** revenue (11,648 units)[cite: 26].

### 2. Menu Anchors & Size Preferences
* **Large (L) Size Dominance:** Contributes **$375,319 (~46% of total revenue)**, acting as the primary anchor for ticket size[cite: 26].

### 3. Peak Trading Hours & Weekly Trends
* **Busiest Days:** **Friday ($136,074)** and **Thursday ($123,529)** experience highest customer volume, whereas **Sunday ($99,204)** is the slowest day[cite: 26].
* **Peak Ordering Windows:** Lunch rush (**12:00 PM – 1:00 PM**) and dinner peak (**6:00 PM – 8:00 PM**).

### 4. Star Performers
* **Top Revenue Sellers:** *The Thai Chicken Pizza* ($43,434), *The Barbecue Chicken Pizza* ($42,768), and *The California Chicken Pizza* ($41,410)[cite: 26].
* **Top Volume Sellers:** *The Classic Deluxe Pizza* (2,453 units), *The Barbecue Chicken Pizza* (2,432 units), and *The Hawaiian Pizza* (2,422 units)[cite: 26].

---

## 💻 Core SQL Queries

```sql
-- 1. Total Number of Orders
SELECT COUNT(*) AS Total_orders 
FROM orders;

-- 2. Total Gross Revenue
SELECT ROUND(SUM(order_details.quantity * pizzas.price), 2) AS total_revenue
FROM order_details 
JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id;

-- 3. Highest Priced Pizza
SELECT pt.name, p.price
FROM pizzas p
JOIN pizza_types pt ON p.pizza_type_id = pt.pizza_type_id
ORDER BY p.price DESC 
LIMIT 1;

-- 4. Top 5 Most Ordered Pizza Types
SELECT pt.name, SUM(od.quantity) AS total_quantity
FROM order_details od
JOIN pizzas p ON od.pizza_id = p.pizza_id
JOIN pizza_types pt ON p.pizza_type_id = pt.pizza_type_id
GROUP BY pt.name
ORDER BY total_quantity DESC 
LIMIT 5;

-- 5. Daily Average Pizzas Sold (Subquery)
SELECT ROUND(AVG(pizzas_per_day), 0) AS avg_pizzas_per_day
FROM (
    SELECT o.date, SUM(od.quantity) AS pizzas_per_day
    FROM orders o
    JOIN order_details od ON o.order_id = od.order_id
    GROUP BY o.date
) AS daily_totals;

```

---

## 🛠️ Tools & Technologies

* **Database:** MySQL / PostgreSQL
* **Language:** SQL (Joins, Subqueries, Aggregations, GROUP BY, ORDER BY)
* **Documentation:** MS Word (`.docx`), MS PowerPoint (`.pptx`)

---

## 🚀 Strategic Business Recommendations

1. **Upsize Upselling:** Implement checkout prompts for Large (L) size upgrades to increase AOV beyond $38.31.


2. **Kitchen Staffing:** Align staff rosters and ingredient preps for Thursday-Saturday peak dinner hours.


3. **Menu Optimization:** Promote high-margin specialty chicken pizzas on digital channels and combo packages.


4. **Off-Peak Offers:** Introduce Sunday "Family Value Bundles" to boost volume on slow trading days.


