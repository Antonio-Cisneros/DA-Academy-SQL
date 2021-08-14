# SQL - Exercises - Week 3 - Day 4

## 1. Write a query to find the addresses (location_id, street_address, city, state_province, country_name) of all the departments.

```sql
SELECT L.LOCATION_ID, L.STREET_ADDRESS, L.CITY, L.STATE_PROVINCE, C.COUNTRY_NAME
FROM locations L
	JOIN countries C
	ON L.COUNTRY_ID = L.COUNTRY_ID;
```

## 2. Write a query to find the name (first_name, last name), department ID and name of all the employees.

```sql
SELECT D.DEPARTMENT_ID, D.DEPARTMENT_NAME, CONCAT(E.FIRST_NAME," ",E.LAST_NAME) AS "Name"
FROM employees E
	JOIN departments D
	ON E.DEPARTMENT_ID = D.DEPARTMENT_ID;
```

## 3. Write a query to find the name (first_name, last_name), job, department ID and name of the employees who works in London.

```sql
SELECT CONCAT(E.FIRST_NAME," ",E.LAST_NAME) AS "Name", E.JOB_ID, D.DEPARTMENT_ID, D.DEPARTMENT_NAME 
FROM employees E
	JOIN departments D
	ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
	JOIN locations L
	ON D.LOCATION_ID = L.LOCATION_ID
WHERE L.CITY = "London";
```

## 4. Write a query to find the employee id, name (last_name) along with their manager_id and name (last_name).

```sql
SELECT E.EMPLOYEE_ID, CONCAT(E.FIRST_NAME,' ', E.LAST_NAME) AS "Employee Name",
	CONCAT(E2.FIRST_NAME,' ', E2.LAST_NAME) AS "Manager Name"
FROM employees E
	JOIN employees E2
	ON E.MANAGER_ID = E2.EMPLOYEE_ID;
```

## 5. Write a query to find the name (first_name, last_name) and hire date of the employees who was hired after 'Jones'.

```sql
SELECT E.EMPLOYEE_ID, CONCAT(E.FIRST_NAME,' ', E.LAST_NAME) AS "Employee Name", E.HIRE_DATE AS "Hire date"
FROM employees E
	JOIN employees J
	ON J.LAST_NAME = "Jones"
WHERE J.HIRE_DATE < E.HIRE_DATE;
```

## 6. Write a query to get the department name and number of employees in the department.

```sql
SELECT D.DEPARTMENT_ID, D.DEPARTMENT_NAME, COUNT(*) AS "Number of employees"
FROM employees E
	JOIN departments D
	ON E.DEPARTMENT_ID = D.DEPARTMENT_ID
GROUP BY D.DEPARTMENT_ID, D.DEPARTMENT_NAME;
```

## 7. Write a query to find the employee ID, job title, number of days between ending date and starting date for all jobs in department 90.

```sql
SELECT JH.EMPLOYEE_ID, J.JOB_TITLE, JH.END_DATE - JH.START_DATE AS "Number of days"
FROM jobs J
	JOIN job_history JH
	ON J.JOB_ID = JH.JOB_ID
WHERE JH.DEPARTMENT_ID LIKE (90);
```

## 8. Write a query to display the department ID and name and first name of manager.

```sql
SELECT D.DEPARTMENT_ID, D.DEPARTMENT_NAME, E.FIRST_NAME AS "Manager's name"
FROM departments D
	JOIN employees E
	ON D.MANAGER_ID = E.EMPLOYEE_ID;
```

## 9. Write a query to display the department name, manager name, and city.

```sql
SELECT D.DEPARTMENT_NAME, E.FIRST_NAME AS "Manager's name", L.CITY 
FROM employees E
	JOIN departments D
	ON E.EMPLOYEE_ID = D.MANAGER_ID
	JOIN locations L
	ON D.LOCATION_ID = L.LOCATION_ID;
```
	
## 10. Write a query to display the job title and average salary of employees.

```sql
SELECT J.JOB_TITLE, ROUND(AVG(E.SALARY)) "Average saLary"
FROM jobs J
	JOIN employees E
	ON J.JOB_ID = E.JOB_ID
GROUP BY J.JOB_TITLE;
```

## 11. Write a query to display job title, employee name, and the difference between salary of the employee and minimum salary for the job.

```sql
SELECT J.JOB_TITLE, CONCAT(E.FIRST_NAME,' ', E.LAST_NAME) AS "Employee Name", (E.SALARY - J.MIN_SALARY) AS "Salary difference" 
FROM jobs J
	JOIN employees E
	ON J.JOB_ID = E.JOB_ID
```

## 12. Write a query to display the job history that were done by any employee who is currently drawing more than 10000 of salary.

```sql
SELECT E.EMPLOYEE_ID, CONCAT(E.FIRST_NAME,' ', E.LAST_NAME) AS "Employee Name", JH.START_DATE, JH.END_DATE, JH.DEPARTMENT_ID,
		E.SALARY
FROM job_history JH
	JOIN employees e
	ON JH.EMPLOYEE_ID = E.EMPLOYEE_ID
WHERE E.SALARY > 1000;
```

## 13. Write a query to display department name, name (first_name, last_name), hire date, salary of the manager for all managers whose experience is more than 15 years.

/*
SELECT D.DEPARTMENT_NAME, CONCAT(E.FIRST_NAME,' ', E.LAST_NAME) AS "Employee Name", E.HIRE_DATE, E.SALARY, CURDATE()
FROM employees E
	JOIN departments D
	ON E.EMPLOYEE_ID = D.MANAGER_ID
*/

```sql
SELECT D.DEPARTMENT_NAME, CONCAT(E.FIRST_NAME,' ', E.LAST_NAME) AS "Employee Name", E.HIRE_DATE, E.SALARY,
	DATEDIFF(CURDATE(), E.HIRE_DATE)/365 AS "Experience"
FROM employees E
	JOIN departments D
	ON E.EMPLOYEE_ID = D.MANAGER_ID
WHERE DATEDIFF(CURDATE(), E.HIRE_DATE)/365 > 15
ORDER BY D.DEPARTMENT_NAME;
```