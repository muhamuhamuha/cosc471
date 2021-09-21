# LECTURE 3-2

## SQL Queries

```sql
-- typical format
SELECT -- <attribute list>
FROM -- <table list>
WHERE -- <conditions>;

SELECT FNAME, LNAME   -- circle sigma symbol
FROM Emp, Dept        -- pie symbol
WHERE Salary > 75000; -- join symbol because choosing more than one table
```

### WARNING

The where clause is the relational-algebra select symbol

The Select clause is the relational-algebra project symbol

## Operators

* "*" everything
* "DISTINCT" removes duplicates
* can use arithmetic operators in select
  * AVG, MIN, MAX, COUNT...
  * result in a summary table with one column

```sql
SELECT LNAME, 1.3 * Salary FROM Emp;
```

* "as" for aliasing

```sql
SELECT E.FNAME FROM Emp AS E;
```

* logical operators like AND, OR, NOT, >, <, >=, ...
* BETWEEN operator
