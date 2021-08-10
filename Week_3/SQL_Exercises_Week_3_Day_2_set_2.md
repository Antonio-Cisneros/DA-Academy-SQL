# SQL - Exercises - Week 3 - Day 2 - Second set of exercises

## 1. Write a query to list the number of jobs available in the employees table.

```sql
SELECT COUNT(*) "Number of jobs" FROM jobs;
```

## 2. Write a query to get the total salaries payable to employees.

```sql
SELECT SUM(SALARY) "Total salary" FROM employees;
```

## 3. Write a query to get the minimum salary from employees table.

```sql
SELECT MIN(SALARY) "Minimum salary" FROM employees;
```

## 4. Write a query to get the maximum salary of an employee working as a Programmer.

```sql
SELECT MAX(E.SALARY) "Maximum salary" FROM employees E, jobs J
WHERE J.JOB_TITLE = "Programmer";
```

## 5. Write a query to get the average salary and number of employees working the department 90.

```sql
SELECT AVG(SALARY), COUNT(*) FROM employees
WHERE DEPARTMENT_ID IN (90);
```

## 6. Write a query to get the highest, lowest, sum, and average salary of all employees.

```sql
SELECT MAX(SALARY) "Maximum salary", MIN(SALARY) "Minimum salary",
SUM(SALARY) "Total salary", 
AVG(SALARY) "Average salary" FROM employees;
```

## 7. Write a query to get the number of employees with the same job.

```sql
SELECT COUNT(*) "Numbber of employees", JOB_ID FROM employees GROUP BY JOB_ID;
```

## 8. Write a query to get the difference between the highest and lowest salaries.

```sql
SELECT MAX(SALARY) - MIN(SALARY) "Salary difference" FROM employees;
```

## 9. Write a query to find the manager ID and the salary of the lowest-paid employee for that manager.

```sql
SELECT MANAGER_ID, MIN(SALARY) FROM employees
GROUP BY MANAGER_ID ORDER BY MIN(SALARY) DESC;
```

## 10. Write a query to get the department ID and the total salary payable in each department.

```sql
SELECT DEPARTMENT_ID, SUM(SALARY) "Total salary" FROM employees GROUP BY DEPARTMENT_ID
ORDER BY SUM(SALARY);
```

## 11. Write a query to get the average salary for each job ID excluding programmer.

```sql
SELECT AVG(SALARY) "Average salary", JOB_ID FROM employees WHERE JOB_ID NOT IN ("Programmer")
GROUP BY JOB_ID ORDER BY JOB_ID;

```

## 12. Write a query to get the total salary, maximum, minimum, average salary of employees (job ID wise), for department ID 90 only.

```sql
SELECT JOB_ID, SUM(SALARY) "Total salary", MAX(SALARY) "Maximum salary", MIN(SALARY) "Minimum salary",
AVG(SALARY) "Average salary"
FROM employees
WHERE DEPARTMENT_ID IN (90)
GROUP BY JOB_ID;
```

## 13. Write a query to get the job ID and maximum salary of the employees where maximum salary is greater than or equal to $4000.

```sql
SELECT JOB_ID, MAX(SALARY) "Maximum salary" FROM employees
GROUP BY JOB_ID HAVING MAX(SALARY) >= 4000 ORDER BY MAX(SALARY);
```

## 14. Write a query to get the average salary for all departments employing more than 10 employees.

```sql
SELECT DEPARTMENT_ID, AVG(SALARY) "Average salary" FROM employees
GROUP BY DEPARTMENT_ID HAVING COUNT(*) > 10;
```
