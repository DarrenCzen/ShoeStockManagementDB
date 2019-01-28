# ShoeStockManagementDB
Coded in PostGreSQL 11 as a learning exercise and crash course. A simple database for keeping and listing down the inventory of shoes.

Here are my notes gathered over approx. 8 hours.

PG CRASH COURSE

To connect to PG DB:
You can use PSQL(PG command line) or pgAdmin4 Query Tool

Connecting DB to other software programs:
JDBC (To connect to Java Programs)

To find out current version of PG:
`SELECT VERSION();`

To create DB:
`CREATE DATABASE dvdrental;`

--------------------------------------------------------------------------------------------------

Database is a container which contains Tables, Views, Functions, Indexes.
Tables contains data.
Schema: Logical container/collection which contains tables and other database objects

Tablespaces: Allow admins to define locations in FS where files representing DB objects can be stored.
Views: Virtual tables, Database object that is of a stored query (query from one or more tables).

Functions: SQL Code that can be reused again
Operators - Symbolic Functions

Sequences - Similar to AUTO_INCREMENT in SQL

Primary Key - Unique Identifier
Foreign Key - Used to reference a primary key in another table

PG SQL datatypes
boolean, character, number, temporal, array, special types

character - VARCHAR(N)
number - INT, FLOAT(n), NUMBERIC(P,S) - real number with p digits and s digits behind dp. 
temporal - DATE, TIME, TIMESTAMP
--------------------------------------------------------------------------------------------------
Creating a table:

CREATE TABLE table_name (
	column1_name datatype column_constraint,
	column2_name datatype column_constraint
);

CREATE TABLE person (
	id serial PRIMARY KEY,
	first_name VARCHAR (50),
	last_name VARCHAR (50),
	email VARCHAR (50) UNIQUE
);

--------------------------------------------------------------------------------------------------

Inserting data:
INSERT INTO person (first_name,last_name,email)
VALUES('jack','doe','j.doe@hotmail.com');

--------------------------------------------------------------------------------------------------

WHERE clause:
Filtering rows returned from SELECT query using conditions.

Selecting data from a table:
SELECT column1, column2
FROM table_name
WHERE conditions;

--------------------------------------------------------------------------------------------------

DISTINCT keyword in SELECT statement to prevent duplicates

`ORDER BY column ASC/DESC` to sort data

--------------------------------------------------------------------------------------------------

GROUP BY Clause - used to divide rows returned from select statement into groups:

SELECT column1, aggregate_function(column_2)
FROM table1
GROUP BY column_1;

aggregate functions - AVG, COUNT, MAX, MIN, SUM, FIRST, LAST

--------------------------------------------------------------------------------------------------

HAVING clause - used to in conjunction with GROUP BY clause

SELECT column1, aggregate_function(column_2)
FROM table1
GROUP BY column_1
HAVING condition;

--------------------------------------------------------------------------------------------------

TRUNCATE - remove data from a table after selecting data

DROP - delete a table

--------------------------------------------------------------------------------------------------

UPDATE table_name
SET column1=value1, column2=value2
WHERE condition;

--------------------------------------------------------------------------------------------------

DELETE FROM table_name
WHERE condition;

--------------------------------------------------------------------------------------------------

INSERT INTO table_name(column1,column2)
VALUES (value1,value2);

--------------------------------------------------------------------------------------------------

Comparism Operator: 
= 
<> != 
> >= < <=
IN() - matches value in a list
IS NULL
BETWEEN - within a range
LIKE - pattern matching with wild cards %

--------------------------------------------------------------------------------------------------

BETWEEN clause

SELECT column1, column2
FROM table_name
WHERE column2 BETWEEN value1 AND value2;

there is also NOT BETWEEN

--------------------------------------------------------------------------------------------------

LIKE clause

SELECT column1, column2
FROM table_name
WHERE column2 LIKE 'A%';

--------------------------------------------------------------------------------------------------

other possible condition clauses that are placed in the WHERE section

NOT, OR, AND

IN - selective values

--------------------------------------------------------------------------------------------------

LIMIT clause - to attain a subset or row returned by a query, get number of highest or lowest items in a  table

SELECT column1, column2
FROM table_name
ORDER BY column2
LIMIT n OFFSET m;

if m = 3, n = 4, it will show id 4 5 6 7

--------------------------------------------------------------------------------------------------

UNION operator - used to combine result sets of multiple queries into a single result
queries must have same number of columns and compatible datatypes

UNION ALL - keeps duplicates

INTERSECT operator - returns all rows in both results

EXCEPT operator - return rows by comparing the result sets of two or more queries
return rows in first query that is not present in output of second query.

--------------------------------------------------------------------------------------------------

Types of JOINs - combining data from multiple tables

INNER JOIN - return records that have matching values from columns in both tables

Suppose you want to get data from two tables named A and B 
B has column which relates to primary key column of A

SELECT A.pka, A.data, B.pkb, B.c2
FROM A 
INNER JOIN B ON A.pka = B.fka;

LEFT JOIN

FULL OUTER JOIN

CROSS JOIN

NATURAL JOIN

--------------------------------------------------------------------------------------------------

aggregate functions

COUNT(), MAX()

AVG(), SUM()

--------------------------------------------------------------------------------------------------

analytic window function syntax

window_function(arg1, arg2,..) OVER (PARTITION BY expression ORDER BY expression)


--------------------------------------------------------------------------------------------------

Views - virtual table

CREATE VIEW view_name AS query;

--------------------------------------------------------------------------------------------------

Trigger - Happens when an event involving a table occues. Used to maintain data integrity rules, check accessing activity.

CREATE FUNCTION trigger_function() RETURN trigger AS

CREATE TRIGGER trigger_name {BEFORE|AFTER|INSTEAD OF}{event[OR...]}
ON table_name[FOR[EACH]{ROW|STATEMENT}] EXECUTE PROCEDURE trigger_function

--------------------------------------------------------------------------------------------------
BACK UP DB

pg_dump -U postgres -W -F t <dbname> > c:\pgbackup\<dbname>.tar

pg_restore --dbname=<dbname> -U postgres --verbose tarfilepath

--------------------------------------------------------------------------------------------------
Creating tablespace - location on disk where PG stores data

pg_default (store user data)
pg_global (stores global data)

CREATE TABLESPACE tbspace_name
OWNER user_name
LOCATION directory_path;

e.g. CREATE TABLESPACE dbname LOCATION 'c:\pg\\data\dbname';

--------------------------------------------------------------------------------------------------

To quit
\q
