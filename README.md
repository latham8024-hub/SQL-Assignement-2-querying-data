# SQL-Assignement-2-querying-data
SQL

MySQL queries for dataset
1. Distinct Values
SELECT DISTINCT salary
FROM employees;


2. Alias (AS)
SELECT
    age AS Employee_Age,
    salary AS Employee_Salary
FROM employees;


3. WHERE Clause & Operators
Q3. Salary greater than 50000 and hired before 2016-01-01
SELECT *
FROM employees
WHERE salary > 50000
AND hire_date < '2016-01-01';


Q4. Find missing designation and update it
SELECT *
FROM employees
WHERE designation IS NULL;


UPDATE employees
SET designation = 'Data Scientist'
WHERE designation IS NULL;


4. Sorting and Grouping Data
Q5. ORDER BY
SELECT *
FROM employees
ORDER BY department_id ASC, salary DESC;


Q6. LIMIT – First 5 employees hired in 2018
SELECT *
FROM employees
WHERE YEAR(hire_date) = 2018
ORDER BY hire_date ASC
LIMIT 5;


Q7. SUM – Total salary in Finance department
SELECT SUM(e.salary) AS Total_Salary
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id
WHERE d.department_name = 'Finance';


Q8. Minimum age
SELECT MIN(age) AS Minimum_Age
FROM employees;


Q9. Maximum salary for each location
SELECT
    l.location AS Location,
    MAX(e.salary) AS Maximum_Salary
FROM employees e
INNER JOIN location l
ON e.location_id = l.location_id
GROUP BY l.location_id, l.location;


Q10. Average salary for each designation containing Analyst
SELECT
    designation,
    AVG(salary) AS Average_Salary
FROM employees
WHERE designation LIKE '%Analyst%'
GROUP BY designation;


Q11. Departments with less than 3 employees
SELECT
    d.department_name,
    COUNT(e.employee_id) AS Total_Employees
FROM departments d
LEFT JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name
HAVING COUNT(e.employee_id) < 3;


Q12. Locations with female employees whose average age is below 30
SELECT
    l.location,
    AVG(e.age) AS Average_Age
FROM employees e
INNER JOIN location l
ON e.location_id = l.location_id
WHERE e.gender = 'F'
GROUP BY l.location_id, l.location
HAVING AVG(e.age) < 30;


5. Joins
Q13. INNER JOIN – Employee names, designations and department names
SELECT
    e.employee_name,
    e.designation,
    d.department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id;


Q14. LEFT JOIN – All departments and employee count
SELECT
    d.department_name,
    COUNT(e.employee_id) AS Total_Employees
FROM departments d
LEFT JOIN employees e
ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name;


Q15. RIGHT JOIN – All locations and employee names
SELECT
    l.location,
    e.employee_name
FROM employees e
RIGHT JOIN location l
ON e.location_id = l.location_id;



Important: Check your location table
Your INSERT statement is:
INSERT INTO location (location) VALUES
('Chennai'),
('Bangalore'),
('Hyderabad'),
('Pune');


This assumes location table has an automatically generated location_id column.

 
