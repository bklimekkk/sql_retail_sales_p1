# Retail Sales Analysis SQL Project

## Project Overview

**Project Title**: Retail Sales Analysis  
**Level**: Beginner – Intermediate  
**Database**: retail_sales

This project showcases SQL skills used in real-world data analytics for retail. The aim is to work with sales transaction data to explore, clean, and analyze business metrics such as total sales, customer behavior, category performance, and time-based trends. The project is suitable for anyone looking to enhance their SQL experience and portfolio with practical business-driven queries.

## Objectives
**1. Create and populate a retail sales table**  
**2. Clean the data** by removing null or incomplete entries  
**3. Perform exploratory data analysis (EDA)**  
**4. Answer business questions using SQL**

## Project Structure
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
