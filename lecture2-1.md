## Constraints

### Domain Constraints

* Each value must be atomic
* Each value must fit within its assigned domain (data type)

### Key Constraints
What is a Key?
* Makes each tuple (row) unique
* Can be a combination of attributes (column values)
* Different types of keys:
  * Super Key: An attribute or combination of attributes that make tuples unique
  * Candidate Key: any super key minus the attributes that make it 
  * Primary Key
    * Candidate key
    * chosen by database designer

Superkey is a superset of all candidate keys, which are a superset of all primary keys

Example relations with primary keys:
* EMPLOYEE(<u>SSN</u>, LName, FName, Salary)
* DEPT(<u>Dept Number</u>, DName, Location)

In the above database, we can link each employee to their department using Dept Number as a Foreign key.
Why not the other way around? Because its a many:1 relationship (many employees: 1 dept, but not the other way around).
Always place foreign key in the many side of the relationship.

Relationships between two tables fall under "Referential Integrity Constraints".
Primary keys are not allowed to be NULL but foreign keys can be NULL.

## Creating Schema Diagrams

* each table is in a box with its columns listed  

