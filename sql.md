# SQL

## Types of SQL Databases
PostgreSQL

SQLite

MySQL - runs as a server
* CLI
  * `mysql.server start`
  * `mysql.server stop`
  * Always comes with a root user

* npm Module

  * With Node: `require('mysql')`
  * .createConnnection()
    * Connects you to a specific mysql database
    * Takes in an object, with properties: host, user, password, database
  * chain `.connect()` after to connect
  * chain `.query()` after to enter SQL query
    * 1st param: a string with SQL query
    * 2nd param: callback which takes:
      * err
      * rows (data entries)
      * fields (columns)
  * chain `.end()` after to stop connection

```js
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'me',
  password : 'secret',
  database : 'my_db'
});

connection.connect();

connection.query('SELECT 1 + 1 AS solution', function(err, rows, fields) {
  if (err) throw err;

  console.log('The solution is: ', rows[0].solution);
});

connection.end();
```

## Basic SQL Commands

* ALTER TABLE: `ALTER TABLE table_name ADD column datatype;`
* AS: `SELECT column_name AS 'Alias'`
* AVG: average
* BETWEEN
* COUNT(): function that takes the name of a column as an argument and counts the number of rows where the column is not NULL.
* CREATE TABLE: `CREATE TABLE table_name (column_1 datatype, column_2 datatype, column_3 datatype);`
* GROUP BY
* INNER JOIN: will combine rows from different tables if the join condition is true for both tables.
* INSERT: `INSERT INTO table_name (column_1, column_2) VALUES (value_1, 'value_2');`
* LIMIT: `SELECT column_name(s) FROM table_name LIMIT number;`
* MAX(): function that takes the name of a column as an argument and returns the largest value in that column.
* MIN(): ditto for minimum value.
* OR
* ORDER BY
* OUTER JOIN: will combine rows from different tables even if the the join condition is not met.
  * LEFT JOIN: Every row in the left table is returned in the result set, and if the join condition is not met from the right table, then NULL values are used to fill in the columns.
  * RIGHT JOIN: ditto but for right.
* ROUND(): function that takes a column name and an integer as an argument. It rounds the values in the column to the number of decimal places specified by the integer.
* SELECT
* SELECT DISTINCT: returns only unique values in the specified column(s).
* SUM()
* UPDATE
* WHERE

## SQL Data Types

* CHARACTER(n): string, fixed-length n
* VARCHAR(n): string, variable length, max length n
* BOOLEAN
* INTEGER
* DECIMAL(p,s): precision p, scale s. Example: decimal(5,2) is a number that has 3 digits before the decimal and 2 digits after the decimal
* DATE:  Stores year, month, and day values
* TIME:  Stores hour, minute, and second values
* TIMESTAMP: Stores year, month, day, hour, minute, and second values




