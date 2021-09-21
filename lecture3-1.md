# LECTURE 3-1

## DDL

Used to create and update descriptions of tables

### Create, Alter, and Drop Tables

#### CREATE

* Creates a new base relation by giving it a name
* Specifies all the columns in the new table and their data types
  * INTEGER
  * FLOAT
  * DECIMAL
  * CHAR
  * VARCHAR -- max length must be specified
* The constraint NOT NULL may be specified on a column

Example:

```sql
CREATE TABLE DEPARTMENT (
  DNAME     VARCHAR(10)   NOT NULL,
  DNUMBER   INTEGER       NOT NULL,
  MGRSSN    CHAR(9),
  STARTDATE CHAR(9),
  PRIMARY KEY (DNUMBER),
  UNIQUE (DNAME),  -- this would be a candidate key
  FOREIGN KEY (MGRSSN) REFERENCES EMP,
);
```

#### ALTER

* adds columns to a table
* NOT NULL constraint is not allowed since all rows will be NULL once the command is run
* rows can be updated using **UPDATE** DML command

Example:

```sql
ALTER TABLE EMPLOYEE
  ADD JOB VARCHAR(12);
```

#### DROP

* removes a relation and its definition
* relation can no longer be queried if this is run

Example:

```sql
DROP TABLE DEPARTMENT;
```

### Setting primary and foreign key constraints

### Unique, not null, and default constraints

## DML

### Insert

* used to append rows to a table
* columns should be listed in the same order as used by **CREATE TABLE** DDL

Example 1:

```sql
INSERT INTO EMPLOYEE
  VALUES(
    'Richard',
    'K',
    'Man',
    '6543221',
    '30-DEC-42',
    '84 Oak Forest, Katy, TX',
  );
```

Example 2:

```sql
-- specifies columns
INSERT INTO EMPLOYEE (FNAME, LNAME, SSN)
  VALUES(
    'Richard',
    'Johnson',
    '654321234',
  );

```

### Delete

```sql
-- removes all rows from table:
DELETE FROM EMPLOYEE;

-- removes specific rows:
DELETE FROM EMPLOYEE WHERE LNAME='Brown';
```

### Update

```sql
UPDATE PROJECT
SET (
  PLOCATION = 'Bellaire',
  DNUM = 5,
)
WHERE PNUMBER = 10;
```
