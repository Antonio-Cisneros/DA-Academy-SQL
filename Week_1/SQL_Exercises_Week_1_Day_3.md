# Exercises - Week 1 - Day 3

## 1. What products do we sell the most of and how much do we charge for them?

```sql
SELECT DISTINCT P.ProductID, P.ProductName, OD.Quantity, P.Price
FROM products P
	LEFT JOIN order_details OD 
	ON OD.ProductID = P.ProductID
ORDER BY OD.Quantity DESC LIMIT 5;
```

## 2. Which products brings us the most revenue? (Excluding “Alice Mutton” because they are going out of business.)

```sql
SELECT DISTINCT P.ProductID, P.ProductName, SUM(OD.Quantity * P.Price) Revenue
FROM products P
	JOIN order_details OD 
	ON OD.ProductID = P.ProductID
WHERE P.ProductName != "Alice Mutton"
GROUP BY P.ProductID, P.ProductName
ORDER BY Revenue DESC LIMIT 5;
```

## 3. What is our Annual Total Revenue?

```sql
SELECT EXTRACT(YEAR FROM O.OrderDate) AS "Year", SUM(OD.Quantity * P.Price) AS "Total Revenue"
FROM orders O
	JOIN order_details OD 
	ON OD.OrderID = O.OrderID
	JOIN products P 
	ON P.ProductID = OD.ProductID
GROUP BY EXTRACT(YEAR FROM O.OrderDate);
```

## 4. Who is the shipper that delivers most of our customers' orders?

```sql
SELECT S.ShipperID, S.ShipperName
FROM shippers S
	JOIN orders O
	ON O.ShipperID = S.ShipperID
GROUP BY S.ShipperID, S.ShipperName
ORDER BY COUNT(*);
```

## 5. Do we have customers that only request orders for one category of products?

```sql
SELECT DISTINCT C.CustomerID, C.CustomerName, O.OrderID, P.CategoryID,
	CASE P.CategoryID
		WHEN 1 THEN "Beverages"
		WHEN 2 THEN "Condiments"
		WHEN 3 THEN "Confections"
		WHEN 4 THEN "Dairy Products"
		WHEN 5 THEN "Grains/Cereals"
		WHEN 6 THEN "Meat/Poultry"
		WHEN 7 THEN "Produce"
		WHEN 8 THEN "Seafodd"
		ELSE "Unknown category"
	END AS "Category name"
FROM products P
LEFT OUTER JOIN order_details OD ON OD.ProductID = P.ProductID
LEFT OUTER JOIN orders O ON O.OrderID = OD.OrderID
LEFT OUTER JOIN customers C ON C.CustomerID = C.CustomerID
ORDER BY COUNT(*);
```
