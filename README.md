# 🧮 Customer Profiling & Segmentation (SQL Project)

This project focuses on analyzing customer and transaction data using **SQL** to uncover meaningful business insights such as customer segmentation, spending behavior, recency of transactions, and customer value. It's built as part of my **GeeksforGeeks Data Science Training Program**.

---

## 📌 Objectives

- Segment customers by **age group** (Young, Middle-aged, Senior)
- Identify **high-value** and **inactive** customers
- Analyze **product category trends**
- Perform basic **RFM analysis** (Recency, Frequency, Monetary)
- Export findings for business use

---

## 🗂️ Database Schema

### `customers` Table
| Column        | Type         | Description                |
|---------------|--------------|----------------------------|
| Customer_id   | INT (PK)     | Unique ID for each customer |
| FirstName     | VARCHAR(50)  | First name                 |
| LastName      | VARCHAR(50)  | Last name                  |
| Email         | VARCHAR(50)  | Email address              |
| Gender        | VARCHAR(10)  | Gender                     |
| Age           | INT          | Age of customer            |
| City          | VARCHAR(50)  | City                       |
| State         | VARCHAR(50)  | State                      |

### `transactions` Table
| Column          | Type          | Description                      |
|------------------|---------------|----------------------------------|
| Transaction_id   | INT (PK)      | Unique ID for each transaction  |
| Customer_id      | INT (FK)      | Links to `customers` table       |
| TransactionDate  | DATE          | Date of transaction              |
| Amount           | DECIMAL(10,2) | Amount spent                     |
| Product          | VARCHAR(100)  | Product purchased                |
| Category         | VARCHAR(50)   | Product category                 |

---

## 📊 Key SQL Queries

### 1. Age-Based Customer Segmentation
```sql
SELECT 
    CASE 
        WHEN Age < 25 THEN 'Young'
        WHEN Age BETWEEN 25 AND 40 THEN 'Middle-aged'
        ELSE 'Senior'
    END AS AgeSegment,
    COUNT(*) AS CustomerCount
FROM customers
GROUP BY AgeSegment;
```
### 2.High-Value Customers (Monetary)
```sql
SELECT c.Customer_id, c.FirstName, SUM(t.Amount) AS TotalSpent
FROM customers c
JOIN transactions t ON c.Customer_id = t.Customer_id
GROUP BY c.Customer_id
HAVING TotalSpent > 500;
```
### 3.Inactive Customers
```sql
SELECT c.*
FROM customers c
LEFT JOIN transactions t ON c.Customer_id = t.Customer_id
WHERE t.Transaction_id IS NULL;
```
### 4. Recency (Last Transaction Date)
```sql
SELECT c.Customer_id, MAX(t.TransactionDate) AS LastPurchaseDate
FROM customers c
JOIN transactions t ON c.Customer_id = t.Customer_id
GROUP BY c.Customer_id;

```
### 5. Category-Wise Purchase Behavior
```sql
SELECT c.Customer_id, c.FirstName, t.Category, COUNT(*) AS Purchases
FROM customers c
JOIN transactions t ON c.Customer_id = t.Customer_id
GROUP BY c.Customer_id, t.Category
ORDER BY Purchases DESC;

```
---
## 🧠 Learnings

- Practiced SQL joins, GROUP BY, HAVING, and CASE statements
- Built real-world logic for customer segmentation
- Understood the business value of profiling and behavioral targeting
- Exported reports for potential dashboard use
---
## 🛠 Tech Used

- MySQL 8.0
- MySQL Workbench
- CSV Exports
- Google Sheets / Excel (for viewing results)

---
## 🔗 Author

- Naresh Tallapaka
- 📧 naresh.tallapaka@protonmail.com
- 🌐 LinkedIn
- 🌐 GitHub Portfolio
---
## ✅ Status

- ✅ Completed and available as a course project
- 📂 Can be extended with Python dashboard or Power BI
---