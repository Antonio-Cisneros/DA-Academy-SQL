# SQL - Exercises - Week 3 - Day 2

## 1. Write a query to display the name (first_name, last_name) and salary for all employees whose salary is not in the range $10,000 through $15,000.

```sql
SELECT CONCAT(FIRST_NAME," ",LAST_NAME) AS "Name", SALARY
FROM employees
WHERE SALARY NOT BETWEEN 10000 AND 15000;
```

## 2. Write a query to display the name (first_name, last_name) and department ID of all employees in departments 30 or 100 in ascending order.

```sql
SELECT CONCAT(FIRST_NAME," ",LAST_NAME) AS "Name", DEPARTMENT_ID
FROM employees
WHERE DEPARTMENT_ID IN (30,100)
ORDER BY DEPARTMENT_ID;
```

## 3. Write a query to display the name (first_name, last_name) and salary for all employees whose salary is not in the range $10,000 through $15,000 and are in department 30 or 100.

```sql
SELECT CONCAT(FIRST_NAME," ",LAST_NAME) AS "Name", DEPARTMENT_ID, SALARY
FROM employees
WHERE SALARY NOT BETWEEN 10000 AND 15000
AND DEPARTMENT_ID IN (30,100);
```

## 4. Write a query to display the name (first_name, last_name) and hire date for all employees who were hired in 1987.
Hint: Google the usage of the SQL function YEAR().

```sql
SELECT CONCAT(FIRST_NAME," ",LAST_NAME) AS "Name", HIRE_DATE AS "Hire date"
FROM employees
WHERE EXTRACT(YEAR FROM HIRE_DATE) = "1987";
```

## 5. Write a query to display the first_name of all employees who have both "b" and "c" in their first name.

```sql
SELECT CONCAT(FIRST_NAME," ",LAST_NAME) AS "Name"
FROM employees
WHERE FIRST_NAME LIKE "%b%" 
AND FIRST_NAME LIKE "%c%";
```

## 6. Write a query to display the last name, job, and salary for all employees whose job is that of a Programmer or a Shipping Clerk, and whose salary is not equal to $4,500, $10,000, or $15,000.

```sql
SELECT E.LAST_NAME, J.JOB_TITLE, E.SALARY
FROM employees E
	JOIN jobs J 
	ON E.JOB_ID = J.JOB_ID
WHERE J.JOB_TITLE IN ("Programmer", "Shipping Clerk") 
AND E.SALARY NOT IN (4500.00, 10000.00, 15000.00);
```

## 7. Write a query to display the last name of employees whose names have exactly 6 characters.
Hint: Google the usage of the SQL function CHARACTER_LENGTH().

```sql
SELECT LAST_NAME, CHAR_LENGTH(FIRST_NAME) + CHAR_LENGTH(LAST_NAME) AS "Name length"
FROM employees
WHERE CHAR_LENGTH(FIRST_NAME) + CHAR_LENGTH(LAST_NAME) = 6;
```

## 8. Write a query to display the last name of employees having 'e' as the third character.

```sql
SELECT LAST_NAME
FROM employees
WHERE LAST_NAME LIKE "__e%";
```

## 9. Write a query to display the jobs/designations available in the employees table.

```sql
SELECT JOB_ID AS "Available jobs"
FROM jobs;
```

## 10. Write a query to display the name (first_name, last_name), salary and PF (calculate as 15% of salary) of all employees.

```sql
SELECT CONCAT(FIRST_NAME," ",LAST_NAME) AS "Name", SALARY, (SALARY * 0.15) AS PF 
FROM employees;
```

## 11. Write a query to select all record from employees where last name in 'BLAKE', 'SCOTT', 'KING' and 'FORD'

```sql
SELECT * FROM employees WHERE LAST_NAME = 'BLAKE'
OR LAST_NAME = 'SCOTT'
OR LAST_NAME = 'KING' 
OR LAST_NAME = 'FORD';
```
