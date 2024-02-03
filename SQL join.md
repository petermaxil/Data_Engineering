# 1. INNER JOIN:
An INNER JOIN retrieves records from both tables where there is a match based on the specified condition. It excludes unmatched rows from both tables.

Example:

sql
SELECT employees.emp_id, employees.emp_name, departments.dept_name
FROM employees
INNER JOIN departments ON employees.dept_id = departments.dept_id;
Result:
This query returns records where the dept_id in the "employees" table matches the dept_id in the "departments" table, creating a dataset containing information about employees and their corresponding departments.

# 2. LEFT JOIN (LEFT OUTER JOIN):
A LEFT JOIN retrieves all records from the left table and matching records from the right table. Non-matching right table records contain NULL values.

Example:

sql
SELECT customers.customer_id, orders.order_id
FROM customers
LEFT JOIN orders ON customers.customer_id = orders.customer_id;
Result:
This query includes all customers and, for those with orders, appends the order details. Customers without orders will have NULL values in columns related to orders.

# 3. RIGHT JOIN (RIGHT OUTER JOIN):
A RIGHT JOIN retrieves all records from the right table and matching records from the left table. Non-matching left table records contain NULL values.

Example:

sql
SELECT orders.order_id, order_details.product_id
FROM orders
RIGHT JOIN order_details ON orders.order_id = order_details.order_id;
Result:
This query includes all order details, and for those with associated orders, the order details are included. Order details without an associated order will have NULL values in columns related to orders.

# 4. FULL JOIN (FULL OUTER JOIN):
A FULL JOIN retrieves all records when there is a match in either the left or right table. Non-matching records from both tables contain NULL values.

Example:

sql
SELECT customers.customer_id, orders.order_id
FROM customers
FULL JOIN orders ON customers.customer_id = orders.customer_id;
Result:
This query includes all customers and orders. Where there's a match, both customer and order details are combined. For non-matching records, the columns from the table without a match contain NULL.

# 5. CROSS JOIN:
A CROSS JOIN generates the Cartesian product of two tables, resulting in all possible combinations of records.

Example:

sql
SELECT employees.emp_name, departments.dept_name
FROM employees
CROSS JOIN departments;
Result:
This query includes every combination of employee and department, creating a dataset with a size equal to the product of the number of records in both tables.

# 6. SELF JOIN:
A SELF JOIN joins a table with itself, typically used to compare rows within the same table.

Example:

sql
SELECT a.emp_name, b.emp_name
FROM employees a
INNER JOIN employees b ON a.manager_id = b.emp_id;
Result:
This query compares employees with their managers, creating pairs of employee and manager names.

# 7. NATURAL JOIN:
A NATURAL JOIN performs a join based on columns with the same name in both tables.

Example:

sql
SELECT customers.customer_id, orders.order_id
FROM customers
NATURAL JOIN orders;
Result:
This query includes columns with common names in both "customers" and "orders," automatically joining on these common columns.

# 8. INNER JOIN with UNION:
Combining results of multiple INNER JOINs using the UNION operator.

Example:

sql

SELECT employee_id, project_id
FROM employees
INNER JOIN project_assignments ON employees.employee_id = project_assignments.employee_id
UNION
SELECT employee_id, project_id
FROM contractors
INNER JOIN project_assignments ON contractors.contractor_id = project_assignments.contractor_id;
Result:
The result is a combination of project assignments for both employees and contractors.

# 9. ANTI-JOIN:
An ANTI-JOIN retrieves records from the left table where no match is found in the right table.

Example:

sql
SELECT customers.customer_id
FROM customers
LEFT JOIN orders ON customers.customer_id = orders.customer_id
WHERE orders.customer_id IS NULL;
Result:
This query includes customers who have not placed any orders.

# 10. SEMI-JOIN:
A SEMI-JOIN retrieves records from the left table where a match is found in the right table, but includes each matching row only once.

Example:

sql
SELECT DISTINCT employees.emp_id
FROM employees
WHERE EXISTS (
    SELECT 1
    FROM project_assignments
    WHERE employees.emp_id = project_assignments.emp_id
);
Result:
The result contains distinct employee IDs for those who have at least one project assignment.
