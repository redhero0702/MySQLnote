MySQL syntax
=====================

SELECT 
---------------------
- SYNTAX

```sql
SELECT column_name,column_name
FROM table_name;
UNION EXAMPLE
```

- SELECT AND UNION


```sql
SELECT c.City as CITYNAME FROM Customers as c WHERE c.City LIKE "A%"
Union 
SELECT s.City FROM Suppliers as s WHERE s.City LIKE "A%"
```

UPDATE  
---------------------
 - SYNTAX
 
```sql
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE some_column=some_value;
```

 - EXAMPLE
 
```sql
SELECT o.OrderID AS OID, o.OrderDate AS ODATE, c.CustomerName AS CUSTOMNAME
FROM Customers AS c, Orders AS o
WHERE c.CustomerName="Around the Horn" AND c.CustomerID=o.CustomerID;
```

 - UPDATE  WARNING
 
```sql
UPDATE Customers
SET ContactName='Alfred Schmidt', City='Hamburg';
```

DELETE 
---------------------
- delete specified record

```sql
DELETE FROM table_name WHERE some_column=some_value;   
```

- delete all data

```sql
DELETE FROM table_name; or DELETE * FROM table_name; 
```

LONG SQL SYNTAX (SELECT, AS, ORDER BY)
----------------------------------------------------
```sql
SELECT column_name AS alias_column, column_name AS alias_column
FROM table_name AS alias_table
ORDER BY column_name ASC|DESC, column_name ASC|DESC;
```

CLASSIC EXAMPLE
----------------------------------------------------
```sql
SELECT C.CustomerName AS [Customer Name], O.OrderID AS [Order ID]
FROM Customers AS C 
INNER JOIN Orders O
ON C.CustomerID=O.CustomerID
WHERE O.OrderID LIKE '10%'
ORDER BY C.CustomerName
LIMIT 50
```

SELECT DISTINCT 
----------------------------------------------------
- SYNTAX

```sql
SELECT DISTINCT column_name,column_name
FROM table_name;
```

- EXAMPLE

```sql
SELECT DISTINCT City FROM Customers;
```


ORDER BY
----------------------------------------------------
```sql
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```

UNION
--------------------------------------------------------------------------------------------
- UNION, combines the result of more SELECT statements (selects only distinct values by default)

```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

- UNION ALL, combines the result of two or more SELECT statements (allow duplicated values)

```sql
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
```

- UNION ALL with WHERE

```sql
SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION ALL
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;
```

SELECT INTO
----------------------------------------------------
- copy all columns into the new table

```sql
SELECT *
INTO newtable [IN externaldb]
FROM table1;
```

- copy only the columns into the new table

```sql
SELECT column_name(s)
INTO newtable [IN externaldb]
FROM table1;
```

- create a backup copy of Customers

```sql
SELECT *
INTO CustomersBackup2013
FROM Customers;
```

- Use the IN clause to copy the table into another database

```sql
SELECT *
INTO CustomersBackup2013 IN 'Backup.mdb'
FROM Customers;
```

- Copy only a few columns into the new table

```sql
SELECT CustomerName, ContactName
INTO CustomersBackup2013
FROM Customers;
```

- Copy only the German customers into the new table

```sql
SELECT *
INTO CustomersBackup2013
FROM Customers
WHERE Country='Germany';
```

- Copy data from more than one table into the new table

```sql
SELECT Customers.CustomerName, Orders.OrderID
INTO CustomersOrderBackup2013
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID=Orders.CustomerID;
```

- The SELECT INTO statement can also be used to create a new, empty table using the schema of another

```sql
SELECT *
INTO newtable
FROM table1
WHERE 1=0;
```

WHERE
----------------------
```sql
SELECT pid FROM planets WHERE userid = NULL;
This will not give you the expected result, because from mysql doc
```

> In SQL, the NULL value is never true in comparison to any other value, even NULL. you cannot use an expr = NULL test. The following statement returns no rows, because expr = NULL is never true for any expression

#### solution
```sql
SELECT pid FROM planets WHERE userid IS NULL; 
```

To test for NULL, use the IS NULL and IS NOT NULL operators.

1. operator IS NULL tests whether a value is NULL.
2. operator IS NOT NULL tests whether a value is not NULL.
3. MySQL comparison operators


CREATE DATABASE STATEMENT
---------------------------------
```sql
CREATE DATABASE dbname;
```

MANIPULATE TABLE 
---------------------------------
- CREATE A TABLE

```sql
CREATE TABLE table_name
(
column_name1 data_type(size),
column_name2 data_type(size),
column_name3 data_type(size),
....
);
```

- EXAMPLE

```sql
CREATE TABLE Persons
(
PersonID int,
LastName varchar(255),
FirstName varchar(255),
Address varchar(255),
City varchar(255)
);
```

- DELTE TABLE, delete records with specified condition

```sql
DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste' AND ContactName='Maria Anders';
```

- DELTE TABLE, delete all data in a table

```sql
DELETE FROM table_name; 
DELETE * FROM table_name;
```

CREATE TABLE WITH CONSTRAINTS
------------------------------------------------------------------
```sql
CREATE TABLE table_name
(
column_name1 data_type(size) constraint_name,
column_name2 data_type(size) constraint_name,
column_name3 data_type(size) constraint_name,
....
);
```


SQL CONSTRAINTS
-----------------------------
1. NOT NULL - Indicates that a column cannot store NULL value
2. UNIQUE - Ensures that each row for a column must have a unique value
3. PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Ensures that a column (or combination of two or more columns) have a unique identity which helps to find a particular record in a table more easily and quickly
4. FOREIGN KEY - Ensure the referential integrity of the data in one table to match values in another table
5. CHECK - Ensures that the value in a column meets a specific condition
6. DEFAULT - Specifies a default value for a column

COPY TABLE
------------------------------------------------------------------
```sql
CREATE TABLE new_table LIKE old_table;
INSERT new_table SELECT * FROM old_table;
```

SQL NOT NULL Constraint
------------------------------------------------------------------
```sql
CREATE TABLE PersonsNotNull
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255)
)
```

HAVING SYNTAX
------------------------------------------------------------------

The HAVING clause was added to SQL because the WHERE keyword could not be used with 
aggregate functions.

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
HAVING aggregate_function(column_name) operator value;
```
