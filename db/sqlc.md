# Devopssec
## databases
### SQL
#### D a t a T y p e s
- Exact Numeric’s:
  • INTEGER
  • SMALLINT
  • BIGINT
  • NUMERIC
  • DECIMAL
  Approximate Numeric’s:
  • REAL
  • DOUBLE PRECISION
  • FLOAT
  • DECFLOAT
-  Binary Strings:
   • BINARY
   • BINARY VARYING
   • BINARY LARGE OBJECT
   Boolean:
   Intervals:
   • INTERVAL DAY
   • INTERVAL YEAR
- Character Strings:
  • CHARACTER
  • CHARACTER VARYING (VARCHAR)
  • CHARACTER LARGE OBJECT
  • NATIONAL CHARACTER
  • NATIONAL CHARACTER VARYING
  • NATIONAL CHARACTER LARGE
  OBJECT
-  Date times:
   • DATE
   • TIME WITHOUT TIMEZONE
   • TIMESTAMP WITHOUT TIMEZONE
   • TIME WITH TIMEZONE
   • TIMESTAMP WITH TIMEZONE
   Collection Types:
   • ARRAY
   • MULTISET
   Other Types:
   • ROW
   • XML
#### QUERYING DATA FROM A TABLE
- SELECT It is used to specify which column to query. Use * for all
  FROM It is used to declare the table to select from
  WHERE It is used to define a condition
  = Used to compare a value with the given input
  LIKE
  It is a special operator used with WHERE to search for a   specific pattern from a column or row
  GROUP BY It is used to group identical data
  HAVING   It is used to specify that rows with aggregate values which   meets the specifies condition must be returned
  INNER JOIN   It is used to return all rows where key records of one table   is same as that of the other table
  LEFT JOIN   It is used to return all rows from the left table with the   matching rows in the right table
  RIGHT JOIN   It is used to return all rows from right table with the   matching rows in the left table
  FULL OUTER   JOIN   It is used to return rows that match either in the left or   right table
- SELECT c1, c2 FROM t;
  Query data in columns c1, c2 from a table
  SELECT * FROM t;
  Query all rows and columns from a table
  SELECT c1, c2 FROM t
  WHERE condition;
  Query data and filter rows with a condition
  SELECT DISTINCT c1 FROM t
  WHERE condition;
  Query distinct rows from a table
- SELECT c1, c2 FROM t
  ORDER BY c1 ASC [DESC];
  Sort the result set in ascending or descending
  order
- SELECT c1, c2 FROM t
  ORDER BY c1
  LIMIT n OFFSET offset;
  Skip offset of rows and return the next n rows
- SELECT c1, aggregate(c2)
  FROM t
  GROUP BY c1;
  Group rows using an aggregate function
  SELECT c1, aggregate(c2)
  FROM t
  GROUP BY c1
  HAVING condition;
  Filter groups using HAVING clause
#### QUERYING FROM MULTIPLE TABLES
- SELECT c1, c2
  FROM t1
  INNER JOIN t2 ON condition;
  Inner join t1 and t2
  SELECT c1, c2
  FROM t1
  LEFT JOIN t2 ON condition;
  Left join t1 and t1
  SELECT c1, c2
  FROM t1
  FULL OUTER JOIN t2 ON condition;
  Perform full outer join
- SELECT c1, c2
  FROM t1
  CROSS JOIN t2;
  Produce a Cartesian product of rows in tables
  SELECT c1, c2
  FROM t1 A
  INNER JOIN t2 B ON condition;
  Join t1 to itself using INNER JOIN clause
  SELECT c1, c2
  FROM t1
  RIGHT JOIN t2 ON condition;
  Right join t1 and t2
- SELECT c1, c2
  FROM t1, t2;
  Another way to perform cross join
#### USING SQL OPERATORS
- SELECT c1, c2 FROM t1
  UNION [ALL]
  SELECT c1, c2 FROM t2;
  Combine rows from two queries
  SELECT c1, c2 FROM t1
  INTERSECT
  SELECT c1, c2 FROM t2;
  Return the intersection of two queries
-  SELECT c1, c2 FROM t1
   MINUS
   SELECT c1, c2 FROM t2;
   Subtract a result set from another result set
   SELECT c1, c2 FROM t1
   WHERE c1 [NOT] LIKE pattern;
   Query rows using pattern matching %, _
   SELECT c1, c2 FROM t
   WHERE c1 [NOT] IN value_list;
   Query rows in a list
-  SELECT c1, c2 FROM t
   WHERE c1 BETWEEN low AND high;
   Query rows between two values
   SELECT c1, c2 FROM t
   WHERE c1 IS [NOT] NULL;
   Check if values in a table is NULL or not
#### MANAGING TABLES
- CREATE TABLE t (
  id INT PRIMARY KEY,
  name VARCHAR NOT NULL,
  price INT DEFAULT 0
  );
  Create a new table with three columns
- DROP TABLE t ;
  Delete the table from the database
  ALTER TABLE t ADD column;
  Add a new column to the table
  ALTER TABLE t DROP COLUMN c ;
  Drop column c from the table
- ALTER TABLE t ADD constraint;
  Add a constraint
  ALTER TABLE t DROP constraint;
  Drop a constraint
- ALTER TABLE t1 RENAME c1 TO c2 ;
  Rename column c1 to c2
  TRUNCATE TABLE t;
  Remove all data in a table
#### USING SQL CONSTRAINTS
- CREATE TABLE t(
  c1 INT, c2 INT, c3 VARCHAR,
  PRIMARY KEY (c1,c2)
  );
  Set c1 and c2 as a primary key
- CREATE TABLE t1(
  c1 INT PRIMARY KEY,
  c2 INT,
  FOREIGN KEY (c2) REFERENCES t2(c2)
  );
  Set c2 column as a foreign key
- CREATE TABLE t(
  c1 INT, c1 INT,
  UNIQUE(c2,c3)
  );
  Make the values in c1 and c2 unique
- CREATE TABLE t(
  c1 INT, c2 INT,
  CHECK(c1> 0 AND c1 >= c2)
  );
  Ensure c1 > 0 and values in c1 >= c2
- CREATE TABLE t(
  c1 INT PRIMARY KEY,
  c2 VARCHAR NOT NULL
  );
  Set values in c2 column not NULL
#### MODIFYING DATA
- INSERT INTO t(column_list)
  VALUES(value_list);
  Insert one row into a table
  INSERT INTO t(column_list)
  VALUES (value_list),
  (value_list), ….;
  Insert multiple rows into a table
  INSERT INTO t1(column_list)
  SELECT column_list
  FROM t2;
  Insert rows from t2 into t1
- UPDATE t
  SET c1 = new_value;
  Update new value in the column c1 for all rows
- UPDATE t
  SET c1 = new_value,
  c2 = new_value
  WHERE condition;
  Update values in the column c1, c2 that match
  the condition
  DELETE FROM t;
  Delete all data in a table
  DELETE FROM t
  WHERE condition;
  Delete subset of rows in a table
#### MANAGING VIEWS
- CREATE VIEW v(c1,c2)
  AS
  SELECT c1, c2
  FROM t;
  Create a new view that consists of c1 and c2
- CREATE VIEW v(c1,c2)
  AS
  SELECT c1, c2
  FROM t;
  WITH [CASCADED | LOCAL] CHECK OPTION;
  Create a new view with check option
- CREATE RECURSIVE VIEW v
  AS
  select-statement -- anchor part
  UNION [ALL]
  select-statement; -- recursive part
  Create a recursive view
- CREATE TEMPORARY VIEW v
  AS
  SELECT c1, c2
  FROM t;
  Create a temporary view
- DROP VIEW view_name
  Delete a view
#### MANAGING INDEXES
- CREATE INDEX idx_name
  ON t(c1,c2);
  Create an index on c1 and c2 of the table t
- CREATE UNIQUE INDEX idx_name
  ON t(c3,c4);
  Create a unique index on c3, c4 of the table t
- DROP INDEX idx_name;
  Drop an index
#### SQL AGGREGATE FUNCTIONS
- AVG returns the average of a list
- COUNT returns the number of elements of a list
  SUM returns the total of a list
  MAX returns the maximum value in a list
  MIN returns the minimum value in a list
- TO_DATE It is used to convert a string to date.
  COALESCE   Returns the first non NULL results, when querying with the   columns that contain NULL
  CURRENT_TIME  STAMP  Returns the correct time on the database server
  LISTAGG   It is used to transform values from a group of rows into a   delimited string
-
#### MANAGING TRIGGERS
- CREATE OR MODIFY TRIGGER trigger_name
  WHEN EVENT
  ON table_name TRIGGER_TYPE
  EXECUTE stored_procedure;
  Create or modify a trigger
- WHEN
  • BEFORE – invoke before the event occurs
  • AFTER – invoke after the event occurs
- EVENT
  • INSERT – invoke for INSERT
  • UPDATE – invoke for UPDATE
  • DELETE – invoke for DELETE
- TRIGGER_TYPE
  • FOR EACH ROW
  • FOR EACH STATEMENT
- CREATE TRIGGER before_insert_person
  BEFORE INSERT
  ON person FOR EACH ROW
  EXECUTE stored_procedure;
  Create a trigger invoked before a new row is
  inserted into the person table
- DROP TRIGGER trigger_name
  Delete a specific trigger


#### part 7
SQL Vs MySQL – Difference Between SQL and MySQL
- Difference Between SQL and MySQL
  There are times when people get confused between what is SQL and what is MySQL. So let us look at the primary difference between SQL and MySQL.

- Key Category	SQL	MySQL
  Developers/Owners	SQL is developed by Microsoft Corporation.	MySQL was developed by MySQL AB but is currently acquired and owned by Oracle Corporation.
  Function	SQL is a structured query language used for managing and retrieving data from the database system	MySQL is a Relational database system that uses SQL to query data from the databases.
  Syntax and Format	The syntax and format are fixed, declarative, and easy to use.
  Start with the clause and end with a semicolon.	MySQL is software and not a programming language, hence it does not have any commands or particular format.

- There are, however, the latest updates and versions of MySQL for enhanced performance.
  Licensing/Availability	SQL is proprietary based software owned by Microsoft and not open to others for free.	MySQL is an open-source free platform that allows access to any and everyone.
  Platform Support	SQL was built for WIndows, works partially for Linux, macOS with its latest versions.	MySQL is adaptable for cross-platforms, working well for Linux, macOS, Windows.
  Language Support	SQL is in itself a programming language used for database systems.	MySQL supports all the basic programming languages like C, C++, Perl, PHP, Python, Ruby, and many others.
  Storage Engine	SQL supports only a single storage engine for different operations	MySQL supports different storage engines and does not take up a lot of space for different functions and operations. It also enables the plugin storage engine as well.
  Data Security	SQL servers are secured as no third party or outsiders are allowed to manipulate data.	MySQL is susceptible to more security threats due to its open-source nature. It gives access to data manipulation and modification to unauthorized users as well during the run-time.
  Server and Database	In SQL, the server and database work independently. This allows users or interested parties to work on databases even during recovery sessions.	MySQL servers do not work independently from databases and hence, blocks the time for the users to do anything else.

- This function allows a lesser chance for data manipulation or corruption during the shifting of data into different versions of the software.
  Data Restoration	Time consumed for data restoration in SQL is less for a large amount of data.	In MySQL, the process of data restoration is quite time-consuming and requires a number of SQL statements for the same.
  Query Execution	SQL allows truncating a query even during execution without disabling the whole process.	MySQL does not allow you to cancel a query in the middle of execution. The user can cancel the query execution at the cost of stopping the entire process.
  Multilingual	SQL is available in different languages.	MySQL is available only in a single language that is English.
  Connector Support	SQL does not come up or support any connectors.	MySQL supports connectors like WorkBench Tool for building databases.
  Flexibility	SQL supports user-defined functions and XML.	MySQL does not support any user-defined function and XML.
  Community Support	The only support for SQL problems and queries is Microsoft Support care due to its highly protective usage.	MySQL has great community support as it allows free access.
  Advantages	– Interactive Language
  – Coding is not required
  – Portability
  – High Speed
  – Multiple Data Views	– Open-Source
  – Data Security
  – High Performance
  – Complete workflow Control

- Difference Between SQL and PLSQL
  SQL	PL/SQL
  It is a structured query language for databases.	It is a procedural language that is designed to implement SQL statements in a better way.
  The query executes a single operation at a time	Group of operations is performed in a single block
  SQL is declarative (program specifies what is to be done than how it is to be done)	PL/SQL is procedural (code that is written as a sequence of instructions)
  SQL is used in relational databases to execute various queries like create table, delete table, insert into table etc.	PL/SQL is used to write program blocks, procedures, functions, cursors, triggers, and packages
  SQL does not support data variables	PL/SQL provides support for variable constraints and data types
  Control structures are not supported	Control structures such as if-else, For loop, While loop are supported
  SQL is used to retrieve data from the database. We can modify data and table structure with SQL	PL/SQL is used to create web applications and server pages.
  It is possible to embed SQL in PLSQL syntax as PLSQL is an extension of SQL	Embedding PL/SQL in SQL syntax is not possible
  SQL directly interacts with the database server	PL/SQL does not directly interact with the database server
  Error handling feature is not present in SQL	PL/SQL handles errors and exceptions effectively with the help of the inbuilt exception handlers.
  Handling a large chunk of data can’t be effectively achieved by SQL	PL/SQL handles a large chunk of data effectively with the help of procedures, functions and triggers.
  SQL provides lesser processing speed	PL/SQL offers a high processing speed
  Execution of statements in SQL does not result in reduced traffic as multiple statements cannot get executed at the same time. The queries are executed one at a time which increases the network traffic.	Execution of operation results in reduced network traffic as a block of statements are executed at once
  SQL is easy to use and understand	Certain concepts of PL/SQL can be complex and prior knowledge might be necessary
  SQL does not support I/O operations	PL/SQL supports I/O operations as it can accept inputs and then store and process it.

- PostgreSQL vs MySQL: Difference You Need To Know
- Key differences
  MySQL is a Relational Database Management System (RDBMS) and PostgreSQL is an object-relational Database Management System (ORDBMS). In Relational Database Models, the database is represented as a collection of relations. An ORDBMS has qualities of an RDBMS and in addition to that, it has several features of object-oriented management systems like objects, classes, and inheritance.
  PostgreSQL is ACID (Atomicity Consistency Isolation Durability) compliant while MySQL is not ACID-compliant. MySQL is ACID-compliant only with InnoDB (an ACID-compliant storage engine for MySQL) and NDB (Network Database) cluster engines.
  PostgreSQL has Multi-Version Concurrency Control (MVCC) which enables multiple users to work on a PostgreSQL database simultaneously. MySQL provides MVCC support only after using InnoDB.
  MySQL provides MySQL Workbench as a GUI tool, PostgreSQL provides PgAdmin.
  MySQL only supports standard data types (string, numeric, date, and time) while PostgreSQL supports advanced data types such as arrays, hstore, and user-defined data types.
  PostgreSQL vs MySQL
  Now that we know the basic features and characteristics of PostgreSQL and MySQL, we are in a position to explore the topic MySQL vs PostgreSQL.

- MySQL	PostgreSQL
  It is a Relational Database Management System.	It is an Object-Relational Database Management System.
  MySQL was developed by a Swedish company called MySQL AB in 1995.	PostgreSQL was developed by the Department of Computer Science, University of California.
  MySQL is not completely ACID compliant. It supports ACID only when used in InnoDB and NDB.	PostgreSQL is completely ACID compliant.
  MySQL is simple, reliable, and faster.	PostgreSQL is complex and slower.
  MySQL is easy to troubleshoot as it has a nice and devoted community ready to help.	PostgreSQL is not easy to troubleshoot.
  Users cannot be assigned object-level privileges.	Users can be assigned object-level privileges.
  Only partially SQL compliant.	PostgreSQL is fully SQL compliant.
  It is licensed under GNU GPU	It is licensed under MIT style.
  It is written in C/C++.	It is written in C.
  MySQL is best suited for simple operations like read and write.	PostgreSQL is generally used for large and complex operations.
  MySQL supports standard data types like string, numeric, and date and time, etc.	PostgreSQL supports standard data types and in addition to these data types, PostgreSQL also supports advanced data types such as arrays, hstore, and user-defined data types.
  It does not provide materialized views. A materialized view is a pre-computed query result that can be used later.	It provides materialized views.
  It does not provide table inheritance.	It provides table inheritance.
  Join capabilities in MySQL are limited.	PostgreSQL has a number of join capabilities like inner join, right join, left join, cross join, full outer join, natural join, and self join.
  MySQL does not provide support for MVCC.	MVCC is one of the most important reasons companies choose PostgreSQL. It handles concurrency better than MySQL.
  MySQL has a multilayer structure having a set of storage engines.	PostgreSQL is a unified database storage server and has a single storage engine.
  MySQL provides a workbench as a user interface.	PostgreSQL provides PgAdmin as a user interface.
  Every connection created in MySQL is an Operating System (OS) thread.	Every connection created in PostgreSQL is an Operating System (OS) process.
  It has native Server Sockets Layer (SSL) support. SSL is a security protocol that creates a secure encrypted link between a web server and a web browser.	It has native Transport Layer Security (TLS) support. TLS is an improved version of SSL.
  It does not support partial, bitmap, or expression indexes.	PostgreSQL supports all of these.
  Replication in MySQL is one-way asynchronous replication where one server is used as primary and others as replicas.	Replication in PostgreSQL is synchronous replication where the master database is synchronized with the slave database. It utilizes two database instances running simultaneously.
  Companies that use MySQL:
  Facebook, Tesla, YouTube, Airbnb, NASA	Companies that use PostgreSQL:
  Apple, Cisco, Netflix, Reddit, Spotify, Fujitsu

- SQL Vs NoSQL: Difference Between SQL and NoSQL
- Features of SQL
  Provide High-Performance Capabilities
  SQL is a powerful tool as it is highly compatible with all types of RDBMS like MySQL, SQL Server, Oracle Database, MS Access, etc.
  Data Consistency: SQL adheres to ACID properties with a strict schema that ensures better data consistency.
  Ensures Vertical Scalability
  Handle Large Transactions with efficiency
  Robust Security Measures like rigid schema, data consistency, data integrity, regular updates, etc.
  Suitable for every type of organization – large or small.
  SQL is easy to learn and manage
  Open Source Programming Language
  Supports Data Definition Language and Data Manipulation Language to query the databases
- Features of NoSQL
  NoSQL has higher scalability than other database management systems
  Schema Free: You do not need to define the schema of the database before storing the data onto the system.
  NoSQL allows the distribution of data on more than just one device.
  With NoSQL Database, you do not require specialized or complex hardware or storage solutions.
  Does not require data normalization
  Simple API for easy user interfaces
  Can store unstructured, semi-structured, or structured data.

- SQL vs NoSQL: Head to Head Comparison
  Parameter	SQL	NoSQL
  Define	SQL databases are a type of system software that supports management, analysis, capturing and querying the structured data in a relational format.	NoSQL databases are a type of software that allows to maintain and retrieve structured, unstructured, polymorphic data for different purposes.
  Purpose	A language used to communicate with databases for storage, deletion, updation, insertion and retrieval of data.	A software to retrieve, store and manage scalability of databases.
  Development Year	SQL was developed in the year 1970 for flat file storage problems.	NoSQL was developed in 2000 as an enhanced version for SQL databases for unstructured and semi-structured data.
  Query Language	SQL databases support Structured Query Languages.	NonSQL does not have any declarative query language.
  Type	Supports table based data type.	Supports document oriented, graph databases, key value pair-based.
  Scalability	Vertically Scalable  (Add resources to increase the capacity of the existing hardware and software).	Horizontally Scalable (Changing small nodes with larger nodes to increase the capacity of the existing hardware and software).
  Schemas	SQL supports predefined schemas, making the storage of data restrictive to structured type only.	Nosql supports dynamic schemas to store different forms of data.
  Architecture	SQL is relational.	Non-SQL is non relational.
  Ideal Use Cases	SQL is best suitable for complex queries, multi-row transactions.	NoSQL is best suited for unstructured data or documents. Not ideal for complex queries.
  Hardware	Databases that support SQL require powerful hardware to support vertical scaling.	NonSQL databases require commodity hardware for horizontal scaling.
  Properties	SQL enables ACID(atomicity, consistency, isolation, and durability) properties	NonSQL follows CAP (consistency, availability, partition tolerance) properties.
  Data Storage	SQL does not support hierarchical storage of data.	NoSQL is best suited for hierarchical storage of data.
  Distributed Data	SQL databases can only be run on a single system and hence, does not follow distribution of data.	NoSQL databases are designed to follow data distribution features like repetition, partition.
  Best Features	• Secure
  • Cross Platform Support
  • Free	• High Performance
  • Flexible
  • Easy to use
  Top Companies Using	Microsoft, Dell, Cognizant, etc.	Amazon, Capgemini, Adobe, etc.
  Examples	SQL supports databases like MySQL, SQL Server, Oracle, etc.	Nosql databases are Hbase, MongoDB, Redis, etc.

- Pros/Advantages of SQL
  Coding
  No prior knowledge of extensive coding is needed. SQL is simple and easy to learn with declarative commands.

Portability
SQL is highly portable and can be run on Laptops, Mainframes, PC’s, tablets or smartphones, etc.

Open-source
SQL is an open-source product that ensures a stronger community for development and assistance in this domain.

Interactive Language
SQL is an interactive language which means it is easy to learn and quite efficient in working with complex queries. Programmers prefer this language as data retrieval in SQL is rapid.

Defined standards
SQL standards are well defined as they were foremostly used by ISO and ANSI.

Data Views
Allows multiple data views

SQL supports the client-server architecture completely.
High Demand
SQL is in high demand. Many top tier companies are using RDBMS and require administrators with proficiency in SQL skills. Companies like Micorosoft, Hootsuite, Cognizant, and many others  are using SQL databases.

- Cons/Drawbacks of SQL
  Complex Structure
  Access is difficult in SQL because of its complex structure.

Interfacing
The process of interfacing can get complicated in SQL as there is not much coding involved in writing SQL queries.

Limited
SQL demand and scaling are limited to particular projects and data types like you cannot use SQL to query unstructured or semi-structured data. It is fixated on a relational schema.

- Pros/Advantages of NoSQL
  Scale-Out Architecture
  NoSQL was designed in 2000 to cover the concerns faced in SQL. It is inevitable to stop the exponential growth of data and to manage that NoSQL provides a scale-out architecture. This technology will allow changing the data plane resources by adding more nodes to the cluster that ensure larger storage capacity and scalability of data.

Data Type Storage
NoSQL flexibility is its biggest advantage. Programmers are not limited to storing only structured data. The freedom from the predefined schema allows NoSQL databases to store and retrieve data easily. From structured data to loosely structured values like maps, strings, binary values etc, can all be stored and retrieved at ease by the data administrators.

Developer Friendly
There is not much hassle in storing and using data for creating applications in NoSQL. Programmers can store data “as it is” i.e., without converting the semi-structured data into a table format for retrieval and manipulation. This enables developers to adapt to structure and technology on their own.

Less Management
NoSQL databases are an enhanced version of a database management system and, thus, does not require a big team of data administrators to perform small tasks or to manage the system. In addition to this, the less complex structure of NoSQL makes it easier to handle and operate.

Big Data Applications
NoSQL databases have a large capacity to store massive volumes of data.

- Cons/Drawbacks of NoSQL
  ACID properties
  Unlike relational databases, NoSQL does not support ACID properties that limit it to provide reliability functions.

Query Language
NoSQL databases do not have any standard query language like SQL. It makes the process of data handling, retrieval, and management more complex and slower.

Different Data Models
NoSQL has different data models for storing and maintaining data like Key-value, document, column family,etc.  It hampers NoSQL to facilitate a single database for different purposes instead one has to operate with multiple databases and data models to perform all the niches. This makes the functioning complex, and increases the chances for less data consistency.

Huge Databases
Data quality and Data Duplication are two of the prime issues with NoSQL as it can store up to a massive amount of data without the ACID properties.
