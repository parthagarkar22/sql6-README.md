CREATE TABLE Employees (
    emp_id INTEGER PRIMARY KEY,
    name TEXT,
    department_id INTEGER,
    salary INTEGER
);

CREATE TABLE Departments (
    department_id INTEGER PRIMARY KEY,
    department_name TEXT
);
INSERT INTO Departments VALUES (1, 'HR'), (2, 'IT'), (3, 'Finance');

INSERT INTO Employees VALUES 
(1, 'Alice', 1, 50000),
(2, 'Bob', 2, 60000),
(3, 'Charlie', 2, 70000),
(4, 'David', 3, 55000),
(5, 'Eva', 1, 52000);
SELECT 
    name,
    (SELECT department_name FROM Departments d WHERE d.department_id = e.department_id) AS dept_name,
    salary,
    (SELECT AVG(salary) FROM Employees WHERE department_id = e.department_id) AS avg_dept_salary
FROM Employees e;
SELECT *
FROM Employees
WHERE salary > (SELECT AVG(salary) FROM Employees);
SELECT d.department_name, dept_summary.total_salary
FROM Departments d
JOIN (
    SELECT department_id, SUM(salary) AS total_salary
    FROM Employees
    GROUP BY department_id
) AS dept_summary
ON d.department_id = dept_summary.department_id;
