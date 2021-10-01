
## Set Operations

* union, intersect, except, minus
  * automatically removes duplicates
  * can only use on "union-compatible relations"
    1. same number of attributes
    2. same domains (data types)
    3. attribute names from table1 are retained
  * usually done on subset of same table

```sql
SELECT * FROM table1 WHERE UNION|INTERSECT|EXCEPT SELECT * FROM table2;

-- find courses that ran in Fall '09 OR Spring '10
(SELECT course_id FROM section WHERE sem = 'Fall' AND "year" = 2009)
UNION
(SELECT course_id FROM section WHERE sem = 'Spring' AND "year" = 2010);

-- find courses that ran in Fall '09 AND Sprint '10
(SELECT course_id FROM section WHERE sem = 'Fall' AND "year" = 2009)
INTERSECT
(SELECT course_id FROM section WHERE sem = 'Spring' AND "year" = 2010);

-- find courses that in Fall '09 but not in Spring '10
(SELECT course_id FROM section WHERE sem = 'Fall' AND "year" = 2009)
EXCEPT
(SELECT course_id FROM section WHERE sem = 'Spring' AND "year" = 2010);
```

## Handling Nulls

* Arithmetic operations on NULL type = NULL
* Comparison operations (< or >) on NULL = 'Unkonwn'

|x      |y      |AND    |OR     |
|-------|-------|-------|-------|
|True   |Unknown|Unknown|True   |
|False  |Unknown|False  |Unknown|
|Unknown|Unknown|Unknown|Unknown|

* IS NULL or IS NOT NULL predicates are available to use
* DISTINCT treats two NULLs as equal

```sql
SELECT "name"
FROM some_table
WHERE "name" IS NULL;
```

## Multiple-Table Queries (Joins)

```sql
-- cartesian product
SELECT * FROM employee, department;

-- join
SELECT * FROM employee, department WHERE employee.DNo = department.DNumber;

-- natural join fixes two+ tables on their common attributes
-- Incorrect version (equates course.dept_name with instructor.dept_name)
SELECT "name", title
FROM instructor
NATURAL JOIN teaches NATURAL JOIN course;
-- Correct version
SELECT "name", title
FROM instructor
NATURAL JOIN teaches, course
WHERE teaches.course_id = course.course_id;
-- Another correct version
SELECT "name", title
FROM (instructor natural join teaches) JOIN course USING(course_id);

-- aliasing tables
SELECT D, E.name
FROM employee AS E, department AS D
WHERE E.DNo = D.Dnum AND E.Dno < 3;

-- self-join by giving one table two aliases
SELECT E.Lname, E2.Lname
FROM employee AS E, Employee AS E2
WHERE E.SuperSSN = E2.SSN;

-- outer join by creating nulls wherever there is no foreign-primary key match
-- left outer join keeps everything from left table, right outer join keeps everything from right

-- inner join is the same thing as natural join

```


