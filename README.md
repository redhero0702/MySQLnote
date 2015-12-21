MySQL syntax
=====================

SELECT SYNTAX
---------------------
```mysql
SELECT column_name,column_name
FROM table_name;
UNION EXAMPLE
```


SELECT c.City as CITYNAME FROM Customers as c WHERE c.City LIKE "A%"
Union 
SELECT s.City FROM Suppliers as s WHERE s.City LIKE "A%"

UPDATE  SYNTAX
---------------------
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE some_column=some_value;

UPDATE  EXAMPLE
---------------------
SELECT o.OrderID AS OID, o.OrderDate AS ODATE, c.CustomerName AS CUSTOMNAME
FROM Customers AS c, Orders AS o
WHERE c.CustomerName="Around the Horn" AND c.CustomerID=o.CustomerID;

UPDATE  WARNING
---------------------

UPDATE Customers
SET ContactName='Alfred Schmidt', City='Hamburg';
DELETE SYNTAX

- delete specified record
DELETE FROM table_name WHERE some_column=some_value;   
- delete all data
DELETE FROM table_name; or DELETE * FROM table_name; 

LONG SQL SYNTAX (SELECT, AS, ORDER BY)
----------------------------------------------------
SELECT column_name AS alias_column, column_name AS alias_column
FROM table_name AS alias_table
ORDER BY column_name ASC|DESC, column_name ASC|DESC;

CLASSIC EXAMPLE
----------------------------------------------------
SELECT C.CustomerName AS [Customer Name], O.OrderID AS [Order ID]
FROM Customers AS C 
INNER JOIN Orders O
ON C.CustomerID=O.CustomerID
WHERE O.OrderID LIKE '10%'
ORDER BY C.CustomerName
LIMIT 50

SELECT DISTINCT SYNTAX
----------------------------------------------------
SELECT DISTINCT column_name,column_name
FROM table_name;
SELECT DISTINCT EXAMPLE
SELECT DISTINCT City FROM Customers;

ORDER BY Several Columns Example
----------------------------------------------------
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;

UNION SYNTAX
--------------------------------------------------------------------------------------------
- combines the result of more SELECT statements (selects only distinct values by default)
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;

UNION ALL SYNTAX
----------------------------------------------------
- combines the result of two or more SELECT statements (allow duplicated values)
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;

UNION ALL With WHERE
----------------------------------------------------
SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION ALL
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;

SELECT INTO SYNTAX
----------------------------------------------------
- copy all columns into the new table
SELECT *
INTO newtable [IN externaldb]
FROM table1;

- copy only the columns into the new table
SELECT column_name(s)
INTO newtable [IN externaldb]
FROM table1;
SELECT INTO Statement

- create a backup copy of Customers
SELECT *
INTO CustomersBackup2013
FROM Customers;

- Use the IN clause to copy the table into another database
SELECT *
INTO CustomersBackup2013 IN 'Backup.mdb'
FROM Customers;

- Copy only a few columns into the new table
SELECT CustomerName, ContactName
INTO CustomersBackup2013
FROM Customers;

- Copy only the German customers into the new table
SELECT *
INTO CustomersBackup2013
FROM Customers
WHERE Country='Germany';

- Copy data from more than one table into the new table
SELECT Customers.CustomerName, Orders.OrderID
INTO CustomersOrderBackup2013
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID=Orders.CustomerID;

- The SELECT INTO statement can also be used to create a new, empty table using the schema of another
SELECT *
INTO newtable
FROM table1
WHERE 1=0;
WHERE
SELECT pid FROM planets WHERE userid = NULL;
This will not give you the expected result, because from mysql doc

In SQL, the NULL value is never true in comparison to any other value, even NULL. you cannot use an expr = NULL test. The following statement returns no rows, because expr = NULL is never true for any expression
Solution
SELECT pid FROM planets WHERE userid IS NULL; 
To test for NULL, use the IS NULL and IS NOT NULL operators.
- operator IS NULL tests whether a value is NULL.
- operator IS NOT NULL tests whether a value is not NULL.
- MySQL comparison operators


CREATE DATABASE STATEMENT
---------------------------------
CREATE DATABASE dbname;

CREATE TABLE SYNTAX
---------------------------------
CREATE TABLE table_name
(
column_name1 data_type(size),
column_name2 data_type(size),
column_name3 data_type(size),
....
);

CREATE TABLE EXAMPLE
---------------------------------
CREATE TABLE Persons
(
PersonID int,
LastName varchar(255),
FirstName varchar(255),
Address varchar(255),
City varchar(255)
);
DELETE TABLE EXAMPLE
------------------------------------------------------------------
- delete records with specified condition
DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste' AND ContactName='Maria Anders';
- delete all data in a table
DELETE FROM table_name; 
DELETE * FROM table_name;

CREATE TABLE + CONSTRAINT SYNTAX
------------------------------------------------------------------
CREATE TABLE table_name
(
column_name1 data_type(size) constraint_name,
column_name2 data_type(size) constraint_name,
column_name3 data_type(size) constraint_name,
....
);
In SQL, we have the following constraints:
1. NOT NULL - Indicates that a column cannot store NULL value
2. UNIQUE - Ensures that each row for a column must have a unique value
3. PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Ensures that a column (or combination of two or more columns) have a unique identity which helps to find a particular record in a table more easily and quickly
4. FOREIGN KEY - Ensure the referential integrity of the data in one table to match values in another table
5. CHECK - Ensures that the value in a column meets a specific condition
6. DEFAULT - Specifies a default value for a column

COPY TABLE
------------------------------------------------------------------
CREATE TABLE new_table LIKE old_table;
INSERT new_table SELECT * FROM old_table;

SQL NOT NULL Constraint
------------------------------------------------------------------
CREATE TABLE PersonsNotNull
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255)
)

HAVING SYNTAX
------------------------------------------------------------------
- The HAVING clause was added to SQL because the WHERE keyword could not be used with aggregate functions.
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
HAVING aggregate_function(column_name) operator value;
