
<style>
  .question {
    color: red;
  }

  .answer {
    color: green;
  }
</style>

# Lecture 5-1

## Views

* sometimes its not desirable for all users to see the logical model
  * i.e. all the relations stored in the database
  * consider someone needs to know an instructor's name and department but not salary
    * temp tables would not be a good solution for this problem
    * if the master table is updated, the temp table would also have to be updated...
  * a view is a mechanism to hide certain data from the view of certain users
  * any relation that is not part of the conceptual model but is visible to a user as virtual relation is a view
* View tables are not saved, view queries are saved
* View tables should not be updated
* Materialized views are saved
  * <span class="question">What are these used for?</span>
  * <span class="question">Why create these?</span>
* <span class="question">Can views be used in calculations?</span>
* <span class="question">Is saving a summary (to be used in reporting) in a view ok? Or is there a better mechanism for doing something like this (e.g. just save it as a table?)</span>


```sql
-- CREATE VIEW view_name AS <some valid SQL here>

-- view not created
CREATE VIEW dependent_names AS (
  SELECT eSSN, DName
  FROM dependent_table;
)

-- view created
SELECT * FROM dependent_names;
```

## Maintaining Integrity Constraints

* Example constraints
  * NOT NULL
    * Forces a column to not have any NULL
  * PRIMARY KEY
  * UNIQUE
    * Forces a column to only allow unique values
  * DEFAULT
    * Will assign a default value to a column, if it's not specified it will resort to this default instead of null
  * CHECK -predicate-

```sql
CREATE TABLE section (
  course_id       VARCHAR(8)      NOT NULL,
  sec_id          VARCHAR(8),
  semester        VARCHAR(6),
  "year"          NUMERIC(4, 0),
  building        VARCHAR(15)     NOT NULL,
  room_number     VARCHAR(7)      DEFAULT = 0,
  time_slot_id    VARCHAR(4), 
  PRIMARY KEY(course_id, sec_id, semester, "year"),
  CHECK (semester IN ('Fall', 'Winter', 'Spring', 'Summer'))
);
```

### Referential Integrity

* A foreign key in another table is guaranteed to reference something that exists
* What if the attribute the foreign key is referencing is updated/deleted? How should that be handled?
  1. Either never allow what the keys are referencing to be updated/deleted,
  2. or; change the foreign key to NULL if what it references is deleted,
      * SET NULL
  3. or; set the foreign key to a default value,
      * SET DEFAULT
  4. or; delete the rows if their reference is deleted
      * This is called CASCADE DELETE
      * CASCADE UPDATE is similar

```sql
CREATE TABLE course (
  course_id         CHAR(5)       PRIMARY KEY,
  title             VARCHAR(20),
  dept_name         VARCHAR(20)   REFERENCES department 
);

CREATE TABLE course (
  ...

  dept_name         VARCHAR(20)   REFERENCES department 
    ON DELETE SET DEFAULT
    ON UPDATE CASCADE,

  ...
);
```

## SQL Data Types

* date, containing a 4-digit year, month, and date
  * e.g. DATE '2005-7-27'
* time, in hours, minutes, and seconds
  * e.g. TIME '09:00:30'
* timestamp, date + time
  * e.g. TIMESTAMP '2005-7-27T09:00:30'
* interval, period of time
  * e.g. INTERVAL '1' day
  * arithmetic on date/time/timestamp value from another gives INTERVAL
  * INTERVAl can be added back to date/time/timestamp values
* clob (character large object)
* blob (binary large object)

### Create Custom Data Type

```sql
CREATE TYPE Dollars AS NUMERIC(12, 2) FINAL

CREATE TABLE department (
  dept_name         VARCHAR(20),
  building          VARCHAR(15),
  budget            Dollars
);
```

## Indexes

* by default, these are created from primary key
* can also be created

```sql
CREATE INDEX lname_ind ON employee(lname);
```

## Authorization

* Identity Access Management...

## Recursive Queries

* find supervisor of supervisor...
* can be done manually with UNION
* would typically be done with a loop
* <span class="question">Can this be done with a dynamic view and a CASE clause?</span>

## Interfacing With A Programming Language

* API can be created to interact with a database server
* Done using ODBC/JDBC
