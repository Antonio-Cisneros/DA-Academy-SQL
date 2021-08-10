# Exercises - Week 3 - Day 1

## 1. Write a query to display the names (first_name, last_name) using alias name “First Name", "Last Name".

```sql
SELECT FIRST_NAME "First Name", LAST_NAME "Last Name" FROM employees;
```

## 2. Write a query to get unique department ID from employee table.

```sql
SELECT DISTINCT DEPARTMENT_ID FROM employees;
```

## 3. Write a query to get all employee details from the employee table order by first name, descending.

```sql
SELECT * FROM employees ORDER BY FIRST_NAME DESC;
```

## 4. Write a query to get the names (first_name, last_name), salary, PF of all the employees (PF is calculated as 15% of salary).

```sql
SELECT CONCAT(FIRST_NAME," ",LAST_NAME) "Name", SALARY, (SALARY * 0.15) PF FROM employees;
```

## 5. Write a query to get the employee ID, names (first_name, last_name), salary in ascending order of salary.

```sql
SELECT EMPLOYEE_ID, CONCAT(FIRST_NAME," ",LAST_NAME) "Name", SALARY FROM employees ORDER BY SALARY;
```

## 6. Write a query to get the total salaries payable to employees.

```sql
SELECT SUM(SALARY) "Total salary" FROM employees;
```

## 7. Write a query to get the maximum and minimum salary from employees table.

```sql
SELECT MAX(SALARY) "Maximum salary", MIN(SALARY) "Minimum salary" FROM employees;
```

## 8. Write a query to get the average salary and number of employees in the employees table.

```sql
SELECT AVG(SALARY) "Average salary", COUNT(*) "Number of employees" FROM employees;
```

## 9. Write a query to get the number of employees working with the company.

```sql
SELECT COUNT(*) "Number of employees" FROM employees;
```

## 10. Write a query to get the number of jobs available in the employees table.

```sql
SELECT COUNT(JOB_ID) "Number of Available jobs" FROM jobs;
```

## 11. Write a query get all first name from employees table in upper case.

```sql
SELECT UPPER(FIRST_NAME) "First name" FROM employees;
```

## 12. Write a query to get the first 3 characters of first name from employees table.

```sql
SELECT LEFT(FIRST_NAME, 3) "First name" FROM employees;
```

## 13. Write a query to calculate 171*214+625.

```sql
SELECT 171 * 214 + 625 Output;
```

## 14. Write a query to get the names (for example Ellen Abel, Sundar Ande etc.) of all the employees from employees table.

```sql
SELECT CONCAT(FIRST_NAME," ",LAST_NAME) "Name" FROM employees;
```

## 15. Write a query to get first name from employees table after removing white spaces from both side.

```sql
SELECT LTRIM(FIRST_NAME) "First name" FROM employees;
```

## 16. Write a query to get the length of the employee names (first_name, last_name) from employees table.

```sql
SELECT CONCAT(FIRST_NAME," ",LAST_NAME) "Name",
CHAR_LENGTH(FIRST_NAME) + CHAR_LENGTH(LAST_NAME) "Name length" 
FROM employees;
```

## 17. Write a query to check if the first_name fields of the employees table contains numbers.

```sql
SELECT FIRST_NAME FROM employees WHERE FIRST_NAME REGEXP '[0-9]';
```

## 18. Write a query to select first 10 records from a table.

```sql
SELECT * FROM jobs LIMIT 10;
```

## 19. Write a query to get monthly salary (round 2 decimal places) of each and every employee. Note : Assume the salary field provides the 'annual salary' information.

```sql
SELECT CONCAT(FIRST_NAME," ",LAST_NAME) "Name", ROUND(SALARY / 12, 2) "Monthly salary" FROM employees;
```
