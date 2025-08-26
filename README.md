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

--- sql

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

---   

### 2️⃣ Data Exploration
- Counted total sales records  
- Found distinct customers and unique product categories  

### 3️⃣ Business Analysis (Key Queries)
1. Retrieve all sales on **2022-11-05**  
2. Retrieve transactions in **Clothing** category with `quantity > 10` in **Nov 2022**  
3. Calculate **total sales per category**  
4. Find **average age** of customers purchasing **Beauty** items  
5. Retrieve all transactions with `total_sale > 1000`  
6. Find **number of transactions per gender in each category**  
7. Find the **best-selling month** in each year using window functions  
8. Identify **Top 5 customers by highest total purchase**  
9. Find **unique customers per category**  
10. Categorize transactions by **shifts (Morning, Afternoon, Evening)** based on `sale_time`  

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
📍 Pune, India | 📧 artac534@gmail.com | 📞 9270112860  
