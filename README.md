# 📊 Sales Analysis with SQLiteStudio & Jupyter Notebook

This project demonstrates how to analyze a small sales dataset using **SQLite** for storage and **Jupyter Notebook** for querying and visualization. It’s designed as a beginner-friendly introduction to working with databases and Python for data analysis.

---

## 🔧 Tools & Technologies

- 🗃️ SQLiteStudio (for creating and managing the database)
- 📓 Jupyter Notebook (for executing SQL and visualizing data)
- 🐍 Python
- 📦 pandas
- 📊 matplotlib
- 🔌 sqlite3 (Python’s built-in SQLite library)

---

## 🗂️ Dataset Overview

The database is named `sales_data.db` and contains a single table: `sales`

### Table Schema


CREATE TABLE sales (
    Product TEXT,
    Quantity INTEGER,
    Price REAL
);

INSERT INTO sales (Product, Quantity, Price) VALUES 
('Crimson Kiwi', 7, 1.45),
('Alpine Honey Jar', 3, 5.80),
('Velvet Mango', 2, 2.75),
('Sea Salt Crackers', 4, 3.10),
('Glacier Water 500ml', 6, 1.25),
('Basil Oat Cookies', 5, 2.40),
('Dried Dragonfruit', 1, 4.60),
('Smoked Tofu Block', 2, 3.90),
('Lemon Quinoa Mix', 3, 2.85),
('Midnight Coffee Pods', 8, 6.20);

### SQL Queries Used

-- View all sales data
SELECT * FROM sales;

-- View only product names
SELECT Product FROM sales;

-- Get total quantity sold
SELECT SUM(Quantity) AS total_qty FROM sales;

-- Get total revenue by product
SELECT 
    Product, 
    SUM(Quantity) AS total_qty, 
    SUM(Quantity * Price) AS revenue 
FROM sales 
GROUP BY Product;

### Python Code

import sqlite3
import pandas as pd
import matplotlib.pyplot as plt

-- Connect to SQLite database
conn = sqlite3.connect(r"C:\Users\sushmita\OneDrive\Desktop\sales_data.db")

-- SQL query
query = """
SELECT 
    Product, 
    SUM(Quantity) AS total_qty, 
    SUM(Quantity * Price) AS revenue 
FROM sales 
GROUP BY Product;
"""

-- Load result into DataFrame
df = pd.read_sql_query(query, conn)

-- Close the database connection
conn.close()

-- Print the result
print(df)

-- Plotting
df.plot(kind='bar', x='Product', y='revenue', legend=False, color='skyblue')
plt.title("Revenue by Product")
plt.xlabel("Product")
plt.ylabel("Revenue ($)")
plt.xticks(rotation=45)
plt.tight_layout()

- Save the chart to file
plt.savefig(r"C:\Users\sushmita\Desktop\sales_chart.png", dpi=300)

-- Optional: Show the chart
plt.show()

