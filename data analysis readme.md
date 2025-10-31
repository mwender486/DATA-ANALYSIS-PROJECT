
# 💄 Online Beauty Shop Database & R Analysis

<div align="center">
  <h2><b>Beauty Shop Analytics Project</b></h2>
</div>

## 📗 Table of Contents
- [📖 About the Project](#-about-the-project)
- [🛠 Tech Stack](#-tech-stack)
- [🛍️ Database Schema](#️-database-schema)
- [📥 Sample Data](#-sample-data)
- [🔌 R Connection](#-r-connection)
- [📊 Data Analysis in R](#-data-analysis-in-r)
- [📈 Visualizations](#-visualizations)
- [📁 Project Files](#-project-files)
- [🚀 How to Run](#-how-to-run)
- [✅ Conclusion](#-conclusion)
- [👤 Author](#-author)

---

## 📖 About the Project
This project analyzes an **Online Beauty Shop** using a PostgreSQL database hosted on **Supabase** and visualizes insights using **R + ggplot2**.

---

## 🛠 Tech Stack
| Tool | Purpose |
|------|--------|
| Supabase | PostgreSQL Database |
| RStudio / Posit Cloud | Data analysis & visualization |
| R Libraries | DBI, RPostgres, ggplot2, dplyr |

---

## 🛍️ Database Schema

```sql
CREATE TABLE customers (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  full_name TEXT NOT NULL,
  email TEXT UNIQUE NOT NULL
);

CREATE TABLE products (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  category TEXT,
  price NUMERIC NOT NULL,
  stock INT NOT NULL
);

CREATE TABLE orders (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  customer_id UUID REFERENCES customers(id),
  product_id UUID REFERENCES products(id),
  quantity INT NOT NULL,
  total NUMERIC NOT NULL
);
```

---

## 📥 Sample Data

```sql
INSERT INTO customers (full_name, email) VALUES
('Mary Beauty', 'mary@example.com'),
('Anna Glam', 'anna@example.com'),
('Joy Makeup', 'joy@example.com');

INSERT INTO products (name, category, price, stock) VALUES
('Matte Lipstick', 'Makeup', 15.99, 50),
('Face Serum', 'Skincare', 25.50, 30),
('Body Lotion', 'Skincare', 10.00, 40);
```

---

## 🔌 R Connection

```r
library(DBI)
library(RPostgres)

con <- dbConnect(
  Postgres(),
  host = "YOUR_SUPABASE_HOST",
  port = 5432,
  dbname = "postgres",
  user = "postgres",
  password = "YOUR_PASSWORD",
  sslmode = "require"
)

dbListTables(con)
```

---

## 📊 Data Analysis in R

```r
customers <- dbGetQuery(con, "SELECT * FROM customers;")
products <- dbGetQuery(con, "SELECT * FROM products;")
orders <- dbGetQuery(con, "
  SELECT c.full_name, p.name AS product, o.quantity, o.total
  FROM orders o
  JOIN customers c ON o.customer_id = c.id
  JOIN products p ON o.product_id = p.id;
")
```

---

## 📈 Visualizations

```r
library(ggplot2)

# Customers
ggplot(customers, aes(x = full_name)) +
  geom_bar() +
  theme_minimal() +
  labs(title = "Number of Customers", x = "Customer", y = "Count")

# Product per category
ggplot(products, aes(x = category)) +
  geom_bar() +
  theme_minimal() +
  labs(
    title = "Number of Products by Category",
    x = "Product Category",
    y = "Count"
  )


# Price Distribution
ggplot(products, aes(x = price)) +
  geom_histogram() +
  geom_bar(fill = "green") +
  theme_minimal() +
  labs(title = "Product Price Distribution", x = "Price", y = "Count")
```

---

## Outputs for analaysis and visuaolizations
```r
ustomers <- dbGetQuery(con, "SELECT * FROM customers;")
```
<img width="1920" height="651" alt="image" src="https://github.com/user-attachments/assets/9418d953-86cd-4037-8e30-abb45253f42c" />

```r
# Customers
ggplot(customers, aes(x = full_name)) +
  geom_bar() +
  theme_minimal() +
  labs(title = "Number of Customers", x = "Customer", y = "Count")
```
<img width="1920" height="922" alt="image" src="https://github.com/user-attachments/assets/b21f7f92-b886-47b3-abd7-be1d3ffb509a" />
---

```r
# Product per category
ggplot(products, aes(x = category)) +
  geom_bar() +
  theme_minimal() +
  labs(
    title = "Number of Products by Category",
    x = "Product Category",
    y = "Count"
  )
```
<img width="1920" height="927" alt="image" src="https://github.com/user-attachments/assets/eb319d13-f6f8-41a7-9098-f8e92d7ced7a" />
---

# Price Distribution
ggplot(products, aes(x = price)) +
  geom_histogram() +
  geom_bar(fill = "green") +
  theme_minimal() +
  labs(title = "Product Price Distribution", x = "Price", y = "Count")
<img width="1920" height="904" alt="image" src="https://github.com/user-attachments/assets/88744875-b3ba-4af3-8112-da903412a6b8" />
---



## 📁 Project Files
| File | Description |
|------|------------|
| `README.md` | Project documentation |
| `analysis.R` | Analysis code |
| `data_dictionary.md` | Table definitions |
| `schema.sql` | Database SQL |

---

## 🚀 How to Run
1. Sign in to Posit Cloud  
2. Install required R packages  
3. Run Supabase schema  
4. Connect to DB using R  
5. Execute analysis and view graphs  

---

## ✅ Conclusion
This project demonstrates:

✅ Supabase Database  
✅ SQL Queries  
✅ R Connection & Data Pull  
✅ ggplot2 Visualizations  

---

## 👤 Author
**Your Name — Data Analytics Student**
