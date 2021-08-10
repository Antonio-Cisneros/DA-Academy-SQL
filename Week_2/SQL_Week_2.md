# SQL - Week 2

## Queries done during week 2

```sql
SELECT CONCAT(ST.firstName,' ',ST.lastName) AS 'Student name', G.CLASS_NAME, G.GRADE FROM students ST
JOIN grades G ON G.STUDENT_ID = ST.studentId
ORDER BY G.GRADE DESC;
```

```sql
SELECT CONCAT(ST.firstName,' ',ST.lastName) AS 'Student name', G.CLASS_NAME, G.GRADE FROM students ST
LEFT JOIN grades G ON ST.studentId = G.STUDENT_ID ORDER BY ST.studentId;
```

```sql
SELECT CONCAT(ST.firstName,' ',ST.lastName) AS 'Student name', ST.age,
    CASE
        WHEN ST.age BETWEEN 0 AND 21 THEN "Gen Z"
        WHEN ST.age BETWEEN 22 AND 25 THEN "Millenial"
        WHEN ST.age >= 26 THEN "Baby Boomer"
        ELSE "Unknown"
    END AS "Generation"
FROM students ST
```

```sql
SELECT CONCAT(ST.firstName,' ',ST.lastName) AS 'Student name', G.GRADE
FROM students ST
LEFT JOIN grades G ON ST.studentId = G.STUDENT_ID
WHERE G.GRADE IS NULL;
```

```sql
SELECT CONCAT(A.firstName,' ',A.lastName) AS 'Student name', CONCAT(B.firstName,' ',B.lastName) AS 'People Lead name'
FROM students A 
INNER JOIN students B ON A.peopleLeadID = B.studentId
ORDER BY A.peopleLeadID DESC;
```

```sql
SELECT ST.state, COUNT(*) AS "Number of Students" FROM students ST GROUP BY ST.state;
```

```sql
SELECT ST.state, COUNT(*) AS "Number of Students"
FROM students ST
GROUP BY ST.state
HAVING COUNT(*) > 1;
```

```sql
SELECT * FROM categories WHERE CategoryName NOT IN ('Beverages', 'Dairy Products');
```

```sql
SELECT * FROM categories WHERE CategoryName IN ('Beverages', 'Dairy Products');
```

```sql
SELECT *, ROW_NUMBER() OVER (PARTITION BY Quantity ORDER BY OrderID DESC ) AS 'Row number',
RANK() OVER (PARTITION BY Quantity ORDER BY OrderID DESC ) AS 'Rank',
DENSE_RANK() OVER (PARTITION BY Quantity ORDER BY OrderID DESC) AS 'DENSE_RANK'
FROM order_details WHERE Quantity = 4;
```

```sql
SELECT Quantity, OrderID, RANK() OVER (PARTITION BY Quantity ORDER BY OrderID DESC ) AS "Rank"
FROM order_details WHERE Quantity = 4;
```

```sql
SELECT *,
ROW_NUMBER() OVER (PARTITION BY Quantity, OrderID) AS rowNumber
FROM order_details;
```

```sql
SELECT *,
RANK() OVER (PARTITION BY Quantity, productID ORDER BY OrderID) AS rowNumber
FROM order_details;
```

```sql
SELECT C.CustomerName, OD.OrderDetailID, OD.Quantity,
ROW_NUMBER() OVER (ORDER BY O.OrderID) AS "Row number",
RANK() OVER (ORDER BY O.OrderID) AS "Row rank",
DENSE_RANK() OVER (ORDER BY O.OrderID) AS "Row dense rank"
FROM customers C
JOIN orders O ON O.CustomerID = C.CustomerID
JOIN order_details OD ON OD.OrderID = O.OrderID
HAVING OD.Quantity > 60
```

```sql
SELECT DISTINCT O.OrderID, O.CustomerID, O.OrderDate, CONCAT(E.FirstName," ", E.LastName) AS "Name",
ROW_NUMBER() OVER (ORDER BY O.OrderID) AS "Row number",
RANK() OVER (ORDER BY O.OrderID) AS "Row rank",
DENSE_RANK() OVER (ORDER BY O.OrderID) AS "Row dense rank"
FROM orders O
JOIN employees E ON O.EmployeeID = E.EmployeeID
WHERE O.OrderDate BETWEEN '1996-09-02' AND '1996-09-30'
ORDER BY O.OrderID;
```
