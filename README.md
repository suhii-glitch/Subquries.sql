# Subquries.sql
-- SubQueries Assignment Solution
-- Employee, Department & Sales Dataset
-- PwSkills SQL Assignment

-- Q1: Retrieve the names of employees who earn more than the average salary of all employees.
SELECT name
FROM employee
WHERE salary > (
    SELECT AVG(salary)
    FROM employee
);

-- Q2: Find the employees who belong to the department with the highest average salary.
SELECT name
FROM employee
WHERE department_id = (
    SELECT department_id
    FROM employee
    GROUP BY department_id
    ORDER BY AVG(salary) DESC
    LIMIT 1
);

-- Q3: List all employees who have made at least one sale.
SELECT name
FROM employee
WHERE emp_id IN (
    SELECT DISTINCT emp_id
    FROM sales
);

-- Q4: Find the employee with the highest sale amount.
SELECT name
FROM employee
WHERE emp_id = (
    SELECT emp_id
    FROM sales
    ORDER BY sale_amount DESC
    LIMIT 1
);

-- Q5: Retrieve the names of employees whose salaries are higher than Shubham’s salary.
SELECT name
FROM employee
WHERE salary > (
    SELECT salary
    FROM employee
    WHERE name = 'Shubham'
);

-- Q6: Find employees who work in the same department as Abhishek.
SELECT name
FROM employee
WHERE department_id = (
    SELECT department_id
    FROM employee
    WHERE name = 'Abhishek'
)
AND name <> 'Abhishek';

-- Q7: List departments that have at least one employee earning more than ₹60,000.
SELECT department_name
FROM department
WHERE department_id IN (
    SELECT department_id
    FROM employee
    WHERE salary > 60000
);

-- Q8: Find the department name of the employee who made the highest sale.
SELECT department_name
FROM department
WHERE department_id = (
    SELECT department_id
    FROM employee
    WHERE emp_id = (
        SELECT emp_id
        FROM sales
        ORDER BY sale_amount DESC
        LIMIT 1
    )
);

-- Q9: Retrieve employees who have made sales greater than the average sale amount.
SELECT name
FROM employee
WHERE emp_id IN (
    SELECT emp_id
    FROM sales
    WHERE sale_amount > (
        SELECT AVG(sale_amount)
        FROM sales
    )
);

-- Q10: Find the total sales made by employees who earn more than the average salary.
SELECT SUM(sale_amount) AS TotalSales
FROM sales
WHERE emp_id IN (
    SELECT emp_id
    FROM employee
    WHERE salary > (
        SELECT AVG(salary)
        FROM employee
    )
);

-- Q11: Find employees who have not made any sales.
SELECT name
FROM employee
WHERE emp_id NOT IN (
    SELECT emp_id
    FROM sales
);

-- Q12: List departments where the average salary is above ₹55,000.
SELECT department_name
FROM department
WHERE department_id IN (
    SELECT department_id
    FROM employee
    GROUP BY department_id
    HAVING AVG(salary) > 55000
);

-- Q13: Retrieve department names where the total sales exceed ₹10,000.
SELECT department_name
FROM department
WHERE department_id IN (
    SELECT department_id
    FROM employee
    WHERE emp_id IN (
        SELECT emp_id
        FROM sales
        GROUP BY emp_id
        HAVING SUM(sale_amount) > 10000
    )
);

-- Q14: Find the employee who has made the second-highest sale.
SELECT name
FROM employee
WHERE emp_id = (
    SELECT emp_id
    FROM sales
    ORDER BY sale_amount DESC
    LIMIT 1 OFFSET 1
);

-- Q15: Retrieve the names of employees whose salary is greater than 
-- the highest sale amount recorded.
SELECT name
FROM employee
WHERE salary > (
    SELECT MAX(sale_amount)
    FROM sales
);
