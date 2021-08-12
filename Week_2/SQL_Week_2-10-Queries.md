# 10 SQL Queries


## Query #1
```sql
SELECT DISTINCT O.OrderID, OD.ProductID, P.Unit, P.Price, SUM(OD.Quantity + P.Price) AS Revenue, 
	P.CategoryID,
	CASE P.CategoryID
			WHEN 1 THEN "Beverages"
			WHEN 2 THEN "Condiments"
			WHEN 3 THEN "Confections"
			WHEN 4 THEN "Diary Products"
			WHEN 5 THEN "Grains/Cereals"
			WHEN 6 THEN "Meat/Poultry"
			WHEN 7 THEN "Produce"
			WHEN 8 THEN "Seafood"
			ELSE "Unknown category"
	END AS "Category Name"
FROM orders O
	LEFT JOIN order_details OD
	ON OD.OrderID = O.OrderID
	LEFT JOIN products P
	ON P.ProductID = OD.ProductID
GROUP BY P.CategoryID
HAVING SUM(OD.Quantity + P.Price) > 2000;
```

## Query #2

```sql
SELECT P.ProductID, P.ProductName,
ROW_NUMBER() OVER (PARTITION BY Quantity ORDER BY OrderID DESC ) AS 'Row number'
FROM products P
	JOIN order_details OD 
	ON OD.ProductID = P.ProductID LIMIT 5;
```

## Query #3

```sql
SELECT O.OrderID, P.ProductName, P.CategoryID, C.CategoryName, O.OrderDate
FROM orders O
	LEFT OUTER JOIN order_details OD
	ON OD.OrderID = O.OrderID
	LEFT OUTER JOIN products P
	ON P.ProductID = OD.ProductID
	LEFT OUTER JOIN categories C
	ON C.CategoryID = P.CategoryID
WHERE OrderDate BETWEEN '1996-08-01' AND '1996-12-31'
AND P.CategoryID NOT IN (1,3,5,7);
```

## Query #4

```sql
SELECT P.ProductID, P.ProductName, S.SupplierName
FROM products P
	RIGHT JOIN suppliers S
	ON P.SupplierID = S.SupplierID
WHERE S.Country = "Germany";
```

## Query #5

```sql
SELECT SH.ShipperName, COUNT(O.OrderID) AS "Orders on 1997"
FROM orders O
	JOIN shippers SH
	ON SH.ShipperID = O.ShipperID
WHERE O.OrderDate > "1996-12-31"
GROUP BY SH.ShipperName DESC;
```

## Query #6

```sql
SELECT P.ProductName, OD.OrderDetailID
FROM order_details OD
	JOIN products P
	ON P.ProductID = OD.OrderDetailID
WHERE OD.OrderID = 10248;
```

## Query #7

```sql
SELECT OrderID, COUNT(*) AS "Count of orders"
FROM order_details
GROUP BY OrderID 
HAVING COUNT(*) = 1;
```

## Query #8

```sql
SELECT DISTINCT OD.OrderID, P.ProductName, 
RANK() OVER (PARTITION BY P.ProductID ORDER BY OD.OrderID) AS rowNumber
FROM order_details OD, products P
WHERE OD.ProductID = P.ProductID;
```

## Query #9

```sql
SELECT COUNT(CustomerID), Country
FROM customers
WHERE ContactName LIKE "An%"
GROUP BY Country;
```

## Query #10

```sql
SELECT P.ProductID, P.ProductName, C.CategoryName, P.Price
FROM products P, categories C
WHERE C.CategoryID = 1 AND P.Price BETWEEN 1 AND 10;
```
