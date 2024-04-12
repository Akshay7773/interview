## Q.1 can you tell me about ALTER command in SQL?
The ALTER command in SQL is used to modify existing database objects, such as tables, views, or procedures. It allows you to change the structure of a table, 
add or remove columns, modify column data types, rename objects, or add constraints. 

Here's a basic syntax for altering a table:

```sql
ALTER TABLE table_name
  ADD column_name datatype;

ALTER TABLE table_name
  DROP COLUMN column_name;

ALTER TABLE table_name
  MODIFY COLUMN column_name datatype;

ALTER TABLE table_name
  RENAME TO new_table_name;
```

These are just a few examples. The ALTER command provides a wide range of options depending on the specific database management system (DBMS) 
being used (e.g., MySQL, PostgreSQL, SQL Server, etc.).

<br> 


## Q.2 Update command in SQL
The UPDATE command in SQL is used to modify existing records in a table. It allows you to change the values of one or more columns in one or more rows based on specified conditions.

Here's the basic syntax for the UPDATE command:

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

In this syntax:

- `table_name` is the name of the table you want to update.
- `column1`, `column2`, etc., are the names of the columns you want to update.
- `value1`, `value2`, etc., are the new values you want to set for the corresponding columns.
- `condition` is an optional clause that specifies which rows to update. If omitted, all rows in the table will be updated.

For example, to update the 'salary' column in the 'employees' table for employees with an 'employee_id' of 1001:

```sql
UPDATE employees
SET salary = 60000
WHERE employee_id = 1001;
```

This query sets the 'salary' to 60000 for the employee with an 'employee_id' of 1001.

Remember to use the WHERE clause carefully to avoid unintended updates to your data. If omitted, the UPDATE command will modify all rows in the table that meet the specified conditions.



<br>

## Q.3 like operator in SQL.
The LIKE operator in SQL is used to search for a specified pattern in a column. It's commonly used in conjunction with the SELECT statement's WHERE clause to filter rows based on patterns rather than exact matches.

The basic syntax of the LIKE operator is as follows:

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern;
```

In the syntax:

- `column_name(s)` are the name(s) of the column(s) you want to retrieve.
- `table_name` is the name of the table from which you want to retrieve data.
- `column_name` is the name of the column you want to search.
- `pattern` is the pattern you want to search for. It can include wildcard characters:
  - `%` represents zero or more characters.
  - `_` represents a single character.

Here are a few examples of using the LIKE operator:

1. To find all customers whose names start with "J":

```sql
SELECT * 
FROM customers
WHERE name LIKE 'J%';
```

2. To find all products whose names contain "phone":

```sql
SELECT * 
FROM products
WHERE name LIKE '%phone%';
```

3. To find all email addresses from a specific domain:

```sql
SELECT * 
FROM contacts
WHERE email LIKE '%@example.com';
```

These are just a few examples of how you can use the LIKE operator to perform pattern matching in SQL queries.


<br> 

## Q.4 What is the difference between WHERE clause and HAVING clause in SQL? 
The WHERE clause and the HAVING clause are both used in SQL queries to filter rows, but they operate in different contexts:

1. **WHERE Clause:**
   - The WHERE clause is used to filter rows before any groupings are made. It is typically used with the SELECT, UPDATE, or DELETE statements.
   - It filters rows based on individual row values, typically using comparisons, such as equalities, inequalities, or range checks.
   - The WHERE clause is applied to individual rows in the result set.
   - It cannot be used with aggregate functions like COUNT(), SUM(), AVG(), etc., because those functions operate on groups of rows.

   Example:
   ```sql
   SELECT * FROM employees WHERE department = 'Sales';
   ```

2. **HAVING Clause:**
   - The HAVING clause is used to filter rows after groups have been created using the GROUP BY clause. It is only used in conjunction with the GROUP BY clause.
   - It filters rows based on aggregated values, such as the result of applying aggregate functions (e.g., COUNT(), SUM(), AVG(), etc.) to groups of rows.
   - The HAVING clause is applied to groups of rows, not individual rows.
   - It can be used to filter groups based on conditions involving aggregated values.

   Example:
   ```sql
   SELECT department, AVG(salary) AS avg_salary 
   FROM employees 
   GROUP BY department 
   HAVING AVG(salary) > 50000;
   ```

In summary, the WHERE clause is used to filter individual rows based on specific conditions, whereas the HAVING clause is used to filter groups of 
rows after aggregation has been performed.



<br> 


## Q.5 TCL commands in SQL
In SQL, TCL (Transaction Control Language) commands are used to manage transactions within a database. These commands are responsible for defining the start and end of transactions, as well as controlling their outcomes. The main TCL commands include:

1. **COMMIT:** The COMMIT command is used to permanently save the changes made during the current transaction to the database. Once a COMMIT command is issued, the changes become permanent and visible to other transactions.

   Example:
   ```sql
   COMMIT;
   ```

2. **ROLLBACK:** The ROLLBACK command is used to undo the changes made during the current transaction and restore the database to its state before the transaction began. It is typically used to handle errors or cancel unwanted changes.

   Example:
   ```sql
   ROLLBACK;
   ```

3. **SAVEPOINT:** The SAVEPOINT command is used to set a point within a transaction to which you can later roll back. It allows you to create intermediate
4.  points within a transaction, enabling more granular control over rollbacks.

   Example:
   ```sql
   SAVEPOINT sp1;
   ```

5. **RELEASE SAVEPOINT:** The RELEASE SAVEPOINT command is used to remove a savepoint that was previously set within the current transaction. It releases the savepoint
6. and makes its identifier available for reuse.

   Example:
   ```sql
   RELEASE SAVEPOINT sp1;
   ```

7. **SET TRANSACTION:** The SET TRANSACTION command is used to set transaction characteristics such as isolation level, access mode, and other properties.
8. It allows you to control the behavior of transactions within a session.

   Example:
   ```sql
   SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
   ```

These TCL commands are crucial for ensuring data integrity, managing concurrent transactions, and controlling the behavior of transactions within a database.



<br> 

## Q.6 How should we sort data in SQL ? 
In SQL, you can sort data using the ORDER BY clause in your SELECT statement. The ORDER BY clause allows you to specify one or more columns by which you want the result set to be sorted. By default, sorting is done in ascending order (from lowest to highest value), but you can specify descending order as well.

Here's the basic syntax of the ORDER BY clause:

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC | DESC], column2 [ASC | DESC], ...;
```

In this syntax:

- `column1, column2, ...` are the columns you want to retrieve from the table.
- `table_name` is the name of the table from which you want to retrieve data.
- `ORDER BY` specifies the sorting order.
- `column1, column2, ...` are the columns by which you want to sort the result set.
- `ASC` (ascending) is the default sorting order if not specified explicitly.
- `DESC` (descending) sorts the result set in descending order.

Here are a few examples:

1. Sorting by a single column in ascending order:

```sql
SELECT * 
FROM employees 
ORDER BY last_name;
```

2. Sorting by a single column in descending order:

```sql
SELECT * 
FROM products 
ORDER BY price DESC;
```

3. Sorting by multiple columns:

```sql
SELECT * 
FROM customers 
ORDER BY country, city;
```

In this last example, the result set is first sorted by the country column in ascending order. Within each country, the rows are further sorted by the city column in ascending order.

The ORDER BY clause is very flexible and allows you to sort data in various ways to meet your specific requirements.

<br> 


## Q.7 What is NORMALIZATION and DENORMALIZATION ?


## Q.8 Explain 1NF, 2NF and 3NF in mysql normalization.

## Q.9 What is Primary key and Foreign Key? 

## Q.10 Difference between Primary and Foreign key? 

## Q.11 Primary key vs Candidate key vs Unique key

## Q.12 What is trigger? How you can create trigger in MySQL? 

## Q.13 Explain TRANSACTIONS and how to implement it in MySQL? 

## Q.14 What is index ? How can an index be declared in MySQL ? 

## Q.15 What is view ? How can you create and drop view in MySQL? 

## Q.16 Explain Join?  ( Inner , Left, Right, cross ) 

## Q.17 Union vs Union all

## Q.18 What are MySQL aliases ? 

## Q.19 Explain MySQL subqueryy .

## Q.20 Blob vs text data type in MySQL.


## Q.21 Char vs Varchar in data types .


## Q.22 What are the differences between InnoDB and MyISAM engines ? 


## Q.23 What are some of the common MySQL commands ? 

## Q.24 What are aggregate functions in MySQL ? 


## Q.25 What is DDL, DQL, DML, DCL and TCL Commands?


