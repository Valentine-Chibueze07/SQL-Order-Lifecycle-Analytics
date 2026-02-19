# SQL-Order-Lifecycle-Analytics
SQL Order Lifecycle Analytics 

* Overview

This project analyzes the full order lifecycle using SQL Server.

It focuses on tracking order status progression, revenue contribution, cancellation analysis, delivery performance, and agent productivity.

All business logic was implemented using T-SQL in SQL Server.

**Business Objectives**

Monitor order lifecycle (Created → Confirmed → Delivered → Cancelled)

Measure daily order trends

Track delivered GMV by stock point

Evaluate agent delivery performance

Identify cancelled orders and business loss

Automate order creation via stored procedure

 **Technical Skills Demonstrated**

CRUD operations on SalesOrders

INNER JOIN & LEFT JOIN

GROUP BY with date aggregation

DATE functions (GETDATE, CAST, CONVERT)

Conditional aggregation

Stored Procedure creation

Business rule enforcement

Performance aggregation logic

 **Key SQL Highlights**
✔ Latest 30 Orders with Retailer + Agent
SELECT TOP 30
    S.OrderNumber,
    S.OrderDate,
    R.BusinessName,
    A.FullName
FROM SalesOrders S
INNER JOIN Retailers R ON S.RetailerID = R.RetailerID
INNER JOIN Agents A ON S.AgentID = A.AgentID
ORDER BY S.OrderDate DESC;

✔ Daily Order Count (Last 30 Days)
SELECT 
    CAST(OrderDate AS DATE) AS OrderDate,
    COUNT(*) AS DailyOrderCount
FROM SalesOrders
WHERE OrderDate >= DATEADD(DAY, -30, GETDATE())
GROUP BY CAST(OrderDate AS DATE)
ORDER BY OrderDate DESC;

✔ Delivered GMV by StockPoint
SELECT 
    StockPoint,
    SUM(NetAmount) AS DeliveredGMV
FROM SalesOrders
WHERE Status = 'Delivered'
GROUP BY StockPoint;

✔ Stored Procedure – Create Order Header
CREATE PROCEDURE usp_CreateOrderHeader
    @RetailerID INT,
    @AgentID INT,
    @FulfillmentType NVARCHAR(20),
    @StockPoint NVARCHAR(50)
AS
BEGIN
    INSERT INTO SalesOrders (...)
    VALUES (...);

    SELECT SCOPE_IDENTITY() AS NewOrderID;
END;

** Key Insights Generated**

Identified peak sales days

Tracked delivery performance by location

Measured agent contribution efficiency

Quantified cancelled revenue

Built reusable logic for order automation

** Business Impact**

This project simulates:

✔ Order pipeline monitoring
✔ Revenue forecasting
✔ Operational performance tracking
✔ Delivery efficiency analysis
✔ Commercial loss assessment

🛢 Why This Is Powerful for You

This directly connects to:

Oil & Gas distribution orders

Depot-to-retailer supply tracking

Commercial operations analytics

Revenue reconciliation systems

Recruiters will see:

✔ Real transaction-level SQL maturity
✔ Production-style stored procedure logic
✔ Business KPI thinking
