# SQL & Databases

## Databases

-   organized collection of structured information, or data
-   usually on some form of a computer
-   **persistent** storage of data
    -   data storage that retains after a device is powered off
-   **_Spreadsheets vs Databases_**
    -   **Spreadsheets**
        -   One-time analysis
        -   Quickly need to chart/visualize something out
        -   Reasonable data setsize
        -   Ability for untrained individuals to readily pick it up
    -   **Databases**
        -   Data integrity
        -   Massive amounts of data
        -   Quickly combine different datasets
        -   Automate steps for re-usability
        -   Can support data for websites and apps

## Database Management System (DBMS)

-   Software designed to store, manage and access data.
-   Serves as an interface between an end-user and a database
-   can be classified based on a variety of criteria such as:
    -   the data model
    -   the database distribution
    -   user numbers.
-   Allows for **CRUD** operations
    -   *C*reating
    -   *R*eading
    -   *U*pdating
    -   *D*eleting data
-   Most widely used types of DBMS software are
    -   distributed
    -   hierarchical
    -   object-oriented
    -   network
    -   **relational**

## Relational Database Management System(RDBMS)

-   Focus is on **Relational Database**
    -   been around since the '70s
    -   Stores and provides data that is **related/connected** to each other
        -   Increases query speed
    -   Based around _normalization_ of records(rows) and attributes(columns) of entities(tables)
-   **Schema**
    -   The rules and structure of your database
    -   Your relational model
-   **SQL** is the language used for relational databases
-   _Flavors of Relational DBS_
    -   Microsoft SQL Server
    -   Oracle Database
    -   IBM Db2
    -   MySQL
    -   **PostgreSQL**
        -   great for learning how to use SQL

# **Structured Query Language**(SQL)

## Syntax

-   All commands start with any of the keywords
-   Always end in a semicolon
-   SQL is **case insensitive**
    -   SELECT & select have the same meaning

## Sub-Languages of SQL

### DDL(Data Definition Language)

-   Anything that defines the schema
-   Create and modify the structure of **database objects**
    -   **NOT DATA** ,

```sql
    create -- Used to create the objects in a database (or the database itself)
    alter -- Alters the structure of your database, changes schema
    drop -- Delete objects from the database
    truncate -- Remove all of the records of a table, maintains the schema and table object
```

#### Constraints

-   Are part of DDL
-   They allow you to put restrictions on what can go in each attribute(column value) on a table

```sql
primary key --uniquely identifies the entity
not null -- prevents null records into an attribute
unique -- all records in this attribute must be unique
check -- data must meet the specified criteria
foreign key -- references a primary key from another table
```

### DML(Data Manipulation Language)

-   Anything that manipulates dta _data within_ a table

```sql
insert -- inserts data into our table
update set -- updates existing data within our table
delete -- Removes records from our table
```

### DQL (Data Query Language)

-   Any statement that reads data
-   Gets some schema realtion based ont eh qeury passed to it
-   Results compiled into a temporary table

```sql
select -- Queries our table for the information requestied by our query syntax
select distinct -- Queries our tbale and returns only unique values
select * from coach where first_name = 'Bob'; -- Grabbing all columns from the coach table where the coaches firstname is Bob
```

### DCL(Data Control Language)

-   Responsible for assigning permissions for developers working on the database
-   Database admin generally handles this

```sql
grant -- Gives user acces privileges to the database
revoke -- Command withdraws the user's access privileges given by the GRANT command
```

### TCL(Transaction Control Language)

-   Repsonsible for creating and saving transactions
-   provides the privilege to rollback the transaction if the data is updated in the tables by mistake
-   By default, JDBC and DBeaver "auto-commit"

```sql
commit -- Commits a transaction
rollback -- Rollback a transatction in case of any errors
savepoint -- sets a savepoint with a transaction
```

# Transactions

-   represents a single unit of work performed in sequence against the database.
-   is a collection of read/write operations which succeeds only if all contained operations succeed.
-   A transaction has 4 properties termed as **_[ACID](https://en.wikipedia.org/wiki/ACID) Properties_**:
    -   **A**tomicity
        -   Atomicity means that either all of the transactions will execute successfully or none of them will.
    -   **C**onsistency
        -   Consistency means that constraints are enforced for every committed transaction.
        -   That indicates that all Keys, Data types, Checks, and Triggers are successful and no constraint violation is triggered.
    -   **I**solation
        -   If two transactions are executing concurrently and working on the same data, then one transaction should not disturb the other transaction.
        -   Isolation guarantees that concurrently running transactions should not affect each other.
    -   **D**urability
        -   Durability means that once a transaction is complete, it guarantees that all of the changes are recorded in the database.
        -   If our system is suddenly affected by a system crash or a power outage, then all unfinished committed transactions may be replayed.

# _KEYS_

-   **Canidate Key**
    -   column that can _act_ as a primary key
    -   **ISN'T A PRIMARY KEY**
-   **Primary key**
    -   **uniquely ASSIGNED** identifier for a row
    -   doesn't _NEED_ to be one value
-   **Composite Key**
    -   Multiple columns that act as a primary key
    -   **CAN BE A PRIMARY KEY**
-   **Foreign Key**
    -   Constraint that you can put on a column
    -   This column MUST refer to a unique column in another table
    -   The table with a foreign key is always referred to as a **CHILD**.
    -   The table it refers to is the **PARENT**.

## **Referential Integrity**

-   Foreign Keys must ALWAYS point to a valid record
-   There are no orphan records
    -   Records whose foreign keys point to records that don't exist
-   Attempting to delete a primary key that referenced as a foreign key will result in error
    -   _CAN_ use on delete cascade

# Joins Operators

-   Normalized databases spread the data out accross multiple tables
    -   Can make it difficult to read information
-   Joins combine tables horizontally based on the join predicate 'on'

```sql
select * from player left join coach on player.t_id = coach.t_id;

left join -- all records in the left table plus matches on the right
right join -- all records in the right table plus matches ont he left
inner join -- only records that match
cross join -- every record matched with every record
```

![Joins](https://i.stack.imgur.com/4zjxm.png)

### Union

-   combine the result set of two or more select statements ontop of one another
-   Unions should be logical and should match up with one another
-   Imagine stacking two tables on top of one another

## Functions

-   **Scalar** functions
    -   Take in a single input and give a single output

```sql
-- x = column_name
upper(x) -- uppercase
lower(x) -- lowercase
length(x) -- how long
round(x,0)
mid(x,1,4)

```

-   **Aggregate** functions
    -   Take in a values in a column and gives a single output
    -   Can be paired with group by to create bucket values

```sql
avg()
sum()
min()
count()

select * avg(salary) from coach group by t_id;
```

# Normalization

-   Reducing Redundancy & Dependencyin our databases
    -   Redundant data = useless data = same data stored in the more than one place
-   Divides larger tables into smaller tables and links them using relationships
-   Ranges from 1st to 6th Normalized Form (NF)
    -   **_Industry standard is 3NF_**
-   **_Not always a good thing_**
    -   **Pros**
        -   Increases Transaction Speed
        -   Decrease the amount of data Stored
    -   **Cons**
        -   Makes data more difficult to query
-   **Entity Relationship Diagram(ERD)**
    -   shows entities in a database and the realtionships between tables within that database
    -   3 Basic Elements
        -   **Entites** are the "things" for which we want to store information (our tables)
        -   **Attributes** are the data we want to collect for an entity(columns)
        -   Relationship describes the relations between entities

![Entity Relationship Diagram](https://user-images.githubusercontent.com/6398845/62544355-e7b03700-b85f-11e9-90b2-dfaf3933cf16.png)

-   **1NF**
    -   All records should be uniquely identifiable
        -   _Make sure you have a primary key_
    -   All data in the table should be **atomic**
        -   Data cannot be broken down into smaller more meaningful units
    -   All records in an column is of the same datatype
    -   Disallows multi-valued and composite attributes and their combinations
        -   A field is not a list of something
        -   No array-like data in the table

## Example: 1NF

### Suppose we want to store our employees phone numbers and location

<hr>

## Employee Table

| Employee Name | Employee Phone      |
| ------------- | ------------------- |
| Ashwin        | 476487468           |
| Ashwin        | 476487468           |
| Adam          | 474749498,974647494 |
| Ben           | 3838749043,47349844 |
| Charles       | 3242355233          |

-   The above table _FAILS_ first normalized form
    -   Duplicate entries (row 1 & 2)
    -   Phone column has 2 values in "array-like" structure

## Employee Phone

| Employee ID | Employee Phone | Employee Name |
| ----------- | -------------- | ------------- |
| 29          | 476487468      | Ashwin        |
| 39          | 974647494      | Adam          |
| 39          | 474749498      | Adam          |
| 49          | 383874904      | Ben           |
| 49          | 473498443      | Ben           |
| 59          | 324235523      | Charles       |

-   The above table satisfies 1NF. GOOD JOB!
    <hr>

## 2NF

-   You are in 1NF
-   All non-key attributes are **fully functional dependent** on the whole of the primary key
    -   every coulmn that is not a primary key (non-key attirbute) is dependent on the **WHOLE** of the primary key
-   Relation with a **single-attribute** priary key is automatically in at least 2NF
-   Relations not in 2NF are _more likely_ to suffer from update anomalies

## Example

### Suppose we wanted a table with all of the training offered here & who teaches them

| Employee ID | Curriculum ID | Curriculum                | Cost      | StartDate |
| ----------- | ------------- | ------------------------- | --------- | --------- |
| 29          | 1             | Golf                      | 90000000  | 1/20/21   |
| 39          | 2             | Cloud Native React Native | 20000     | 12/06/21  |
| 49          | 3             | Primer                    | 40000     | 12/20/21  |
| 59          | 3             | Primer                    | 40000     | 12/20/21  |
| 49          | 4             | PEGA                      | 109809129 | 2/4/24    |
| 59          | 5             | Java/React                | 10913919        | 1/24/22       |
| 59          | 6             | Training the Trainer      | 10     |11/29/21      |

-   The above table _FAILS_ to satisfy 2NF
    -   Employee Name and Position is a non-key attribute that is **DEPENDENT** on just employee ID

## Training Table

| Curriculum ID | Curriculum                | Cost      |
| ------------- | ------------------------- | --------- |
| 1             | Golf                      | 90000000  |
| 2             | Cloud Native React Native | 20000     |
| 3             | Primer                    | 40000     |
| 4             | PEGA                      | 109809129 |
| 5             | Java/React                | 10913919        |
| 6             | Training the Trainer      | 10     |

## Training per Employee

| Employee ID | Curriculum ID |
| ----------- | ------------- |
| 29          | 1             |
| 39          | 2             |
| 49          | 3             |
| 49          | 4             |
| 59          | 5             |
| 59          | 3             |
| 59          | 6             |

-   The above tables satifies the 2NF!!!

<hr>

# 3NF

-   You are in 2NF
-   No transitive functional dependencies

## Employee Location Table

| Employee ID | Employee Name | Position           | State | ZIP   | City         |
| ----------- | ------------- | ------------------ | ----- | ----- | ------------ |
| 29          | Ashwin        | CEO                | VA    | 12837 | Reston       |
| 39          | Adam          | Lead Trainer       | WV    | 49818 | Morgantown   |
| 49          | Ben           | Sr Trainer         | FL    | 93901 | Miami        |
| 59          | Charles       | Training Asssitant | PA    | 18901 | Philadelphia |

-   This satisfies 1NF & 2NF
    -   The State, ZIP and City are all dependent on the whole of the primary key
    -   **BUT** City and State are **ALSO** dependent on ZIP

## Employee Table

| Employee ID | Employee Name | Position           | ZIP   |
| ----------- | ------------- | ------------------ | ----- |
| 29          | Ashwin        | CEO                | 12837 |
| 39          | Adam          | Lead Trainer       | 49818 |
| 49          | Ben           | Sr Trainer         | 93901 |
| 59          | Charles       | Training Asssitant | 18901 |

## Location Table

| ZIP   | State | City         |
| ----- | ----- | ------------ |
| 12837 | VA    | Reston       |
| 49818 | WV    | Morgantown   |
| 93901 | FL    | Miami        |
| 18901 | PA    | Philadelphia |

-   This now satisfies the 3NF!!! WOOO!!!
    -   Location table

## Multiplicities

-   One to One
    -   One record matches to one record in another table
-   One to Many
    -   Once record mathces to many records in anothe table
-   Many to Many
    -   Many records ina table match to many records in antoher tablee
    -   Modeled using a junction table
        -   Table that has two foreign keys

