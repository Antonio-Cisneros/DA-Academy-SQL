# SQL - Exercises - Subqueries

## 1. Write a query to find the name (first_name, last_name) and the salary of the employees who have a higher salary than the employee whose last_name='Bull'.


```sql
SELECT CONCAT(FIRST_NAME, " ",LAST_NAME) AS "Name", SALARY
FROM employees
WHERE SALARY > (SELECT SALARY FROM employees WHERE LAST_NAME = "Bull");
```

## 2. Write a query to find the name (first_name, last_name) of all employees who works in the IT department.

```sql
SELECT CONCAT(FIRST_NAME, " ", LAST_NAME) AS "Name", DEPARTMENT_ID
FROM employees
WHERE DEPARTMENT_ID IN (SELECT DEPARTMENT_ID FROM departments WHERE DEPARTMENT_NAME = "IT");
```

## 3. Write a query to find the name (first_name, last_name) of the employees who are managers.

```sql
SELECT CONCAT(FIRST_NAME, " ", LAST_NAME) AS "Name"
FROM employees
WHERE EMPLOYEE_ID IN (SELECT MANAGER_ID FROM employees);
```

## 4. Write a query to find the name (first_name, last_name), and salary of the employees whose salary is greater than the average salary.

```sql
SELECT CONCAT(FIRST_NAME, " ", LAST_NAME) AS "Name", SALARY
FROM employees
WHERE SALARY > (SELECT AVG(SALARY) FROM employees);
```

## 5. Write a query to find the name (first_name, last_name), and salary of the employees who earns more than the average salary and works in any of the IT departments.

```sql
SELECT CONCAT(FIRST_NAME, " ", LAST_NAME) AS "Name", SALARY
FROM employees
WHERE SALARY > (SELECT AVG(SALARY) FROM employees)
AND DEPARTMENT_ID IN (SELECT DEPARTMENT_ID FROM departments WHERE DEPARTMENT_NAME LIKE "IT");
```

## 6. Write a query to find the name (first_name, last_name), and salary of the employees who earns more than the earning of Mr. Bell.

```sql
SELECT CONCAT(FIRST_NAME, " ", LAST_NAME) AS "Name", SALARY
FROM employees
WHERE SALARY > (SELECT SALARY FROM employees WHERE LAST_NAME LIKE "Bell")
```

## 7. Write a query to find the name (first_name, last_name), and salary of the employees who earn the same salary as the minimum salary for all departments.

```sql
SELECT CONCAT(FIRST_NAME, " ", LAST_NAME) AS "Name", SALARY
FROM employees
WHERE SALARY > (SELECT MIN(SALARY) FROM employees);
```

## 8. Write a query to find the name (first_name, last_name), and salary of the employees whose salary is greater than the average salary of all departments.

```sql
SELECT CONCAT(FIRST_NAME, " ", LAST_NAME) AS "Name", SALARY
FROM employees
WHERE SALARY > ALL
	(SELECT AVG(SALARY) FROM employees GROUP BY DEPARTMENT_ID);
```

## 9. Write a query to find the name (first_name, last_name) and salary of the employees who earn a salary that is higher than the salary of all the Shipping Clerk (JOB_ID = 'SH_CLERK'). Sort the results of the salary of the lowest to highest.

```sql
SELECT JOB_ID, CONCAT(FIRST_NAME, " ", LAST_NAME) AS "Name", SALARY
FROM employees
WHERE SALARY > ALL
	(SELECT SALARY FROM employees WHERE JOB_ID LIKE 'SH_CLERK')
ORDER BY SALARY;
```
	
## 10. Write a query to find the name (first_name, last_name) of the employees who are not supervisors. Supervisors = Managers

```sql
SELECT CONCAT(FIRST_NAME, " ", LAST_NAME) AS "Name", MANAGER_ID
FROM employees
WHERE EMPLOYEE_ID NOT IN (SELECT DISTINCT MANAGER_ID FROM employees);
```

## 11. Write a query to select last 10 records from employee table based on the employee id ORDER.


```sql
SELECT * FROM (SELECT * FROM employees ORDER BY EMPLOYEE_ID DESC LIMIT 10) AS E
ORDER BY E.EMPLOYEE_ID;
```

## 12. Write a query to list the department ID and name of all the departments where no employee is working.

```sql
SELECT DEPARTMENT_ID, DEPARTMENT_NAME FROM departments
WHERE DEPARTMENT_ID NOT IN (SELECT DEPARTMENT_ID FROM employees);
```
