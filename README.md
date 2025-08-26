# 🛒 Retail Sales Analysis (SQL Project)

## 📌 Project Overview
This project analyzes a **retail sales dataset** using SQL.  
The dataset contains transaction-level details such as customer demographics, sales amount, product categories, and transaction timestamps.  

The goal of the project is to perform **data cleaning, exploration, and business analysis** to extract actionable insights for decision-making.

---

## 🗂 Dataset
The dataset `SQL - Retail Sales Analysis_utf.csv` includes the following fields:

- `transactions_id` – Unique identifier for each transaction  
- `sale_date` – Date of transaction  
- `sale_time` – Time of transaction  
- `customer_id` – Unique customer identifier  
- `gender` – Gender of customer  
- `age` – Age of customer  
- `category` – Product category (Clothing, Beauty, Electronics, etc.)  
- `quantity` – Number of items purchased  
- `price_per_unit` – Price of each item  
- `cogs` – Cost of goods sold  
- `total_sale` – Final sale value  

---

## ⚙️ Project Workflow

### 1️⃣ Data Cleaning
- Checked for missing values across all columns  
- Removed records with `NULL` values

```sql

SELECT * FROM retail_sales
WHERE transactions_id IS NULL OR 
	  sale_date IS NULL OR	
	  sale_time IS NULL OR	
	  customer_id IS NULL OR	
	  gender IS NULL OR 	
	  age IS NULL OR	
	  category IS NULL OR	
	  quantity IS NULL OR	
	  price_per_unit IS NULL OR	
	  cogs IS NULL OR	
	  total_sale IS NULL;

SELECT COUNT(*) FROM retail_sales
WHERE transactions_id IS NULL OR 
	  sale_date IS NULL OR	
	  sale_time IS NULL OR	
	  customer_id IS NULL OR	
	  gender IS NULL OR 	
	  age IS NULL OR	
	  category IS NULL OR	
	  quantity IS NULL OR	
	  price_per_unit IS NULL OR	
	  cogs IS NULL OR	
	  total_sale IS NULL;

-- 
DELETE FROM retail_sales
WHERE transactions_id IS NULL OR 
	  sale_date IS NULL OR	
	  sale_time IS NULL OR	
	  customer_id IS NULL OR	
	  gender IS NULL OR 	
	  age IS NULL OR	
	  category IS NULL OR	
	  quantity IS NULL OR	
	  price_per_unit IS NULL OR	
	  cogs IS NULL OR	
	  total_sale IS NULL;

```   

### 2️⃣ Data Exploration
- Counted total sales records  
- Found distinct customers and unique product categories  

### 3️⃣ Business Analysis (Key Queries)
1. Retrieve all sales on **2022-11-05**
```sql
SELECT * 
FROM retail_sales
WHERE sale_date = '2022-11-05';
```
2. Retrieve transactions in **Clothing** category with quantity = 4 in **Nov 2022**  
```sql
SELECT * 
FROM retail_sales
WHERE category = 'Clothing' and 
      quantity >= 4 and 
	  TO_CHAR(sale_date ,'YYYY-MM') = '2022-11';
```
3. Calculate **total sales per category**  
```sql
SELECT category,
       SUM(total_sale) AS net_sales,
       COUNT(category) AS total_orders
FROM retail_sales
GROUP BY category;
```
4. Find **average age** of customers purchasing **Beauty** items  
```sql
SELECT ROUND(AVG(age),1) AS average_age
FROM retail_sales
WHERE category = 'Beauty';
```
5. Retrieve all transactions with `total_sale > 1000`  
```sql
SELECT * 
FROM retail_sales
WHERE total_sale > 1000;
```
6. Find **number of transactions per gender in each category**  
```sql
SELECT gender,
       category, 
       COUNT(transactions_id) AS total_purchase
FROM retail_sales
GROUP BY gender , category
ORDER BY COUNT(transactions_id);
```
7. Find the **best-selling month** in each year using window functions  
```sql
SELECT 
       year,
       month,
    avg_sale
FROM 
(    
SELECT 
    EXTRACT(YEAR FROM sale_date) as year,
    EXTRACT(MONTH FROM sale_date) as month,
    AVG(total_sale) as avg_sale,
    RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) as rank
FROM retail_sales
GROUP BY 1, 2
) as t1
WHERE rank = 1
```
8. Identify **Top 5 customers by highest total purchase**  
```sql
SELECT customer_id, 
       SUM(total_sale) AS total_purchase 
FROM retail_sales
GROUP BY customer_id
ORDER BY SUM(total_sale)
DESC
LIMIT 5;
```
9. Find **unique customers per category**  
```sql
SELECT category, 
       COUNT(DISTINCT(customer_id)) AS unique_customer
FROM retail_sales
GROUP BY category ;
```
10. Categorize transactions by **shifts (Morning, Afternoon, Evening)** based on `sale_time`  
```sql
WITH hourly_sale
AS
(
SELECT *,
    CASE
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift
FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) as total_orders    
FROM hourly_sale
GROUP BY shift;
```
---

## 📊 Key Insights
- **Clothing** and **Electronics** are among the top-selling categories.  
- The **average age** of customers in the Beauty category is around 30 years.  
- Transactions above **1000 units** are rare but high-value.  
- **Top 5 customers** contribute significantly to overall sales.  
- **Evening shift** records the highest number of transactions.  

---

## 🚀 Tech Stack
- **SQL** (PostgreSQL / MySQL / SQL Server)  
- **Dataset:** Retail Sales CSV  

---

## 📁 Files in Repository
- `SQL QUERY PROJECT.sql` → All queries (cleaning, exploration, business analysis)  
- `SQL - Retail Sales Analysis_utf.csv` → Dataset  

---

## 📌 How to Run
1. Create the table using the provided `CREATE TABLE` script.  
2. Import the dataset into your SQL database.  
3. Run the queries from `SQL QUERY PROJECT.sql` step by step.  

---

## 📝 Author
👤 **Anurag Chavan**  
📍 Pune, India | 📧 anuragchavanss123@gmail.com | 📞 9270112046  
