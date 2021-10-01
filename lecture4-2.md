
## Grouping Results

* Aggregation functions:
  * avg
  * min
  * max
  * sum
  * count
* HAVING clause is used instead of WHERE when filtering must be done on resulting table

```sql
-- group by attribute is used in select
SELECT something, SUM(something_else)
FROM somewhere
WHERE something = 'this_or_that'
GROUP BY something;

-- HAVING clause
-- find average salary of all employees in departments with only two employees
SELECT DNo, AVG(Salary)
FROM Employee
GROUP BY DNo
HAVING COUNT(SSN) > 2;

```

## Ordering Results

```sql
SELECT something
FROM somewhere
WHERE something = 'this_or_that'
ORDER BY something DESC  -- ascending (ASC) by default
```

## Nested Queries (Sub-Query)

```sql
-- can run subquery off any of these clauses
SELECT  (SELECT ...)
FROM    (SELECT ...)
WHERE   (SELECT ...)
```

* not the same as using UNION or INTERSECTION, though similar results may be achieved
* used for:
  1. Value comparison at WHERE clause using comparison operators (gt, lt...)
  2. Set membership at WHERE clause using IN or NOT IN
  3. Set comparison at WHERE clause using SOME or ALL
  4. Empty sets at WHERE clause using EXISTS or NOT EXISTS

```sql

-- value comparison
-- salary where salary is greater than average salary
SELECT *
FROM employee
WHERE SALARY > (SELECT AVG(SALARY) FROM employee);

-- set membership
--
SELECT *
FROM employee
WHERE ssn NOT IN (SELECT ESSN FROM department);

-- set comparison
-- salaries greater than all employees from department 5
SELECT *
FROM employee
WHERE SALARY > ALL(SELECT salary FROM employee WHERE DNo = 5);

-- empty sets
SELECT *
FROM empoloyee
WHERE NOT EXISTS (SELECT * FROM "dependent" WHERE ssn = essn)

-- correlated query
-- subquery references attributes from outside query

-- subquery in UPDATE is possible

```

## DB Updates Using SELECT
