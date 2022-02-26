# Devopssec
## databases
### MySQL
#### part 5
- Introduction to MySQL:

MySQL is an open-source relational database management system (RDBMS). It runs on the web as well as on the server. MySQL is fast, reliable, and easy to use. It is open-source software. MySQL uses standard SQL and compiles on a number of platforms. It is a multithreaded, multi-user SQL database management system.

The data in a MySQL database is stored in the form of tables. A table is a collection of related data, and it consists of columns and rows.

MySQL has stand-alone clients that allow users to interact directly with a MySQL database using SQL, but more often MySQL is used with other programs to implement applications that need relational database capability.
2. What are some of the advantages of using MySQL?
   Flexibility: MySQL runs on all operating systems
   Power: MySQL focuses on performance
   Enterprise-Level SQL Features: MySQL had for some time been lacking in advanced features such as subqueries, views, and stored procedures.
   Full-Text Indexing and Searching
   Query Caching: This helps enhance the speed of MySQL greatly
   Replication: One MySQL server can be duplicated on another, providing numerous advantages
   Configuration and Security
8. What are some of the common MySQL commands?
   Command	Action
   ALTER	To alter a database or table
   BACKUP	To back-up a table
   \c	To cancel Input
   CREATE	To create a database
   DELETE	To delete a row from a table
   DESCRIBE	To describe a table's columns
   DROP	To delete a database or table
   EXIT(ctrl+c)	To exit
   GRANT	To change user privileges
   HELP (\h, \?)	Display help
   INSERT	Insert data
   LOCK	Lock table(s)
   QUIT(\q)	Same as EXIT
   RENAME	Rename a Table
   SHOW	List details about an object
   SOURCE	Execute a file
   STATUS (\s)	Display the current status
   TRUNCATE	Empty a table
   UNLOCK	Unlock table(s)
   UPDATE	Update an existing record
   USE	Use a database

9. How do you create a database in MySQL?
   Use the following command to create a new database called ‘books’:

CREATE DATABASE books;

10. How do you create a table using MySQL?
    Use the following to create a table using MySQL:

CREATE TABLE history (
author VARCHAR(128),
title VARCHAR(128),
type VARCHAR(16),
year CHAR(4)) ENGINE InnoDB;
11. How do you Insert Data Into MySQL?
    The INSERT INTO statement is used to add new records to a MySQL table:

INSERT INTO table_name (column1, column2, column3,...)
VALUES (value1, value2, value3,...)
If we want to add values for all the columns of the table, we do not need to specify the column names in the SQL query. However, the order of the values should be in the same order as the columns in the table. The INSERT INTO syntax would be as follows:

INSERT INTO table_name
VALUES (value1, value2, value3, ...);
12. How do you remove a column from a database?
    You can remove a column by using the DROP keyword:

ALTER TABLE classics DROP pages;

13. How to create an Index in MySQL?
    In MySQL, there are different index types, such as a regular INDEX, a PRIMARY KEY, or a FULLTEXT index. You can achieve fast searches with the help of an index. Indexes speed up performance by either ordering the data on disk so it's quicker to find your result or, telling the SQL engine where to go to find your data.

Example: Adding indexes to the history table:

ALTER TABLE history ADD INDEX(author(10));
ALTER TABLE history ADD INDEX(title(10));
ALTER TABLE history ADD INDEX(category(5));
ALTER TABLE history ADD INDEX(year);
DESCRIBE history;
14. How to Delete Data From a MySQL Table?
    In MySQL, the DELETE statement is used to delete records from a table:

DELETE FROM table_name
WHERE column_name = value_name
15. How do you view a database in MySQL?
    One can view all the databases on the MySQL server host using the following command:

mysql> SHOW DATABASES;

16. What are the Numeric Data Types in MySQL?
    MySQL has numeric data types for integer, fixed-point, floating-point, and bit values, as shown in the table below. Numeric types can be signed or unsigned, except BIT. A special attribute enables the automatic generation of sequential integer or floating-point column values, which is useful for applications that require a series of unique identification numbers.

- Type Name	Meaning
  TINYINT	Very Small Integer
  SMALLINT	Small Integer
  MEDIUMINT	Medium-sized Integer
  INT	Standard Integer
  BIGINT	Large Integer
  DECIMAL	Fixed-point number
  FLOAT	Single-precision floating-point number
  DOUBLE	Double-precision floating-point number
  BIT	Bit-field

17. What are the String Data Types in MySQL?
    Type Name	Meaning
    CHAR	fixed-length nonbinary(character) string
    VARCHAR	variable-length nonbinary string
    BINARY	fixed-length binary string
    VARBINARY	variable-length binary string
    TINYBLOB	Very small BLOB(binary large object)
    BLOB	Small BLOB
    MEDIUMBLOB	Medium-sized BLOB
    LONGBLOB	Large BLOB
    TINYTEXT	A very small nonbinary string
    TEXT	Small nonbinary string
    MEDIUMTEXT	Medium-sized nonbinary string
    LONGTEXT	Large nonbinary string
    ENUM	An enumeration; each column value is assigned, one enumeration member
    SET	A set; each column value is assigned zero or more set members
    NULL	NULL in SQL is the term used to represent a missing value. A NULL value in a table is a value in a field that appears to be blank. This value is different than a zero value or a field that contains spaces.

18. What are the Temporal Data Types in MySQL?
    Type Name	Meaning
    DATE	A date value, in ' CCYY-MM-DD ' Format
    TIME	A Time value, in ' hh : mm :ss ' format
    DATETIME	Date and time value, in ' CCYY-MM-DD hh : mm :ss ' format
    TIMESTAMP	A timestamp value, in ' CCYY-MM-DD hh : mm :ss ' format
    YEAR	A year value, in CCYY or YY format
    Example: To select the records with an Order Date of "2018-11-11" from a table:

SELECT * FROM Orders WHERE OrderDate='2018-11-11'
19. What is BLOB in MySQL?
    BLOB is an acronym that stands for a binary large object. It is used to hold a variable amount of data.
    There are four types of BLOB:

TINYBLOB
BLOB
MEDIUMBLOB
LONGBLOB
A BLOB can hold a very large amount of data. For example - documents, images, and even videos. You could store your complete novel as a file in a BLOB if needed
20. How to add users in MySQL?
    You can add a User by using the CREATE command and specifying the necessary credentials. For example:

CREATE USER ‘testuser’ IDENTIFIED BY ‘sample password’;

21. What are MySQL “Views”?
    In MySQL, a view consists of a set of rows that is returned if a particular query is executed. This is also known as a ‘virtual table’. Views make it easy to retrieve the way of making the query available via an alias.
    The advantages of views are:

Simplicity
Security
Maintainability
22. How do you create and execute views in MySQL?
    Creating a view is accomplished with the CREATE VIEW statement. As an example:

CREATE
[OR REPLACE]
[ALGORITHM = {MERGE | TEMPTABLE | UNDEFINED }]
[DEFINER = { user | CURRENT_USER }]
[SQL SECURITY { DEFINER | INVOKER }]
VIEW view_name [(column_list)]
AS select_statement
[WITH [CASCADED | LOCAL] CHECK OPTION]
23. What are MySQL Triggers?
    A trigger is a task that executes in response to some predefined database event, such as after a new row is added to a particular table. Specifically, this event involves inserting, modifying, or deleting table data, and the task can occur either prior to or immediately following any such event.
    Triggers have many purposes, including:

Audit Trails
Validation
Referential integrity enforcement

24. How many Triggers are possible in MySQL?
    There are six Triggers allowed to use in the MySQL database:

Before Insert
After Insert
Before Update
After Update
Before Delete
After Delete
25. What is the MySQL server?
    The server, mysqld, is the hub of a MySQL installation; it performs all manipulation of databases and tables.

26. What are the MySQL clients and utilities?
    Several MySQL programs are available to help you communicate with the server. For administrative tasks, some of the most important ones are listed here:

• mysql—An interactive program that enables you to send SQL statements to the server and to view the results. You can also use mysql to execute batch scripts (text files containing SQL statements).

• mysqladmin—An administrative program for performing tasks such as shutting down the server, checking its configuration, or monitoring its status if it appears not to be functioning properly.

• mysqldump—A tool for backing up your databases or copying databases to another server.

• mysqlcheck and myisamchk—Programs that help you perform table checking, analysis, and optimization, as well as repairs if tables become damaged. mysqlcheck works with MyISAM tables and to some extent with tables for other storage engines. myisamchk is for use only with MyISAM tables

27. What are the types of relationships used in MySQL?
    There are three categories of relationships in MySQL:

One-to-One: Usually, when two items have a one-to-one relationship, you just include them as columns in the same table.
One-to-Many: One-to-many (or many-to-one) relationships occur when one row in one table is linked to many rows in another table.
Many-to-Many: In a many-to-many relationship, many rows in one table are linked to many rows in another table. To create this relationship, add a third table containing the same key column from each of the other tables

28. Can you explain the logical architecture of MySQL?
    The top layer contains the services most network-based client/server tools or servers need such as connection handling, authentication, security, and so forth.
    The second layer contains much of MySQL’s brains. This has the code for query parsing, analysis, optimization, caching, and all the built-in functions.

The third layer contains the storage engines that are responsible for storing and retrieving the data stored in MySQL
29. What is Scaling in MySQL?
    In MySQL, scaling capacity is actually the ability to handle the load, and it’s useful to think of load from several different angles such as:

Quantity of data
Number of users
User activity
Size of related datasets
30. What is Sharding in SQL?
    The process of breaking up large tables into smaller chunks (called shards) that are spread across multiple servers is called Sharding.
    The advantage of Sharding is that since the sharded database is generally much smaller than the original; queries, maintenance, and all other tasks are much faster.

31. What are Transaction Storage Engines in MySQL?
    To be able to use MySQL’s transaction facility, you have to be using MySQL’s InnoDB storage engine (which is the default from version 5.5 onward). If you are not sure which version of MySQL your code will be running on, rather than assuming InnoDB is the default engine you can force its use when creating a table, as follows


