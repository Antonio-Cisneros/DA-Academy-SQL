# Exercises - Week 1 - Day 2

## 1. A list of our US suppliers, identifying their phone area code.

```sql
SELECT supplierID, supplierName, Country, SUBSTR(Phone, 2, 3) AS "Phone Area Code"
FROM suppliers WHERE Country = "USA";
```
## 2. What customer(s) have never placed an order?

```sql
SELECT C.CustomerID, C.CustomerName FROM customers C
LEFT JOIN orders O ON O.CustomerID = C.CustomerID
WHERE O.CustomerID IS NULL;
```

## 3. In what countries do we have customers?

```sql
SELECT COUNT(*) AS "Number of customers", Country FROM customers
GROUP BY Country;
```

## 4. What are the 5 most sold products?

```sql
SELECT P.ProductID, P.ProductName, OD.Quantity FROM products P
JOIN order_details OD ON OD.ProductID = P.ProductID
ORDER BY OD.Quantity DESC LIMIT 5;
```

## 5. What product(s) should our client stop offering?

```sql
SELECT P.ProductID, P.ProductName, SUM(OD.Quantity * P.Price) AS Products_sold FROM products P
LEFT JOIN order_details OD ON P.ProductID = OD.ProductID
GROUP BY P.ProductID
#HAVING Products_sold IS NULL
ORDER BY Products_sold LIMIT 5;
```

## Bonus Questions:

A) Describe how could you assign a manager to an employee, hence creating a hierarchical organization of records in the [Employees] table.
(Clue: you're allowed to modify the [Employees] attributes)

```sql
SELECT E.EmployeeID, CONCAT(E.FirstName,' ', E.LastName) AS "Employee Name",
CONCAT(.FirstName,' ', M.LastName) AS "Manager Name"
FROM employees E
JOIN Employees E2 ON E2.ManagerID = E.ManagerID;
```

B) Describe a possible valid business scenario where you would have a need to extract information by cross-joining tables in our case study.

Write a query to get the detail of orders including the supplier name and product characteristics, order by the supplier's country.


```sql
SELECT DISTINCT OD.OrderDetailID, OD.OrderID, S.SupplierName, P.ProductName, P.Price, OD.Quantity
FROM suppliers S
CROSS JOIN products P ON P.SupplierID = S.SupplierID
CROSS JOIN order_details OD ON OD.ProductID = P.ProductID
ORDER BY S.Country;
```