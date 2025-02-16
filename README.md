# Assessment-Task
(1) Explore this dataset and highlight key insights in terms of aggregate and drill down of this sales data.
Aggregate Analysis:
---------------------
Aggregate Sales Overview
1.Total Sales,
2.Average Transaction Value,
3.Total Transactions
4.Product wise sales and returns
5.City wise sales and returns
6.Promotional and non promotional sales
7.Top 5 Best-Selling Products

Drill-Down Analysis of Sales Data
---------------------------------
1.Customer Demographics & Behavior
  Age-wise Spending:
  18-30 years
  31-50 years
  51+ years

  Gender-wise Sales:
  Male Customers
  Female Customers
  Other Gender

2.Store Type Performance
   Online Sales
   In-Store Sales

3.City-wise Performance
  Highest Sales
  Highest Returns
  Fastest Deliveries
  Slowest Deliveries

4.Product-Specific Trends
  Electronics (Laptops, Sofas)
  Clothing (T-Shirts)
  Stationery (Notebooks, Apple)



  (2)Share SQL scripts used to explore data and generate metrics & Key insights in bullet points
1.Total Sales,Average Transaction Value,Total Transactions :
-----------------------------------------------------------
SELECT 
    SUM(TransactionAmount) AS TotalSales, 
    COUNT(TransactionID) AS TotalTransactions, 
    AVG(TransactionAmount) AS AvgTransactionValue
FROM sales_data;

4.Product wise sales and returns
---------------------------------
SELECT 
    ProductName, 
    SUM(TransactionAmount) AS TotalSales, 
    COUNT(TransactionID) AS TotalTransactions, 
    SUM(CASE WHEN Returned = 'Yes' THEN 1 ELSE 0 END) AS TotalReturns,
    (SUM(CASE WHEN Returned = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(TransactionID)) AS ReturnRate
FROM sales_data
GROUP BY ProductName
ORDER BY TotalSales DESC;

5.City wise sales and returns
------------------------------
SELECT 
    City, 
    SUM(TransactionAmount) AS TotalSales, 
    COUNT(TransactionID) AS TotalTransactions, 
    SUM(CASE WHEN Returned = 'Yes' THEN 1 ELSE 0 END) AS TotalReturns,
    (SUM(CASE WHEN Returned = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(TransactionID)) AS ReturnRate
FROM sales_data
GROUP BY City
ORDER BY TotalSales DESC;

6.Promotional and non promotional sales
-----------------------------------------
SELECT 
    IsPromotional, 
    SUM(TransactionAmount) AS TotalSales, 
    COUNT(TransactionID) AS Transactions
FROM sales_data
GROUP BY IsPromotional;

7.Top 5 Best-Selling Products
------------------------------
SELECT 
    ProductName, 
    SUM(TransactionAmount) AS TotalSales, 
    COUNT(TransactionID) AS Transactions
FROM sales_data
GROUP BY ProductName
ORDER BY TotalSales DESC
LIMIT 5;






