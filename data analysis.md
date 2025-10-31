
# 📖 Beauty Shop Dataset Documentation (Posit + Supabase)

This data dictionary describes all tables, columns, and their meanings for the Beauty Shop project, aligned with the R analysis performed in Posit using Supabase.

---

## **Customers Table**

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| id | UUID PRIMARY KEY | Unique customer ID |
| full_name | TEXT NOT NULL | Full name of the customer |
| email | TEXT UNIQUE NOT NULL | Customer email address |

**Usage in R:**  
* Listing all customers for visualization  
* Joining with `orders` to analyze total spending per customer

---

## **Products Table**

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| id | UUID PRIMARY KEY | Unique product ID |
| name | TEXT NOT NULL | Product name |
| category | TEXT | Beauty product category (Makeup / Skincare etc.) |
| price | NUMERIC NOT NULL | Product price |
| stock | INT NOT NULL | Available stock |

**Usage in R:**  
* Visualizing product categories  
* Analyzing average product price  
* Linking with `orders` to evaluate best-selling beauty items

---

## **Orders Table**

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| id | UUID PRIMARY KEY | Unique order ID |
| customer_id | UUID REFERENCES customers(id) | Customer who made the order |
| product_id | UUID REFERENCES products(id) | Purchased product |
| quantity | INT NOT NULL | Number of units ordered |
| total | NUMERIC NOT NULL | Total cost of the order |

**Usage in R:**  
* Joining with `customers` and `products` to determine top buyers and popular items  
* Summarizing total sales and demand by product

---

## **Relationships**

* **customers → orders**: One-to-many  
* **products → orders**: One-to-many  

This means each customer can place multiple orders and each product can appear in many orders.

---

## **Notes for Posit Analysis**

* `DBI` + `RPostgres` used to connect to Supabase
* Data retrieved using `dbGetQuery()`
* `dplyr` used for filtering and aggregation
* `ggplot2` used for charts:
  - Customers count bar chart
  - Product sales bar chart
  - Product price distribution histogram

---

## ✅ Summary

This Beauty Shop dataset supports analytics such as:

- Best‑selling beauty products
- Customer purchase frequency
- Beauty category trends (makeup vs skincare)
- Price distribution analysis

It demonstrates real‑world data workflow between **Supabase**, **R**, and **GitHub**.

