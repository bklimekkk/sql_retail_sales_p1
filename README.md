# 🛍️ Retail Sales Analysis SQL Project

## 📊 Project Overview

**Project Title**: Retail Sales Analysis  
**Level**: Beginner – Intermediate  
**Database**: retail_sales

This project showcases SQL skills used in real-world data analytics for retail. The aim is to work with sales transaction data to explore, clean, and analyze business metrics such as total sales, customer behavior, category performance, and time-based trends. The project is suitable for anyone looking to enhance their SQL experience and portfolio with practical business-driven queries.

## 🎯 Objectives
**1. Create and populate a retail sales table**  
**2. Clean the data** by removing null or incomplete entries  
**3. Perform exploratory data analysis (EDA)**  
**4. Answer business questions using SQL**

## 🧱 Project Structure
### 1. Database Table Creation
```sql
CREATE TABLE IF NOT EXISTS retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,
    customer_id INT,	
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,	
    cogs FLOAT,
    total_sale FLOAT
);
```
### 2. 🔍 Data Exploration & Cleaning
View the data:  
```sql
SELECT * FROM retail_sales;
```
Count total rows:  
```sql
SELECT COUNT(*) FROM retail_sales;
```
Check for missing values:  
```sql
SELECT * FROM retail_sales
WHERE transactions_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR customer_id IS NULL
   OR gender IS NULL
   OR age IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR price_per_unit IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;
```
Delete records with missing data:  
```sql
DELETE FROM retail_sales
WHERE transactions_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR customer_id IS NULL
   OR gender IS NULL
   OR age IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR price_per_unit IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;
```
### 3. 📈 Exploratory Data Analysis (EDA)
Total number of sales:
```sql
SELECT COUNT(*) AS total_sale FROM retail_sales;
```
Number of unique customers:
```sql
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
```
List of unique product categories:
```sql
SELECT DISTINCT category FROM retail_sales;
```
## 🧠 Business Analysis & Insights
### Q1: Retrieve all columns for sales made on '2022-11-05'
```sql
SELECT * FROM retail_sales
WHERE sale_date = '2022-11-05';
```
### Q2: Transactions where category is 'Clothing' and quantity > 3 in November 2022
```sql
SELECT * FROM retail_sales
WHERE category = 'Clothing'
  AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
  AND quantity > 3;
```
### Q3: Total sales and total orders for each category
```sql
SELECT category, 
       SUM(total_sale) AS total_sales, 
       COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
```
### Q4: Average age of customers who purchased items in the 'Beauty' category
```sql
SELECT ROUND(AVG(age), 2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty';
```
### Q5: Transactions where total_sale > 1000
```sql
SELECT * FROM retail_sales
WHERE total_sale > 1000;
```
### Q6: Total number of transactions by gender and category
```sql
SELECT category, gender, COUNT(*) AS total_transactions
FROM retail_sales
GROUP BY category, gender
ORDER BY category;
```
### Q7: Average sale per month and best-selling month of each year
```sql
SELECT year, month, avg_sale 
FROM (
    SELECT 
        EXTRACT(YEAR FROM sale_date) AS year,
        EXTRACT(MONTH FROM sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) 
                    ORDER BY AVG(total_sale) DESC) AS rank
    FROM retail_sales
    GROUP BY 1, 2
) AS ranked_months
WHERE rank = 1;
```
### Q8: Top 5 customers based on highest total sales
```sql
SELECT customer_id, 
       SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
```
### Q9: Unique customers per category
```sql
SELECT category, 
       COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category;
```
### Q10: Orders grouped by shift (Morning, Afternoon, Evening)
```sql
WITH hourly_sale AS (
    SELECT *,
           CASE 
               WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
               WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
               ELSE 'Evening'
           END AS shift
    FROM retail_sales
)
SELECT shift, COUNT(*) AS total_orders
FROM hourly_sale
GROUP BY shift;
```
## 🧰 How to Use
**1. Clone the Repository** from GitHub to your local machine.  
**2. Set Up Your SQL Environment** (PostgreSQL, MySQL, etc.).  
**3. Create the retail_sales table** using the script provided.  
**4. Insert your data** (CSV or SQL insert statements).  
**5. Run the SQL queries** to analyze the data and answer business questions.  
**6. Experiment** by modifying queries or adding your own.

## 👤 Author
**Bartosz Klimek**  
This project is part of my personal portfolio to demonstrate SQL skills for data analysis. Feel free to connect or reach out if you'd like to collaborate or provide feedback!

