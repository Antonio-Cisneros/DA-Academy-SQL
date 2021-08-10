# Exercises - Week 1 - Day 1

## 1. An alphabetical list of customers located in Mexico

```sql
SELECT * FROM customers WHERE Country = "Mexico" ORDER BY CustomerName;
```

## 2. A list of employees from youngest to oldest

```sql
SELECT * FROM employees ORDER BY BirthDate DESC;
```

## 3. A list of orders that included “Dairy Products” and “Grains/Cereals”

```sql
SELECT O.OrderID, OD.OrderDetailID, P.CategoryID,
		CASE P.CategoryID
			WHEN 4 THEN "Dairy Products"
			WHEN 5 THEN "Grains/Cereals"
			ELSE "No category"
		END AS "Category name" 
FROM orders O
JOIN order_details OD ON OD.OrderID = O.OrderID
JOIN products P ON P.ProductID = OD.ProductID
WHERE P.CategoryID = 4 OR P.CategoryID = 5;
```

## 4. What products are supplied by “G'day, Mate”?

```sql
SELECT P.ProductID, P.ProductName
FROM products P
LEFT JOIN suppliers S ON P.SupplierID = S.SupplierID
WHERE S.SupplierName = "G'day, Mate"
```

## 5. What shippers have delivered our orders per country?

```sql
SELECT DISTINCT O.OrderID, O.ShipperID, S.ShipperName, C.Country
FROM orders O
JOIN customers C ON C.CustomerID = O.CustomerID
JOIN shippers S ON S.ShipperID = O.ShipperID
ORDER BY C.Country;
```

## 6. The list of orders managed by Nancy Davolio during 1997

```sql
SELECT O.OrderID, O.CustomerID FROM orders O
LEFT OUTER JOIN employees E ON O.EmployeeID = E.EmployeeID
WHERE E.FirstName = "Nancy" AND O.OrderDate >= "1997-01-01";
```
