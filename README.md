Advanced SQL Function Combinations
This repository explores advanced techniques for combining SQL functions to enhance data manipulation capabilities. Each section includes explanations and practical examples to demonstrate the power of these combinations.

Table of Contents
1. Subqueries and Correlated Subqueries
2. Common Table Expressions (CTEs) and Recursive Queries
3. Window Functions
4. Set Operations
5. Combining String Functions
1. Subqueries and Correlated Subqueries
Subqueries are queries nested within another query. A correlated subquery depends on the outer query for its values.

Example: Retrieve employees earning above the average salary in their department

sql
Copy
Edit
SELECT employee_id, name, salary
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE department_id = e.department_id
);
2. Common Table Expressions (CTEs) and Recursive Queries
CTEs provide a way to define temporary result sets. Recursive CTEs are useful for hierarchical data.

Example: Generate an organizational chart

sql
Copy
Edit
WITH RECURSIVE OrgChart AS (
    SELECT employee_id, name, manager_id, 1 AS level
    FROM employees
    WHERE manager_id IS NULL
    UNION ALL
    SELECT e.employee_id, e.name, e.manager_id, oc.level + 1
    FROM employees e
    INNER JOIN OrgChart oc ON e.manager_id = oc.employee_id
)
SELECT * FROM OrgChart;
3. Window Functions
Window functions perform calculations across a set of table rows related to the current row.

Example: Calculate a running total of sales

sql
Copy
Edit
SELECT order_id, order_date, amount,
       SUM(amount) OVER (ORDER BY order_date) AS running_total
FROM sales;
4. Set Operations
Set operations combine results from multiple queries.

Example: Find customers who made purchases in both 2022 and 2023

sql
Copy
Edit
SELECT customer_id
FROM sales
WHERE YEAR(order_date) = 2022
INTERSECT
SELECT customer_id
FROM sales
WHERE YEAR(order_date) = 2023;
5. Combining String Functions
String functions can be combined to manipulate text data.

Example: Standardize phone numbers

sql
Copy
Edit
SELECT phone_number,
       CONCAT('(', SUBSTRING(phone_number, 1, 3), ') ',
              SUBSTRING(phone_number, 4, 3), '-',
              SUBSTRING(phone_number, 7, 4)) AS formatted_phone
FROM contacts;
These techniques, when combined thoughtfully, can lead to powerful data manipulation capabilities in SQL.
