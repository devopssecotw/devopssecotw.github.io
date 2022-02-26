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
#### 

### Oracle CS
#### INSERT
- INSERT INTO PROPERTIES_DESC (ID,NAME,DESCRIPTION,IS_ACTIVE) VALUES(SEQ.nextval,'app.login.key','login key','T');
- INSERT INTO table (column1, column2, ... column_n ) SELECT expression1, expression2, ... expression_n FROM source_table [WHERE conditions];
#### SELECT
- select pubs1.nextval from dual;
- SELECT name,address,phone_number INTO v_employee_name,v_employee_address,v_employee_phone_number 
  FROM employee WHERE employee_id = 6;
- SELECT ROUND(
  SUM(Q1."Data Files" +
  Q2."Temp Files" +
  Q3."Redo Logs" +
  Q4."Control Files"
  )/1024/1024/1024,  2)
  AS "Total Size (GB)"
  FROM
  (SELECT SUM(bytes) "Data Files" from DBA_DATA_FILES) Q1,
  (SELECT SUM(bytes) "Temp Files" from DBA_TEMP_FILES) Q2,
  (SELECT SUM(bytes) "Redo Logs" from V_$LOG) Q3,
  (SELECT SUM(BLOCK_SIZE * FILE_SIZE_BLKS)"Control Files" FROM V$CONTROLFILE) Q4;  check the size of the database including, its Data files, Temporary files, Redo logs and Control files, run the following command
- SELECT USERNAME, ACCOUNT_STATUS, PROFILE FROM DBA_USERS;
- SELECT * FROM DBA_TAB_PRIVS WHERE GRANTEE='USERNAME';
  view all privileges granted to a user on other users table
- SELECT column1, column2 FROM student
  ORDER BY column1 ASC [DESC];
- SELECT column1, column2
  FROM table1
  INNER JOIN table2 ON condition;

#### functions
##### Aggregate Functions 
- AVG ( [DISTINCT|ALL] expression ) [OVER (
  analytic_clause )]
  COUNT ( [ * | [ DISTINCT | ALL ] expression) [OVER
  (analytic_clause)]
  MAX ( [DISTINCT|ALL] expression ) [OVER
  (analytic_clause)]
  MIN ( [DISTINCT|ALL] expression ) [OVER (
  analytic_clause )]
  SUM ( [DISTINCT|ALL] expression ) [OVER
  (analytic_clause)]
##### Conversion Functions
- BIN_TO_NUM ( expression_list )
  CAST ( expression AS type_name )
  CAST ( MULTISET (subquery) AS type_name )
  COALESCE ( expr1, expr2, [expr…] )
  CHARTOROWID ( input_char )
  FROM_TZ ( timestamp_value, timezone_value )
  HEXTORAW ( charvalue )
  NUMTODSINTERVAL ( number, interval_unit )
  NUMTOYMINTERVAL ( number, interval_unit )
  RAWTOHEX ( charvalue )
  RAWTONHEX ( raw )
-  ROWIDTOCHAR ( rowid )
  ROWIDTONCHAR ( rowid )
  SCN_TO_TIMESTAMP ( number )
  TIMESTAMP_TO_SCN ( timestamp )
  TO_BINARY_DOUBLE ( expression [, format [,
  nlsparam ] ] )
  TO_CHAR( input_value, [format_mask],
  [nls_parameter] )
  TO_CLOB ( input_string )
  TO_DATE( charvalue, [format_mask],
  [nls_date_language] )
  TO_DSINTERVAL ( input_string [, nlsparam] )
-  TO_LOB ( long_value )
  TO_MULTI_BYTE ( string )
  TO_NCHAR ( input_string )
  TO_NCHAR ( input_datetime [, format [,nlsparam ] ] )
  TO_NCHAR ( number [, format [, nlsparam ] ] )
  TO_NCLOB ( lob_value )
  TO_NUMBER ( input_value, [format_mask],
  [nls_parameter] )
  TO_SINGLE_BYTE ( input_string )
  TO_TIMESTAMP ( input_string, [format_mask],
  [‘nlsparam’] )
-  TO_TIMESTAMP_TZ ( input_string [, format_mask] [,
  nls_param] )
  TO_YMINTERVAL ( input_string )
  UNISTR ( string )

##### Date and Time Functions
- ADD_MONTHS ( input_date, number_months )
  CURRENT_DATE
  CURRENT_TIMESTAMP ( [precision] )
  DBTIMEZONE
  LAST_DAY ( input_date )
  LOCALTIMESTAMP ( timestamp_precision )
  MONTHS_BETWEEN ( date1, date2 )
  NEW_TIME ( input_date, timezone1, timezone2 )
  NEXT_DAY ( input_date, weekday )
  SESSIONTIMEZONE
  SYS_EXTRACT_UTC (
  datetime_with_timezone_value )
  SYSDATE
  SYSTIMESTAMP
  TZ_OFFSET ( timezone_name | time_value |
  SESSIONTIMEZONE | DBTIMEZONE )
##### Environment Functions
- CON_DBID_TO_ID ( container_dbid )
  CON_GUID_TO_ID ( container_guid )
  CON_NAME_TO_ID ( container_name )
  CON_UID_TO_ID ( container_uid )
  ORA_INVOKING_USER
  ORA_INVOKING_USERID ( )
  SYS_CONTEXT (namespace, parameter [, length] )
  SYS_GUID()
  SYS_TYPEID ( object_type_value )
  UID
  USER
  USERENV ( parameter )
  SQLCODE
  SQLERRM ( error_number )
##### NLS Functions National Language Support
- NLS_CHARSET_DECL_LEN ( byte_count,
  char_set_id )
  NLS_CHARSET_ID ( string_value )
  NLS_CHARSET_NAME ( number )

##### Numeric and Maths Functions
- ABS ( number )
  ACOS ( number )
  ASIN ( number )
  ATAN2 ( number1 [/|,] number2 )
  BITAND ( expr1, expr2 )
  CEIL ( input_val )
  CORR ( expression1, expression2 )
  COS ( number )
  COSH (number)
-  COVAR_POP ( expression1, expression2 ) [OVER  (analytic_clause)]
  COVAR_SAMP ( expression1, expression2 ) [OVER  (analytic_clause)]
  CUME_DIST (expression1, … expression_n) WITHIN
  GROUP (ORDER BY expression_order1, …  expression_order_n)
  CUME_DIST() OVER ( [query_partition_clause]
  ORDER BY order_clause )
  DENSE_RANK ( expr, [expr(n)] ) WITHIN GROUP (  ORDER BY (order_expr [ASC|DESC] [NULLS  FIRST|LAST] )
  DENSE_RANK() OVER ( [query_partition_clause]
  order_by_clause)
  EXP ( number )
  EXTRACT ( date_component FROM expression )
  FLOOR ( input_number )
  GREATEST ( expr1, [expr_n] )
  LEAST ( expr1, [expr_n] )
-  LN ( number )
  LOG ( [base, ] expression )
  MEDIAN ( expr ) [OVER (query_partition_clause)]
  MOD ( numerator, denominator )
  ORA_HASH ( expression [, max_bucket [,  seed_value ] ] )
  PERCENT_RANK ( expression ) WITHIN GROUP (  ORDER BY (expression_n [. DESC | ASC ] [NULLS  FIRST|LAST] )
  PERCENT_RANK () OVER ( [query_partition_clause]  order_by_clause )
  PERCENTILE_CONT ( expression) WITHIN GROUP  ( ORDER BY expression [ ASC | DESC ] [OVER (  query_partition_clause )
  PERCENTILE_DISC ( expression) WITHIN GROUP (  ORDER BY expression [ ASC | DESC ] [OVER (  query_partition_clause )
  POWER ( n2, n1 )
  RANK ( expr ) WITHIN GROUP ( ORDER BY (
  order_expr [NULLS FIRST/LAST] ) )
  RANK () OVER ( [query_partition_clause]
  order_by_clause )
  REMAINDER ( n2, n1 )
  ROUND ( input, roundto )
  ROWNUM
  ROW_NUMBER () OVER ( [ query_partition_clause]  order_by_clause )
-  SIGN ( number )
  SIN ( number )
  SINH ( number )
  SQRT ( number )
  STANDARD_HASH ( expression [, method ] )
  STDDEV ( [DISTINCT | ALL] expression ) [OVER  (analytical_clause) ]
  STDDEV_POP ( expression) [ OVER (  analytic_clause ) ]
  STDDEV_SAMP ( expression) [ OVER (  analytic_clause ) ]
  TAN ( number )
  TANH ( number )
  TRUNC ( date, fmt )
  TRUNC ( number, decimals )
  VAR_POP ( expression) [OVER ( analytic_clause )]
  VAR_SAMP ( expression) [OVER ( analytic_clause )]
  VARIANCE ( [ DISTINCT | ALL ] expression) [ OVER  ( analytic_clause ) ]  WIDTH_BUCKET ( expression, min_value,  max_value, num_buckets )

##### String and Character Functions
- ASCII ( charvalue )
  ASCIISTR ( charvalue )
  CHR ( number_code [USING NCHAR_CS] )
  COMPOSE ( input_value )
  CONCAT( string1, string2 )
  CONVERT ( input_char, dest_char_set,  [source_char_set] )
  DECODE ( expression, search, result [, search,  result]… [,default] )
  DECOMPOSE ( input_string  [CANONICAL|COMPATIBILITY] )
  DUMP ( expression [, return_format] [, start_position]  [, length] )
- INITCAP ( input_string )
  INSTR ( string, substring, [start_position],  [occurrence] )
  INSTR2 ( string, substring, [start_position],  [occurrence] )
  INSTR4 ( string, substring, [start_position],  [occurrence] )
  INSTRB ( string, substring, [start_position],  [occurrence] )
  INSTRC ( string, substring, [start_position],  [occurrence] )
  LISTAGG ( measure_expr [, delimiter]) WITHIN  GROUP (order_by_clause) [OVER  query_partition_clause]
  LENGTH ( string_value )
  LENGTH2 ( string_value )
-  LENGTH4 ( string_value )
  LENGTHB ( string_value )
  LENGTHC ( string_value )
  LOWER ( input_string )
  LPAD( expr, length [, pad_expr] )
  LTRIM( input_string, [trim_string] )
  LNNVL ( condition )
  NCHR ( number_code )
  NLS_INITCAP ( input_char [, nlsparam ] )
  NLS_LOWER ( input_char [, nlsparam ] )
  NLS_UPPER ( input_char [, nlsparam ] )
  NLSSORT ( input_char [, nlsparam ] )
  NANVL ( check_value, replace_value )
-  NVL ( check_value, replace_value )
  NVL2 ( value_to_check, value_if_not_null,
  value_if_null )
  NULLIF ( expr1, expr2 )
  REGEXP_COUNT ( source_char, pattern [, position [,
  match_pattern [, subexpression ] ] ] )
  REGEXP_INSTR ( source_char, pattern [, position [,
  occurrence [, return_option [, match_pattern [,  subexpression ] ] ] ] ] )
  REGEXP_REPLACE ( source_char, pattern [,
  replace_string [, position [, occurrence [,  match_parameter ] ] ] ] )
  REGEXP_SUBSTR ( source_char, pattern [, position  [, occurrence [, match_parameter ] ] ] ] )
-  REPLACE ( whole_string, string_to_replace,  [replacement_string])
  RPAD ( expr, length [, pad_expr] )
  RTRIM ( input_string, [trim_character])
  SOUNDEX ( string )
  SUBSTR ( string, start_position, [length] )
  TRANSLATE ( source, from_string, to_string )
  TRANSLATE ( charvalue USING
  {CHAR_CS|NCHAR_CS} )
  TREAT ( expression AS [ REF ] [ schema. ] type )
  TRIM ( [ [ LEADING | TRAILING | BOTH ]
  trim_character FROM ] trim_source )
  UPPER ( input_string )
  VSIZE ( expression )
##### Analytic Functions
- FIRST_VALUE ( expression [ IGNORE NULLS ] )
  OVER ( analytic_clause )
  LAST_VALUE ( expression [ IGNORE NULLS ] )
  OVER ( analytic_clause )
  LAG ( expression [, offset [, default] ] ) OVER ( [  query_partition_clause ] order_by_clause )
  LEAD ( expression [, offset [, default] ] ) OVER ( [  query_partition_clause ] order_by_clause )
  NTILE ( expression ) OVER (  [query_partition_clause] order_by_clause )
  RATIO_TO_REPORT( expression ) OVER (  [query_partition_clause] )

##### Other Functions
- CASE [expression]
  WHEN condition_1 THEN result_1
  WHEN condition_n THEN result_n
  ELSE result
  END case_name
  SYS_CONNECT_BY_PATH ( column,
  character_separator )

##### Grouping Functions
- GROUP_ID ( )
  GROUPING ( expression )
  GROUPING_ID ( expression1 [, expression_n ] )
##### Large Object Functions
- BFILENAME ( directory, filename )
  EMPTY_BLOB ()
  EMPTY_CLOB ()

#### DELETE / drop
- DELETE FROM table_name WHERE some_column=some_value
- DROP INDEX index_name;
- drop database;
- DROP TABLE student;
- TRUNCATE TABLE student; Remove all data in a table
- DROP VIEW view-name;
#### UPDATE
- UPDATE customer SET name='Joe' WHERE customer_id=10 and paid > 0;
- ALTER SEQUENCE <sequence_name> INCREMENT BY <integer>;
- ALTER TABLE [table name]
  ADD ( [column name] [datatype], ... );
- ALTER TABLE [table name]
  MODIFY ( [column name] [new datatype] );
- ALTER TABLE [table name]
  DROP COLUMN [column name];
- ALTER TABLE student RENAME column1 TO column3;
- ALTER TABLE [table name]
  ADD CONSTRAINT [constraint name] UNIQUE( [column name] ) USING INDEX [index name];
- ALTER TABLE [table name]
  DROP CONSTRAINT [constraint name];
- ALTER INDEX index_name
  RENAME TO new_index_name;
- ALTER USER username IDENTIFIED BY password;
- 
#### Create
- CREATE SEQUENCE sequence_name MINVALUE value MAXVALUE value START WITH value INCREMENT BY value CACHE value;
- CREATE TABLE [table name]
  ( [column name] [datatype], ... );
- CREATE TABLE table_name
  (
  column1 datatype null/not null,
  column2 datatype null/not null,
  ...
  CONSTRAINT constraint_name CHECK (column_name condition) [DISABLE],
  CONSTRAINT constraint_name UNIQUE (column1, column2, column_n)
  );
- CREATE [UNIQUE] INDEX index_name
  ON table_name (column1, column2, . column_n)
  [ COMPUTE STATISTICS ];
- CREATE [UNIQUE] INDEX index_name
  ON table_name (function1, function2, . function_n)
  [ COMPUTE STATISTICS ];
- CREATE USER username IDENTIFIED BY password;
- CREATE DATABASE test
  DATAFILE 'test_system' SIZE 10M
  LOGFILE GROUP 1 ('test_log1a', 'test_log1b') SIZE 500K,
  GROUP 2 ('test_log2a', 'test_log2b') SIZE 500K;
  test_system is the tablespace of the new database which is 10 MB. 
  test_log1a and test_log1b are the redo log groups
- CREATE INDEX student_idx
- CREATE VIEW v(column1,column12)
  AS
  SELECT column1, column2
  FROM student;
  WITH [CASCADED | LOCAL] CHECK OPTION;
- CREATE TABLE student_bak AS
  SELECT * FROM student;


#### grant
- GRANT privilege TO user;

#### others
- length( string1 ) # returns an integer
- instr( 'oracle pl/sql cheatsheet', '/') # Instr (in string) returns an integer that specifies the location of a sub-string within a string.
- replace( string1, string_to_replace, [ replacement_string ] );
- substr( string, start_position [, length])
- trim ( [ leading | trailing | both ] [ trim-char ] from string-to-be-trimmed );
- Constraint types and codes C	Check on a table	Column
  O	Read Only on a view	Object
  P	Primary Key	Object
  R	Referential AKA Foreign Key	Column
  U	Unique Key	Column
  V	Check Option on a view	Object
- imp brian/brianpassword FILE=mydump.dmp FULL=yes

#### PL/SQL
##### Arithmetic operators
- Addition: +
  Subtraction: -
  Multiplication: *
  Division: /
  Power (PL/SQL only):
##### Comparison operators
- Greater Than: >
  Greater Than or Equal To: >=
  Less Than: <
  Less Than or Equal to: <=
  Equivalence: =
  Inequality: != ^= <> ¬= (depends on platform)
##### String operators
- Concatenate: ||
##### Date operators
- Addition: +
  Subtraction: -

#### types
##### Basic PL/SQL Types
- Scalar type (defined in package STANDARD): NUMBER, CHAR, VARCHAR2, BOOLEAN, BINARY_INTEGER, LONG\LONG RAW, DATE, TIMESTAMP and its family including intervals)
Composite types (user-defined types): TABLE, RECORD, NESTED TABLE and VARRAY
LOB datatypes : used to store an unstructured large amount of data

#### Stored logic
##### Functions
- CREATE [OR REPLACE] FUNCTION function_name [ (parameter [,parameter]) ]
  RETURN [return_datatype]
  IS
  [declaration_section]
  BEGIN
  executable_section
  return [return_value]
  [EXCEPTION
  exception_section]
  END [function_name];
- A function must return a value to the caller.
##### Procedures
- A procedure differs from a function in that it must not return a value to the caller.
- CREATE [OR REPLACE] PROCEDURE procedure_name [ (parameter [,parameter]) ]
  IS
  [declaration_section]
  BEGIN
  executable_section
  [EXCEPTION
  exception_section]
  END [procedure_name];
- There are three types of parameters that can be declared:
IN - The parameter can be referenced by the procedure or function. The value of the parameter can not be overwritten by the procedure or function.
OUT - The parameter can not be referenced by the procedure or function, but the value of the parameter can be overwritten by the procedure or function.
IN OUT - The parameter can be referenced by the procedure or function and the value of the parameter can be overwritten by the procedure or function.

#### Flow control
##### Conditional Operators
- and: AND
  or: OR
  not: NOT
##### If/then/else
- IF [condition] THEN
  [statements]
  ELSEIF [condition] THEN
  [statements}
  ELSE
  [statements}
  END IF;

#### String substitution

#### Advanced Commands
- CURRENT_TIMESTAMP
- SYSDATE


### Mysql


### QA
#### part 1
1. What is Database?
A database is an organized collection of data, stored and retrieved digitally from a remote or local computer system. Databases can be vast and complex, and such databases are developed using fixed design and modeling approaches.

2. What is DBMS?
   DBMS stands for Database Management System. DBMS is a system software responsible for the creation, retrieval, updation, and management of the database. It ensures that our data is consistent, organized, and is easily accessible by serving as an interface between the database and its end-users or application software.

3. What is RDBMS? How is it different from DBMS?
   RDBMS stands for Relational Database Management System. The key difference here, compared to DBMS, is that RDBMS stores data in the form of a collection of tables, and relations can be defined between the common fields of these tables. Most modern database management systems like MySQL, Microsoft SQL Server, Oracle, IBM DB2, and Amazon Redshift are based on RDBMS.

4. What is SQL?
   SQL stands for Structured Query Language. It is the standard language for relational database management systems. It is especially useful in handling organized data comprised of entities (variables) and relations between different entities of the data.

5. What is the difference between SQL and MySQL?
   SQL is a standard language for retrieving and manipulating structured databases. On the contrary, MySQL is a relational database management system, like SQL Server, Oracle or IBM DB2, that is used to manage SQL databases.
6. What are Tables and Fields?
   A table is an organized collection of data stored in the form of rows and columns. Columns can be categorized as vertical and rows as horizontal. The columns in a table are called fields while the rows can be referred to as records.

7. What are Constraints in SQL?
   Constraints are used to specify the rules concerning data in the table. It can be applied for single or multiple fields in an SQL table during the creation of the table or after creating using the ALTER TABLE command. The constraints are:

NOT NULL - Restricts NULL value from being inserted into a column.
CHECK - Verifies that all values in a field satisfy a condition.
DEFAULT - Automatically assigns a default value if no value has been specified for the field.
UNIQUE - Ensures unique values to be inserted into the field.
INDEX - Indexes a field providing faster retrieval of records.
PRIMARY KEY - Uniquely identifies each record in a table.
FOREIGN KEY - Ensures referential integrity for a record in another table
8. What is a Primary Key?
   The PRIMARY KEY constraint uniquely identifies each row in a table. It must contain UNIQUE values and has an implicit NOT NULL constraint.
   A table in SQL is strictly restricted to have one and only one primary key, which is comprised of single or multiple fields (columns).

CREATE TABLE Students (   /* Create table with a single field as primary key */
ID INT NOT NULL
Name VARCHAR(255)
PRIMARY KEY (ID)
);

CREATE TABLE Students (   /* Create table with multiple fields as primary key */
ID INT NOT NULL
LastName VARCHAR(255)
FirstName VARCHAR(255) NOT NULL,
CONSTRAINT PK_Student
PRIMARY KEY (ID, FirstName)
);

ALTER TABLE Students   /* Set a column as primary key */
ADD PRIMARY KEY (ID);
ALTER TABLE Students   /* Set multiple columns as primary key */
ADD CONSTRAINT PK_Student   /*Naming a Primary Key*/
PRIMARY KEY (ID, FirstName);
write a sql statement to add primary key 't_id' to the table 'teachers'.
Write a SQL statement to add primary key constraint 'pk_a' for table 'table_a' and fields 'col_b, col_c'
9. What is a UNIQUE constraint?
   A UNIQUE constraint ensures that all values in a column are different. This provides uniqueness for the column(s) and helps identify each row uniquely. Unlike primary key, there can be multiple unique constraints defined per table. The code syntax for UNIQUE is quite similar to that of PRIMARY KEY and can be used interchangeably.

CREATE TABLE Students (   /* Create table with a single field as unique */
ID INT NOT NULL UNIQUE
Name VARCHAR(255)
);

CREATE TABLE Students (   /* Create table with multiple fields as unique */
ID INT NOT NULL
LastName VARCHAR(255)
FirstName VARCHAR(255) NOT NULL
CONSTRAINT PK_Student
UNIQUE (ID, FirstName)
);

ALTER TABLE Students   /* Set a column as unique */
ADD UNIQUE (ID);
ALTER TABLE Students   /* Set multiple columns as unique */
ADD CONSTRAINT PK_Student   /* Naming a unique constraint */
UNIQUE (ID, FirstName);

10. What is a Foreign Key?
    A FOREIGN KEY comprises of single or collection of fields in a table that essentially refers to the PRIMARY KEY in another table. Foreign key constraint ensures referential integrity in the relation between two tables.
    The table with the foreign key constraint is labeled as the child table, and the table containing the candidate key is labeled as the referenced or parent table.

CREATE TABLE Students (   /* Create table with foreign key - Way 1 */
ID INT NOT NULL
Name VARCHAR(255)
LibraryID INT
PRIMARY KEY (ID)
FOREIGN KEY (Library_ID) REFERENCES Library(LibraryID)
);

CREATE TABLE Students (   /* Create table with foreign key - Way 2 */
ID INT NOT NULL PRIMARY KEY
Name VARCHAR(255)
LibraryID INT FOREIGN KEY (Library_ID) REFERENCES Library(LibraryID)
);

ALTER TABLE Students   /* Add a new foreign key */
ADD FOREIGN KEY (LibraryID)
REFERENCES Library (LibraryID);
What type of integrity constraint does the foreign key ensure?
Write a SQL statement to add a FOREIGN KEY 'col_fk' in 'table_y' that references 'col_pk' in 'table_x'
11. What is a Join? List its different types.
    The SQL Join clause is used to combine records (rows) from two or more tables in a SQL database based on a related column between the two.
    There are four different types of JOINs in SQL:

(INNER) JOIN: Retrieves records that have matching values in both tables involved in the join. This is the widely used join for queries.
SELECT *
FROM Table_A
JOIN Table_B;
SELECT *
FROM Table_A
INNER JOIN Table_B;
LEFT (OUTER) JOIN: Retrieves all the records/rows from the left and the matched records/rows from the right table.
SELECT *
FROM Table_A A
LEFT JOIN Table_B B
ON A.col = B.col;
RIGHT (OUTER) JOIN: Retrieves all the records/rows from the right and the matched records/rows from the left table.
SELECT *
FROM Table_A A
RIGHT JOIN Table_B B
ON A.col = B.col;
FULL (OUTER) JOIN: Retrieves all the records where there is a match in either the left or right table.
SELECT *
FROM Table_A A
FULL JOIN Table_B B
ON A.col = B.col;
12. What is a Self-Join?
    A self JOIN is a case of regular join where a table is joined to itself based on some relation between its own column(s). Self-join uses the INNER JOIN or LEFT JOIN clause and a table alias is used to assign different names to the table within the query.

SELECT A.emp_id AS "Emp_ID",A.emp_name AS "Employee",
B.emp_id AS "Sup_ID",B.emp_name AS "Supervisor"
FROM employee A, employee B
WHERE A.emp_sup = B.emp_id;
13. What is a Cross-Join?
    Cross join can be defined as a cartesian product of the two tables included in the join. The table after join contains the same number of rows as in the cross-product of the number of rows in the two tables. If a WHERE clause is used in cross join then the query will work like an INNER JOIN.

SELECT stu.name, sub.subject
FROM students AS stu
CROSS JOIN subjects AS sub;

Write a SQL statement to CROSS JOIN 'table_1' with 'table_2' and fetch 'col_1' from table_1 & 'col_2' from table_2 respectively. Do not use alias.
Write a SQL statement to perform SELF JOIN for 'Table_X' with alias 'Table_1' and 'Table_2', on columns 'Col_1' and 'Col_2' respectively
14. What is an Index? Explain its different types.
    A database index is a data structure that provides a quick lookup of data in a column or columns of a table. It enhances the speed of operations accessing data from a database table at the cost of additional writes and memory to maintain the index data structure.

CREATE INDEX index_name   /* Create Index */
ON table_name (column_1, column_2);
DROP INDEX index_name;   /* Drop Index */
There are different types of indexes that can be created for different purposes:

Unique and Non-Unique Index:
Unique indexes are indexes that help maintain data integrity by ensuring that no two rows of data in a table have identical key values. Once a unique index has been defined for a table, uniqueness is enforced whenever keys are added or changed within the index.

CREATE UNIQUE INDEX myIndex
ON students (enroll_no);
Non-unique indexes, on the other hand, are not used to enforce constraints on the tables with which they are associated. Instead, non-unique indexes are used solely to improve query performance by maintaining a sorted order of data values that are used frequently.

Clustered and Non-Clustered Index:
Clustered indexes are indexes whose order of the rows in the database corresponds to the order of the rows in the index. This is why only one clustered index can exist in a given table, whereas, multiple non-clustered indexes can exist in the table.

The only difference between clustered and non-clustered indexes is that the database manager attempts to keep the data in the database in the same order as the corresponding keys appear in the clustered index.

Clustering indexes can improve the performance of most query operations because they provide a linear-access path to data stored in the database.

Write a SQL statement to create a UNIQUE INDEX "my_index" on "my_table" for fields "column_1" & "column_2".

15. What is the difference between Clustered and Non-clustered index?
    As explained above, the differences can be broken down into three small factors -

Clustered index modifies the way records are stored in a database based on the indexed column. A non-clustered index creates a separate entity within the table which references the original table.
Clustered index is used for easy and speedy retrieval of data from the database, whereas, fetching records from the non-clustered index is relatively slower.
In SQL, a table can have a single clustered index whereas it can have multiple non-clustered indexes
16. What is Data Integrity?
    Data Integrity is the assurance of accuracy and consistency of data over its entire life-cycle and is a critical aspect of the design, implementation, and usage of any system which stores, processes, or retrieves data. It also defines integrity constraints to enforce business rules on the data when it is entered into an application or a database.

17. What is a Query?
    A query is a request for data or information from a database table or combination of tables. A database query can be either a select query or an action query.

SELECT fname, lname    /* select query */
FROM myDb.students
WHERE student_id = 1;
UPDATE myDB.students    /* action query */
SET fname = 'Captain', lname = 'America'
WHERE student_id = 1;
18. What is a Subquery? What are its types?
    A subquery is a query within another query, also known as a nested query or inner query. It is used to restrict or enhance the data to be queried by the main query, thus restricting or enhancing the output of the main query respectively. For example, here we fetch the contact information for students who have enrolled for the maths subject:

SELECT name, email, mob, address
FROM myDb.contacts
WHERE roll_no IN (
SELECT roll_no
FROM myDb.students
WHERE subject = 'Maths');
There are two types of subquery - Correlated and Non-Correlated.

A correlated subquery cannot be considered as an independent query, but it can refer to the column in a table listed in the FROM of the main query.
A non-correlated subquery can be considered as an independent query and the output of the subquery is substituted in the main query.
Write a SQL query to update the field "status" in table "applications" from 0 to 1.
Write a SQL query to select the field "app_id" in table "applications" where "app_id" less than 1000.
Write a SQL query to fetch the field "app_name" from "apps" where "apps.id" is equal to the above collection of "app_id".
19. What is the SELECT statement?
    SELECT operator in SQL is used to select data from a database. The data returned is stored in a result table, called the result-set.

SELECT * FROM myDB.students;
20. What are some common clauses used with SELECT query in SQL?
    Some common SQL clauses used in conjuction with a SELECT query are as follows:

WHERE clause in SQL is used to filter records that are necessary, based on specific conditions.
ORDER BY clause in SQL is used to sort the records based on some field(s) in ascending (ASC) or descending order (DESC).
SELECT *
FROM myDB.students
WHERE graduation_year = 2019
ORDER BY studentID DESC;
GROUP BY clause in SQL is used to group records with identical data and can be used in conjunction with some aggregation functions to produce summarized results from the database.
HAVING clause in SQL is used to filter records in combination with the GROUP BY clause. It is different from WHERE, since the WHERE clause cannot filter aggregated records.
SELECT COUNT(studentId), country
FROM myDB.students
WHERE country != "INDIA"
GROUP BY country
HAVING COUNT(studentID) > 5;


#### part 2
21. What are UNION, MINUS and INTERSECT commands?
    The UNION operator combines and returns the result-set retrieved by two or more SELECT statements.
    The MINUS operator in SQL is used to remove duplicates from the result-set obtained by the second SELECT query from the result-set obtained by the first SELECT query and then return the filtered results from the first.
    The INTERSECT clause in SQL combines the result-set fetched by the two SELECT statements where records from one match the other and then returns this intersection of result-sets.

Certain conditions need to be met before executing either of the above statements in SQL -

Each SELECT statement within the clause must have the same number of columns
The columns must also have similar data types
The columns in each SELECT statement should necessarily have the same order
SELECT name FROM Students   /* Fetch the union of queries */
UNION
SELECT name FROM Contacts;
SELECT name FROM Students   /* Fetch the union of queries with duplicates*/
UNION ALL
SELECT name FROM Contacts;
SELECT name FROM Students   /* Fetch names from students */
MINUS     /* that aren't present in contacts */
SELECT name FROM Contacts;
SELECT name FROM Students   /* Fetch names from students */
INTERSECT    /* that are present in contacts as well */
SELECT name FROM Contacts;
Write a SQL query to fetch "names" that are present in either table "accounts" or in table "registry".
Write a SQL query to fetch "names" that are present in "accounts" but not in table "registry".
Write a SQL query to fetch "names" from table "contacts" that are neither present in "accounts.name" nor in "registry.name".
22. What is Cursor? How to use a Cursor?
    A database cursor is a control structure that allows for the traversal of records in a database. Cursors, in addition, facilitates processing after traversal, such as retrieval, addition, and deletion of database records. They can be viewed as a pointer to one row in a set of rows.

Working with SQL Cursor:

DECLARE a cursor after any variable declaration. The cursor declaration must always be associated with a SELECT Statement.
Open cursor to initialize the result set. The OPEN statement must be called before fetching rows from the result set.
FETCH statement to retrieve and move to the next row in the result set.
Call the CLOSE statement to deactivate the cursor.
Finally use the DEALLOCATE statement to delete the cursor definition and release the associated resources.
DECLARE @name VARCHAR(50)   /* Declare All Required Variables */
DECLARE db_cursor CURSOR FOR   /* Declare Cursor Name*/
SELECT name
FROM myDB.students
WHERE parent_name IN ('Sara', 'Ansh')
OPEN db_cursor   /* Open cursor and Fetch data into @name */
FETCH next
FROM db_cursor
INTO @name
CLOSE db_cursor   /* Close the cursor and deallocate the resources */
DEALLOCATE db_cursor
23. What are Entities and Relationships?
    Entity: An entity can be a real-world object, either tangible or intangible, that can be easily identifiable. For example, in a college database, students, professors, workers, departments, and projects can be referred to as entities. Each entity has some associated properties that provide it an identity.

Relationships: Relations or links between entities that have something to do with each other. For example - The employee's table in a company's database can be associated with the salary table in the same database.
24. List the different types of relationships in SQL.
    One-to-One - This can be defined as the relationship between two tables where each record in one table is associated with the maximum of one record in the other table.
    One-to-Many & Many-to-One - This is the most commonly used relationship where a record in a table is associated with multiple records in the other table.
    Many-to-Many - This is used in cases when multiple instances on both sides are needed for defining a relationship.
    Self-Referencing Relationships - This is used when a table needs to define a relationship with itself.
25. What is an Alias in SQL?
    An alias is a feature of SQL that is supported by most, if not all, RDBMSs. It is a temporary name assigned to the table or table column for the purpose of a particular SQL query. In addition, aliasing can be employed as an obfuscation technique to secure the real names of database fields. A table alias is also called a correlation name.

An alias is represented explicitly by the AS keyword but in some cases, the same can be performed without it as well. Nevertheless, using the AS keyword is always a good practice.

SELECT A.emp_name AS "Employee"  /* Alias using AS keyword */
B.emp_name AS "Supervisor"
FROM employee A, employee B   /* Alias without AS keyword */
WHERE A.emp_sup = B.emp_id;
Write an SQL statement to select all from table "Limited" with alias "Ltd".
26. What is a View?
    A view in SQL is a virtual table based on the result-set of an SQL statement. A view contains rows and columns, just like a real table. The fields in a view are fields from one or more real tables in the database.
27. What is Normalization?
    Normalization represents the way of organizing structured data in the database efficiently. It includes the creation of tables, establishing relationships between them, and defining rules for those relationships. Inconsistency and redundancy can be kept in check based on these rules, hence, adding flexibility to the database.

28. What is Denormalization?
    Denormalization is the inverse process of normalization, where the normalized schema is converted into a schema that has redundant information. The performance is improved by using redundancy and keeping the redundant data consistent. The reason for performing denormalization is the overheads produced in the query processor by an over-normalized structure.

29. What are the various forms of Normalization?
    Normal Forms are used to eliminate or reduce redundancy in database tables. The different forms are as follows:

- First Normal Form:
A relation is in first normal form if every attribute in that relation is a single-valued attribute. If a relation contains a composite or multi-valued attribute, it violates the first normal form. Let's consider the following students table. Each student in the table, has a name, his/her address, and the books they issued from the public library -
Second Normal Form:
A relation is in second normal form if it satisfies the conditions for the first normal form and does not contain any partial dependency. A relation in 2NF has no partial dependency, i.e., it has no non-prime attribute that depends on any proper subset of any candidate key of the table. Often, specifying a single column Primary Key is the solution to the problem.
Third Normal Form
A relation is said to be in the third normal form, if it satisfies the conditions for the second normal form and there is no transitive dependency between the non-prime attributes, i.e., all non-prime attributes are determined only by the candidate keys of the relation and not by any other non-prime attribute
Boyce-Codd Normal Form
A relation is in Boyce-Codd Normal Form if satisfies the conditions for third normal form and for every functional dependency, Left-Hand-Side is super key. In other words, a relation in BCNF has non-trivial functional dependencies in form X –> Y, such that X is always a super key. For example - In the above example, Student_ID serves as the sole unique identifier for the Students Table and Salutation_ID for the Salutations Table, thus these tables exist in BCNF. The same cannot be said for the Books Table and there can be several books with common Book Names and the same Student_ID

30. What are the TRUNCATE, DELETE and DROP statements?
    DELETE statement is used to delete rows from a table.

DELETE FROM Candidates
WHERE CandidateId > 1000;
TRUNCATE command is used to delete all the rows from the table and free the space containing the table.

TRUNCATE TABLE Candidates;
DROP command is used to remove an object from the database. If you drop a table, all the rows in the table are deleted and the table structure is removed from the database.

DROP TABLE Candidates;
Write a SQL statement to wipe a table 'Temporary' from memory.
Write a SQL query to remove first 1000 records from table 'Temporary' based on 'id'.
Write a SQL statement to delete the table 'Temporary' while keeping its relations intact.
31. What is the difference between DROP and TRUNCATE statements?
    If a table is dropped, all things associated with the tables are dropped as well. This includes - the relationships defined on the table with other tables, the integrity checks and constraints, access privileges and other grants that the table has. To create and use the table again in its original form, all these relations, checks, constraints, privileges and relationships need to be redefined. However, if a table is truncated, none of the above problems exist and the table retains its original structure.

32. What is the difference between DELETE and TRUNCATE statements?
    The TRUNCATE command is used to delete all the rows from the table and free the space containing the table.
    The DELETE command deletes only the rows from the table based on the condition given in the where clause or deletes all the rows from the table if no condition is specified. But it does not free the space containing the table

33. What are Aggregate and Scalar functions?
    An aggregate function performs operations on a collection of values to return a single scalar value. Aggregate functions are often used with the GROUP BY and HAVING clauses of the SELECT statement. Following are the widely used SQL aggregate functions:

- AVG() - Calculates the mean of a collection of values.
COUNT() - Counts the total number of records in a specific table or view.
MIN() - Calculates the minimum of a collection of values.
MAX() - Calculates the maximum of a collection of values.
SUM() - Calculates the sum of a collection of values.
FIRST() - Fetches the first element in a collection of values.
LAST() - Fetches the last element in a collection of values.
Note: All aggregate functions described above ignore NULL values except for the COUNT function.

A scalar function returns a single value based on the input value. Following are the widely used SQL scalar functions:

- LEN() - Calculates the total length of the given field (column).
UCASE() - Converts a collection of string values to uppercase characters.
LCASE() - Converts a collection of string values to lowercase characters.
MID() - Extracts substrings from a collection of string values in a table.
CONCAT() - Concatenates two or more strings.
RAND() - Generates a random collection of numbers of a given length.
ROUND() - Calculates the round-off integer value for a numeric field (or decimal point values).
NOW() - Returns the current date & time.
FORMAT() - Sets the format to display a collection of values

34. What is User-defined function? What are its various types?
    The user-defined functions in SQL are like functions in any other programming language that accept parameters, perform complex calculations, and return a value. They are written to use the logic repetitively whenever required. There are two types of SQL user-defined functions:

Scalar Function: As explained earlier, user-defined scalar functions return a single scalar value.
Table-Valued Functions: User-defined table-valued functions return a table as output.
Inline: returns a table data type based on a single SELECT statement.
Multi-statement: returns a tabular result-set but, unlike inline, multiple SELECT statements can be used inside the function body.
35. What is OLTP?
    OLTP stands for Online Transaction Processing, is a class of software applications capable of supporting transaction-oriented programs. An essential attribute of an OLTP system is its ability to maintain concurrency. To avoid single points of failure, OLTP systems are often decentralized. These systems are usually designed for a large number of users who conduct short transactions. Database queries are usually simple, require sub-second response times, and return relatively few records. Here is an insight into the working of an OLTP system [ Note - The figure is not important for interviews ] -

36. What are the differences between OLTP and OLAP?
    OLTP stands for Online Transaction Processing, is a class of software applications capable of supporting transaction-oriented programs. An important attribute of an OLTP system is its ability to maintain concurrency. OLTP systems often follow a decentralized architecture to avoid single points of failure. These systems are generally designed for a large audience of end-users who conduct short transactions. Queries involved in such databases are generally simple, need fast response times, and return relatively few records. A number of transactions per second acts as an effective measure for such systems.

OLAP stands for Online Analytical Processing, a class of software programs that are characterized by the relatively low frequency of online transactions. Queries are often too complex and involve a bunch of aggregations. For OLAP systems, the effectiveness measure relies highly on response time. Such systems are widely used for data mining or maintaining aggregated, historical data, usually in multi-dimensional schemas.
37. What is Collation? What are the different types of Collation Sensitivity?
    Collation refers to a set of rules that determine how data is sorted and compared. Rules defining the correct character sequence are used to sort the character data. It incorporates options for specifying case sensitivity, accent marks, kana character types, and character width. Below are the different types of collation sensitivity:

Case sensitivity: A and a are treated differently.
Accent sensitivity: a and á are treated differently.
Kana sensitivity: Japanese kana characters Hiragana and Katakana are treated differently.
Width sensitivity: Same character represented in single-byte (half-width) and double-byte (full-width) are treated differently.
38. What is a Stored Procedure?
    A stored procedure is a subroutine available to applications that access a relational database management system (RDBMS). Such procedures are stored in the database data dictionary. The sole disadvantage of stored procedure is that it can be executed nowhere except in the database and occupies more memory in the database server. It also provides a sense of security and functionality as users who can't access the data directly can be granted access via stored procedures.

DELIMITER $$
CREATE PROCEDURE FetchAllStudents()
BEGIN
SELECT *  FROM myDB.students;
END $$
DELIMITER ;

39. What is a Recursive Stored Procedure?
    A stored procedure that calls itself until a boundary condition is reached, is called a recursive stored procedure. This recursive function helps the programmers to deploy the same set of code several times as and when required. Some SQL programming languages limit the recursion depth to prevent an infinite loop of procedure calls from causing a stack overflow, which slows down the system and may lead to system crashes.

DELIMITER $$     /* Set a new delimiter => $$ */
CREATE PROCEDURE calctotal( /* Create the procedure */
IN number INT,   /* Set Input and Ouput variables */
OUT total INT
) BEGIN
DECLARE score INT DEFAULT NULL;   /* Set the default value => "score" */
SELECT awards FROM achievements   /* Update "score" via SELECT query */
WHERE id = number INTO score;
IF score IS NULL THEN SET total = 0;   /* Termination condition */
ELSE
CALL calctotal(number+1);   /* Recursive call */
SET total = total + score;   /* Action after recursion */
END IF;
END $$     /* End of procedure */
DELIMITER ;     /* Reset the delimiter */
40. How to create empty tables with the same structure as another table?
    Creating empty tables with the same structure can be done smartly by fetching the records of one table into a new table using the INTO operator while fixing a WHERE clause to be false for all records. Hence, SQL prepares the new table with a duplicate structure to accept the fetched records but since no records get fetched due to the WHERE clause in action, nothing is inserted into the new table.

SELECT * INTO Students_copy
FROM Students WHERE 1 = 2;

#### part 3
41. What is Pattern Matching in SQL?
    SQL pattern matching provides for pattern search in data if you have no clue as to what that word should be. This kind of SQL query uses wildcards to match a string pattern, rather than writing the exact word. The LIKE operator is used in conjunction with SQL Wildcards to fetch the required information.

Using the % wildcard to perform a simple search
The % wildcard matches zero or more characters of any type and can be used to define wildcards both before and after the pattern. Search a student in your database with first name beginning with the letter K:

SELECT *
FROM students
WHERE first_name LIKE 'K%'
Omitting the patterns using the NOT keyword
Use the NOT keyword to select records that don't match the pattern. This query returns all students whose first name does not begin with K.

SELECT *
FROM students
WHERE first_name NOT LIKE 'K%'
Matching a pattern anywhere using the % wildcard twice
Search for a student in the database where he/she has a K in his/her first name.

SELECT *
FROM students
WHERE first_name LIKE '%Q%'
Using the _ wildcard to match pattern at a specific position
The _ wildcard matches exactly one character of any type. It can be used in conjunction with % wildcard. This query fetches all students with letter K at the third position in their first name.

SELECT *
FROM students
WHERE first_name LIKE '__K%'

Matching patterns for a specific length
The _ wildcard plays an important role as a limitation when it matches exactly one character. It limits the length and position of the matched results. For example -

SELECT *   /* Matches first names with three or more letters */
FROM students
WHERE first_name LIKE '___%'

SELECT *   /* Matches first names with exactly four characters */
FROM students
WHERE first_name LIKE '____'

PostgreSQL Interview Questions
42. What is PostgreSQL?
    PostgreSQL was first called Postgres and was developed by a team led by Computer Science Professor Michael Stonebraker in 1986. It was developed to help developers build enterprise-level applications by upholding data integrity by making systems fault-tolerant. PostgreSQL is therefore an enterprise-level, flexible, robust, open-source, and object-relational DBMS that supports flexible workloads along with handling concurrent users. It has been consistently supported by the global developer community. Due to its fault-tolerant nature, PostgreSQL has gained widespread popularity among developers.

43. How do you define Indexes in PostgreSQL?
    Indexes are the inbuilt functions in PostgreSQL which are used by the queries to perform search more efficiently on a table in the database. Consider that you have a table with thousands of records and you have the below query that only a few records can satisfy the condition, then it will take a lot of time to search and return those rows that abide by this condition as the engine has to perform the search operation on every single to check this condition. This is undoubtedly inefficient for a system dealing with huge data. Now if this system had an index on the column where we are applying search, it can use an efficient method for identifying matching rows by walking through only a few levels. This is called indexing.

Select * from some_table where table_col=120
44. How will you change the datatype of a column?
    This can be done by using the ALTER TABLE statement as shown below:

Syntax:

ALTER TABLE tname
ALTER COLUMN col_name [SET DATA] TYPE new_data_type;
45. What is the command used for creating a database in PostgreSQL?
    The first step of using PostgreSQL is to create a database. This is done by using the createdb command as shown below: createdb db_name
    After running the above command, if the database creation was successful, then the below message is shown:

CREATE DATABASE
46. How can we start, restart and stop the PostgreSQL server?
    To start the PostgreSQL server, we run:
    service postgresql start
    Once the server is successfully started, we get the below message:
    Starting PostgreSQL: ok
    To restart the PostgreSQL server, we run:
    service postgresql restart
    Once the server is successfully restarted, we get the message:

Restarting PostgreSQL: server stopped
ok
To stop the server, we run the command:
service postgresql stop
Once stopped successfully, we get the message:

Stopping PostgreSQL: server stopped
ok

47. What are partitioned tables called in PostgreSQL?
    Partitioned tables are logical structures that are used for dividing large tables into smaller structures that are called partitions. This approach is used for effectively increasing the query performance while dealing with large database tables. To create a partition, a key called partition key which is usually a table column or an expression, and a partitioning method needs to be defined. There are three types of inbuilt partitioning methods provided by Postgres:

Range Partitioning: This method is done by partitioning based on a range of values. This method is most commonly used upon date fields to get monthly, weekly or yearly data. In the case of corner cases like value belonging to the end of the range, for example: if the range of partition 1 is 10-20 and the range of partition 2 is 20-30, and the given value is 10, then 10 belongs to the second partition and not the first.
List Partitioning: This method is used to partition based on a list of known values. Most commonly used when we have a key with a categorical value. For example, getting sales data based on regions divided as countries, cities, or states.
Hash Partitioning: This method utilizes a hash function upon the partition key. This is done when there are no specific requirements for data division and is used to access data individually. For example, you want to access data based on a specific product, then using hash partition would result in the dataset that we require.
The type of partition key and the type of method used for partitioning determines how positive the performance and the level of manageability of the partitioned table are.

48. Define tokens in PostgreSQL?
    A token in PostgreSQL is either a keyword, identifier, literal, constant, quotes identifier, or any symbol that has a distinctive personality. They may or may not be separated using a space, newline or a tab. If the tokens are keywords, they are usually commands with useful meanings. Tokens are known as building blocks of any PostgreSQL code

49. What is the importance of the TRUNCATE statement?
    TRUNCATE TABLE name_of_table statement removes the data efficiently and quickly from the table.
    The truncate statement can also be used to reset values of the identity columns along with data cleanup as shown below:

TRUNCATE TABLE name_of_table
RESTART IDENTITY;
We can also use the statement for removing data from multiple tables all at once by mentioning the table names separated by comma as shown below:

TRUNCATE TABLE
table_1,
table_2,
table_3;
50. What is the capacity of a table in PostgreSQL?
    The maximum size of PostgreSQL is 32TB.

51. Define sequence.
    A sequence is a schema-bound, user-defined object which aids to generate a sequence of integers. This is most commonly used to generate values to identity columns in a table. We can create a sequence by using the CREATE SEQUENCE statement as shown below:

CREATE SEQUENCE serial_num START 100;
To get the next number 101 from the sequence, we use the nextval() method as shown below:

SELECT nextval('serial_num');
We can also use this sequence while inserting new records using the INSERT command:

INSERT INTO ib_table_name VALUES (nextval('serial_num'), 'interviewbit');

52. What are string constants in PostgreSQL?
    They are character sequences bound within single quotes. These are using during data insertion or updation to characters in the database.
    There are special string constants that are quoted in dollars. Syntax: $tag$<string_constant>$tag$ The tag in the constant is optional and when we are not specifying the tag, the constant is called a double-dollar string literal.

53. How can you get a list of all databases in PostgreSQL?
    This can be done by using the command \l -> backslash followed by the lower-case letter L.

54. How can you delete a database in PostgreSQL?
    This can be done by using the DROP DATABASE command as shown in the syntax below:

DROP DATABASE database_name;
If the database has been deleted successfully, then the following message would be shown:

DROP DATABASE
55. What are ACID properties? Is PostgreSQL compliant with ACID?
    ACID stands for Atomicity, Consistency, Isolation, Durability. They are database transaction properties which are used for guaranteeing data validity in case of errors and failures.

- Atomicity: This property ensures that the transaction is completed in all-or-nothing way.
Consistency: This ensures that updates made to the database is valid and follows rules and restrictions.
Isolation: This property ensures integrity of transaction that are visible to all other transactions.
Durability: This property ensures that the committed transactions are stored permanently in the database.
PostgreSQL is compliant with ACID properties

56. Can you explain the architecture of PostgreSQL?
    The architecture of PostgreSQL follows the client-server model.
    The server side comprises of background process manager, query processer, utilities and shared memory space which work together to build PostgreSQL’s instance that has access to the data. The client application does the task of connecting to this instance and requests data processing to the services. The client can either be GUI (Graphical User Interface) or a web application. The most commonly used client for PostgreSQL is pgAdmin.

57. What do you understand by multi-version concurrency control?
    MVCC or Multi-version concurrency control is used for avoiding unnecessary database locks when 2 or more requests tries to access or modify the data at the same time. This ensures that the time lag for a user to log in to the database is avoided. The transactions are recorded when anyone tries to access the content.

For more information regarding this, you can refer here.

58. What do you understand by command enable-debug?
    The command enable-debug is used for enabling the compilation of all libraries and applications. When this is enabled, the system processes get hindered and generally also increases the size of the binary file. Hence, it is not recommended to switch this on in the production environment. This is most commonly used by developers to debug the bugs in their scripts and help them spot the issues. For more information regarding how to debug, you can refer here

#### part 4
59. How do you check the rows affected as part of previous transactions?
    SQL standards state that the following three phenomena should be prevented whilst concurrent transactions. SQL standards define 4 levels of transaction isolations to deal with these phenomena.

- Dirty reads: If a transaction reads data that is written due to concurrent uncommitted transaction, these reads are called dirty reads.
Phantom reads: This occurs when two same queries when executed separately return different rows. For example, if transaction A retrieves some set of rows matching search criteria. Assume another transaction B retrieves new rows in addition to the rows obtained earlier for the same search criteria. The results are different.
Non-repeatable reads: This occurs when a transaction tries to read the same row multiple times and gets different values each time due to concurrency. This happens when another transaction updates that data and our current transaction fetches that updated data, resulting in different values.
To tackle these, there are 4 standard isolation levels defined by SQL standards. They are as follows:

- Read Uncommitted – The lowest level of the isolations. Here, the transactions are not isolated and can read data that are not committed by other transactions resulting in dirty reads.
Read Committed – This level ensures that the data read is committed at any instant of read time. Hence, dirty reads are avoided here. This level makes use of read/write lock on the current rows which prevents read/write/update/delete of that row when the current transaction is being operated on.
Repeatable Read – The most restrictive level of isolation. This holds read and write locks for all rows it operates on. Due to this, non-repeatable reads are avoided as other transactions cannot read, write, update or delete the rows.
Serializable – The highest of all isolation levels. This guarantees that the execution is serializable where execution of any concurrent operations are guaranteed to be appeared as executing serially.
The following table clearly explains which type of unwanted reads the levels avoid:

- Isolation levels 	Dirty Reads 	Phantom Reads 	Non-repeatable reads
Read Uncommitted 	Might occur	Might occur	Might occur
Read Committed 	Won’t occur	Might occur	Might occur
Repeatable Read	Won’t occur	Might occur	Won’t occur
Serializable	Won’t occur	Won’t occur	Won’t occur

60. What can you tell about WAL (Write Ahead Logging)?
    Write Ahead Logging is a feature that increases the database reliability by logging changes before any changes are done to the database. This ensures that we have enough information when a database crash occurs by helping to pinpoint to what point the work has been complete and gives a starting point from the point where it was discontinued.

For more information, you can refer here.

61. What is the main disadvantage of deleting data from an existing table using the DROP TABLE command?
    DROP TABLE command deletes complete data from the table along with removing the complete table structure too. In case our requirement entails just remove the data, then we would need to recreate the table to store data in it. In such cases, it is advised to use the TRUNCATE command.

62. How do you perform case-insensitive searches using regular expressions in PostgreSQL?
    To perform case insensitive matches using a regular expression, we can use POSIX (~*) expression from pattern matching operators. For example:

'interviewbit' ~* '.*INTervIewBit.*'
63. How will you take backup of the database in PostgreSQL?
    We can achieve this by using the pg_dump tool for dumping all object contents in the database into a single file. The steps are as follows:

Step 1: Navigate to the bin folder of the PostgreSQL installation path.

C:\>cd C:\Program Files\PostgreSQL\10.0\bin
Step 2: Execute pg_dump program to take the dump of data to a .tar folder as shown below:

pg_dump -U postgres -W -F t sample_data > C:\Users\admin\pgbackup\sample_data.tar
The database dump will be stored in the sample_data.tar file on the location specified

64. Does PostgreSQL support full text search?
    Full-Text Search is the method of searching single or collection of documents stored on a computer in a full-text based database. This is mostly supported in advanced database systems like SOLR or ElasticSearch. However, the feature is present but is pretty basic in PostgreSQL.

65. What are parallel queries in PostgreSQL?
    Parallel Queries support is a feature provided in PostgreSQL for devising query plans capable of exploiting multiple CPU processors to execute the queries faster.
66. Differentiate between commit and checkpoint.
    The commit action ensures that the data consistency of the transaction is maintained and it ends the current transaction in the section. Commit adds a new record in the log that describes the COMMIT to the memory. Whereas, a checkpoint is used for writing all changes that were committed to disk up to SCN which would be kept in datafile headers and control files.

Conclusion:
SQL is a language for the database. It has a vast scope and robust capability of creating and manipulating a variety of database objects using commands like CREATE, ALTER, DROP, etc, and also in loading the database objects using commands like INSERT. It also provides options for Data Manipulation using commands like DELETE, TRUNCATE and also does effective retrieval of data using cursor commands like FETCH, SELECT, etc. There are many such commands which provide a large amount of control to the programmer to interact with the database in an efficient way without wasting many resources. The popularity of SQL has grown so much that almost every programmer relies on this to implement their application's storage functionalities thereby making it an exciting language to learn. Learning this provides the developer a benefit of understanding the data structures used for storing the organization's data and giving an additional level of control and in-depth understanding of the application.

PostgreSQL being an open-source database system having extremely robust and sophisticated ACID, Indexing, and Transaction supports has found widespread popularity among the developer community.


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



#### part 6
- PL/SQL stands for Procedural Language extensions to SQL (Structured Query Language). It was created by Oracle in order to overcome the disadvantages of SQL for easier building and handling of critical applications in a comprehensive manner.
  Following are the disadvantages of SQL:

There is no provision of decision-making, looping, and branching in SQL.
Since the SQL statements get passed to the Oracle engine all at the same time, the speed of execution decreases due to the nature of increased traffic.
There is no feature of error checking while manipulating the data.
PL/SQL was introduced to overcome the above disadvantages by retaining the power of SQL and combining it with the procedural statements. It is developed as a block-structured language and the statements of the block are passed to the oracle engine which helps to increase the speed of processing due to the decrease in traffic.

1. What are the features of PL/SQL?
   Following are the features of PL/SQL:

PL/SQL provides the feature of decision making, looping, and branching by making use of its procedural nature.
Multiple queries can be processed in one block by making use of a single command using PL/SQL.
The PL/SQL code can be reused by applications as they can be grouped and stored in databases as PL/SQL units like functions, procedures, packages, triggers, and types.
PL/SQL supports exception handling by making use of an exception handling block.
Along with exception handling, PL/SQL also supports error checking and validation of data before data manipulation.
Applications developed using PL/SQL are portable across computer hardware or operating system where there is an Oracle engine.
2. What do you understand by PL/SQL table?
   PL/SQL tables are nothing but objects of type tables that are modeled as database tables. They are a way to provide arrays that are nothing but temporary tables in memory for faster processing.
   These tables are useful for moving bulk data thereby simplifying the process
3. Explain the basic structure followed in PL/SQL?
   The basic structure of PL/SQL follows the BLOCK structure. Each PL/SQL code comprises SQL and PL/SQL statement that constitutes a PL/SQL block.
   Each PL/SQL block consists of 3 sections:
   The optional Declaration Section
   The mandatory Execution Section
   The optional Exception handling Section
   [DECLARE]
   --declaration statements (optional)
   BEGIN
   --execution statements
   [EXCEPTION]
   --exception handling statements (optional)
   END;
4. What is a PL/SQL cursor?
   A PL/SQL cursor is nothing but a pointer to an area of memory having SQL statements and the information of statement processing. This memory area is called a context area. This special area makes use of a special feature called cursor for the purpose of retrieving and processing more than one row.
   In short, the cursor selects multiple rows from the database and these selected rows are individually processed within a program.
-   There are two types of cursors:
   Implicit Cursor:
   Oracle automatically creates a cursor while running any of the commands - SELECT INTO, INSERT, DELETE or UPDATE implicitly.
   The execution cycle of these cursors is internally handled by Oracle and returns the information and status of the cursor by making use of the cursor attributes- ROWCOUNT, ISOPEN, FOUND, NOTFOUND.
   Explicit Cursor:
   This cursor is a SELECT statement that was declared explicitly in the declaration block.
   The programmer has to control the execution cycle of these cursors starting from OPEN to FETCH and close.
   The execution cycle while executing the SQL statement is defined by Oracle along with associating a cursor with it.
-   Explicit Cursor Execution Cycle:
   Due to the flexibility of defining our own execution cycle, explicit cursors are used in many instances. The following diagram represents the execution flow of an explicit cursor:
-   Cursor Declaration:
   The first step to use an explicit cursor is its declaration.
   Declaration can be done in a package or a block.
   Syntax: CURSOR cursor_name IS query; where cursor_name is the name of the cursor, the query is the query to fetch data from any table.
-   Open Cursor:
   Before the process of fetching rows from cursor, the cursor has to be opened.
   Syntax to open a cursor: OPEN cursor_name;
   When the cursor is opened, the query and the bind variables are parsed by Oracle and the SQL statements are executed.
   The execution plan is determined by Oracle and the result set is determined after associating the cursor parameters and host variables and post these, the cursor is set to point at the first row of the result set.
-   Fetch from cursor:
   FETCH statement is used to place the content of the current row into variables.
   Syntax: FETCH cursor_name INTO variable_list;
   In order to get all the rows of a result set, each row needs to be fetched.
-   Close Cursor:
   Once all the rows are fetched, the cursor needs to be closed using the CLOSE statement.
   Syntax: CLOSE cursor_name;
   The instructions tell Oracle to release the memory allocated to the cursor.
   Cursors declared in procedures or anonymous blocks are by default closed post their execution.
   Cursors declared in packages need to be closed explicitly as the scope is global.
   Closing a cursor that is not opened will result in INVALID_CURSOR exception
5. What is the use of WHERE CURRENT OF in cursors?
   We use this clause while referencing the current row from an explicit cursor. This clause allows applying updates and deletion of the row currently under consideration without explicitly referencing the row ID.
   Syntax:
   UPDATE table_name SET field=new_value WHERE CURRENT OF cursor_name
6. How can a name be assigned to an unnamed PL/SQL Exception Block?
   This can be done by using Pragma called EXCEPTION_INIT.
   This gives the flexibility to the programmer to instruct the compiler to provide custom error messages based on the business logic by overriding the pre-defined messages during the compilation time.
   Syntax:
   DECLARE
   exception_name EXCEPTION;
   PRAGMA EXCEPTION_INIT (exception_name, error_code);
   BEGIN
   // PL/SQL Logic
   EXCEPTION
   WHEN exception_name THEN
   // Steps to handle exception
   END;
7. What is a Trigger? Name some instances when “Triggers” can be used.
   As the name indicates, ‘Trigger’ means to ‘activate’ something. In the case of PL/SQL, a trigger is a stored procedure that specifies what action has to be taken by the database when an event related to the database is performed
   Syntax:
   TRIGGER trigger_name
   trigger_event
   [ restrictions ]
   BEGIN
   actions_of_trigger;
   END;
   In the above syntax, if the trigger_name the trigger is in the enabled state, the trigger_event causes the database to fire actions_of_trigger if the restrictions are TRUE or unavailable.

They are mainly used in the following scenarios:
In order to maintain complex integrity constraints.
For the purpose of auditing any table information.
Whenever changes are done to a table, if we need to signal other actions upon completion of the change, then we use triggers.
In order to enforce complex rules of business.
It can also be used to prevent invalid transactions.
You can refer https://docs.oracle.com/database/121/TDDDG/tdddg_triggers.htm for more information regarding triggers.
8. When does a DECLARE block become mandatory?
   This statement is used by anonymous blocks of PL/SQL such as non-stored and stand-alone procedures. When they are being used, the statement should come first in the stand-alone file
9. How do you write comments in a PL/SQL code?
   Comments are those sentences that have no effect on the functionality and are used for the purpose of enhancing the readability of the code. They are of two types:
   Single Line Comment: This can be created by using the symbol -- and writing what we want to mention as a comment next to it.
   Multi-Line comment: These are the comments that can be specified over multiple lines and the syntax goes like /* comment information */
   Example:
   SET SERVEROUTPUT ON;
   DECLARE

-- Hi There! I am a single line comment.
var_name varchar2(40) := 'I love PL/SQL' ;  
BEGIN
/*
Hi! I am a multi line
comment. I span across
multiple lines
*/
dbms_output.put_line(var_name);
END;
/
Output:
I love PL/SQL
10. What is the purpose of WHEN clause in the trigger?
    WHEN clause specifies for what condition the trigger has to be triggered.

11. Can you explain the PL/SQL execution architecture?
    The PL/SQL engine does the process of compilation and execution of the PL/SQL blocks and programs and can only work if it is installed on an Oracle server or any application tool that supports Oracle such as Oracle Forms.

- PL/SQL is one of the parts of Oracle RDBMS, and it is important to know that most of the Oracle applications are developed using the client-server architecture. The Oracle database forms the server-side and requests to the database form a part of the client-side.
So based on the above fact and the fact that PL/SQL is not a standalone programming language, we must realize that the PL/SQL engine can reside in either the client environment or the server environment. This makes it easy to move PL/SQL modules and sub-programs between server-side and client-side applications.
Based on the architecture shown below, we can understand that PL/SQL engine plays an important role in the process and execute the PL/SQL statements and whenever it encounters the SQL statements, they are sent to the SQL Statement Processor.
- Case 1: PL/SQL engine is on the server: In this case, the whole PL/SQL block gets passed to the PL/SQL engine present on the Oracle server which is then processed and the response is sent.
  Case 2: PL/SQL engine is on the client: Here the engine lies within the Oracle Developer tools and the processing of the PL/SQL statements is done on the client-side.
  In case, there are any SQL statements in the PL/SQL block, then they are sent to the Oracle server for SQL processing.
  When there are no SQL statements, then the whole block processing occurs at the client-side
12. Why is SYSDATE and USER keywords used?
    SYSDATE:
    This keyword returns the current time and date on the local database server.
    The syntax is SYSDATE.
    In order to extract part of the date, we use the TO_CHAR function on SYSDATE and specify the format we need.
    Usage:
    SELECT SYSDATE FROM dual;
    SELECT id, TO_CHAR(SYSDATE, 'yyyy/mm/dd') from InterviewBitEmployeeTable where customer_id < 200;
    USER:
    This keyword returns the user id of the current session.
    Usage:
    SELECT USER FROM dual;
13. Differentiate between implicit cursor and explicit cursor.
    Implicit Cursor 	Explicit Cursor
    An implicit cursor is used when a query returns a single row value.	When a subquery returns more than one row, an explicit cursor is used. These rows are called Active Set.
    This is used for all DML operations like DECLARE, OPEN, FETCH, CLOSE.	This is used to process Multirow SELECT Statements.
    NO_DATA_FOUND Exception is handled here.	NO_DATA_FOUND cannot be handled here.
14. Differentiate between SQL and PL/SQL.
    SQL	PL/SQL
    SQL is a natural language meant for the interactive processing of data in the database.	PL/SQL is a procedural extension of SQL.
    Decision-making and looping are not allowed in SQL.	PL/SQL supports all features of procedural language such as conditional and looping statements.
    All SQL statements are executed at a time by the database server which is why it becomes a time-consuming process.	PL/SQL statements are executed one block at a time thereby reducing the network traffic.
    There is no error handling mechanism in SQL.	This supports an error handling mechanism.
15. What is the importance of %TYPE and %ROWTYPE data types in PL/SQL?
    %TYPE: This declaration is used for the purpose of anchoring by providing the data type of any variable, column, or constant. It is useful during the declaration of a variable that has the same data type as that of its table column.
    Consider the example of declaring a variable named ib_employeeid which has the data type and its size same as that of the column employeeid in table ib_employee.
    The syntax would be : ib_employeeid ib_employee.employeeid%TYPE;
    %ROWTYPE: This is used for declaring a variable that has the same data type and size as that of a row in the table. The row of a table is called a record and its fields would have the same data types and names as the columns defined in the table.
    For example: In order to declare a record named ib_emprecord for storing an entire row in a table called ib_employee, the syntax is:
    ib_emprecord ib_employee%ROWTYPE;

16. What are the various functions available for manipulating the character data?
    The functions that are used for manipulating the character data are called String Functions.
    LEFT: This function returns the specified number of characters from the left part of a string.
    Syntax: LEFT(string_value, numberOfCharacters).
    For example, LEFT(‘InterviewBit’, 9) will return ‘Interview’.
    RIGHT: This function returns the defined number of characters from the right part of a string.
    Syntax: RIGHT(string_value, numberOfCharacters)
    For example, RIGHT(‘InterviewBit’,3) would return ‘Bit’.
    SUBSTRING: This function would select the data from a specified start position through the number of characters defined from any part of the string.
    Syntax: SUBSTRING(string_value, start_position, numberOfCharacters)
    For example, SUBSTRING(‘InterviewBit’,2,4) would return ‘terv’.
    LTRIM: This function would trim all the white spaces on the left part of the string.
    Syntax: LTRIM(string_value)
    For example, LTRIM(’ InterviewBit’) will return ‘InterviewBit’.
    RTRIM: This function would trim all the white spaces on the right part of the string.
    Syntax: RTRIM(string_value)
    For example, RTRIM('InterviewBit ') will return ‘InterviewBit’.
    UPPER: This function is used for converting all the characters to the upper case in a string.
    Syntax: UPPER(string_variable)
    For example, UPPER(‘interviewBit’) would return ‘INTERVIEWBIT’.
    LOWER: This function is used for converting all the characters of a string to lowercase.
    Syntax: LOWER(string_variable)
    For example, LOWER(‘INterviewBit’) would return ‘interviewbit’.
17. What is the difference between ROLLBACK and ROLLBACK TO statements in PL/SQL?
    ROLLBACK command is used for rolling back all the changes from the beginning of the transaction.
    ROLLBACK TO command is used for undoing the transaction only till a SAVEPOINT. The transactions cannot be rolled back before the SAVEPOINT and hence the transaction remains active even before the command is specified
18. What is the use of SYS.ALL_DEPENDENCIES?
    SYS.ALL_DEPENDENCIES is used for describing all the dependencies between procedures, packages, triggers, functions that are accessible to the current user. It returns the columns like name, dependency_type, type, referenced_owner etc.
19. What are the virtual tables available during the execution of the database trigger?
    The THEN and NOW tables are the virtual tables that are available during the database trigger execution. The table columns are referred to as THEN.column and NOW.column respectively.
    Only the NOW.column is available for insert-related triggers.
    Only the THEN.column values are available for the DELETE-related triggers.
    Both the virtual table columns are available for UPDATE triggers.
20. Differentiate between the cursors declared in procedures and the cursors declared in the package specifications.
    The cursors that are declared in the procedures will have the local scope and hence they cannot be used by other procedures.
    The cursors that are declared in package specifications are treated with global scope and hence they can be used and accessed by other procedures
21. What are COMMIT, ROLLBACK and SAVEPOINT statements in PL/SQL?
    These are the three transaction specifications that are available in PL/SQL.
    COMMIT: Whenever any DML operations are performed, the data gets manipulated only in the database buffer and not the actual database. In order to save these DML transactions to the database, there is a need to COMMIT these transactions.
    COMMIT transaction action does saving of all the outstanding changes since the last commit and the below steps take place:
    The release of affected rows.
    The transaction is marked as complete.
    The details of the transaction would be stored in the data dictionary.
    Syntax: COMMIT;
    ROLLBACK: In order to undo or erase the changes that were done in the current transaction, the changes need to be rolled back. ROLLBACK statement erases all the changes since the last COMMIT.
    Syntax: ROLLBACK;
    SAVEPOINT: This statement gives the name and defines a point in the current transaction process where any changes occurring before that SAVEPOINT would be preserved whereas all the changes after that point would be released.
    Syntax: SAVEPOINT <savepoint_name>;
22. How can you debug your PL/SQL code?
    We can use DBMS_OUTPUT and DBMS_DEBUG statements for debugging our code:
    DBMS_OUTPUT prints the output to the standard console.
    DBMS_DEBUG prints the output to the log file.
23. What is the difference between a mutating table and a constraining table?
    A table that is being modified by the usage of the DML statement currently is known as a mutating table. It can also be a table that has triggers defined on it.
    A table used for reading for the purpose of referential integrity constraint is called a constraining table.
24. In what cursor attributes the outcomes of DML statement execution are saved?
    The outcomes of the execution of the DML statement is saved in the following 4 cursor attributes:
    SQL%FOUND: This returns TRUE if at least one row has been processed.
    SQL%NOTFOUND: This returns TRUE if no rows were processed.
    SQL%ISOPEN: This checks whether the cursor is open or not and returns TRUE if open.
    SQL%ROWCOUNT: This returns the number of rows processed by the DML statement
25. Is it possible to declare column which has the number data type and its scale larger than the precision? For example defining columns like: column name NUMBER (10,100), column name NUMBER (10,-84)
    Yes, these type of declarations are possible.
    Number (9, 12) indicates that there are 12 digits after decimal point. But since the maximum precision is 9, the rest are 0 padded like 0.000999999999.
    Number (9, -12) indicates there are 21 digits before the decimal point and out of that there are 9 possible digits and the rest are 0 padded like 999999999000000000000.0
26. Write a PL/SQL program using WHILE loop for calculating the average of the numbers entered by user. Stop the entry of numbers whenever the user enters the number 0.
    DECLARE
    n NUMBER;
    average NUMBER :=0 ;
    sum NUMBER :=0 ;
    count NUMBER :=0 ;
    BEGIN
    -- Take input from user
    n := &input_number;
    WHILE(n<>0)
    LOOP
    -- Increment count to find total elements
    count := count+1;
    -- Sum of elements entered
    sum := sum+n;
    -- Take input from user
    n := &input_number;
    END LOOP;
    -- Average calculation
    average := sum/count;
    DBMS_OUTPUT.PUT_LINE(‘Average of entered numbers is ’||average);
    END;
27. Write a PL/SQL procedure for selecting some records from the database using some parameters as filters.
    Consider that we are fetching details of employees from ib_employee table where salary is a parameter for filter.
    CREATE PROCEDURE get_employee_details @salary nvarchar(30)
    AS
    BEGIN
    SELECT * FROM ib_employee WHERE salary = @salary;
    END;
28. Write a PL/SQL code to count the number of Sundays between the two inputted dates.
    --declare 2 dates of type Date
    DECLARE
    start_date Date;
    end_date Date;
    sundays_count Number:=0;
    BEGIN
    -- input 2 dates
    start_date:='&input_start_date';
    end_date:='&input_end_date';
    /*
    Returns the date of the first day after the mentioned date
    and matching the day specified in second parameter.
    */
    start_date:=NEXT_DAY(start_date-1, 'SUNDAY');
    --check the condition of dates by using while loop.
    while(start_date<=end_date)
    LOOP
    sundays_count:=sundays_count+1;
    start_date:=start_date+7;
    END LOOP;

-- print the count of sundays
dbms_output.put_line('Total number of Sundays between the two dates:'||sundays_count);
END;
/
Input:
start_date = ‘01-SEP-19’
end_date = ‘29-SEP-19’

Output:
Total number of Sundays between the two dates: 5

29. Write PL/SQL code block to increment the employee’s salary by 1000 whose employee_id is 102 from the given table below.
    EMPLOYEE_ID	FIRST_NAME	LAST_NAME	EMAIL_ID	PHONE_NUMBER	JOIN_DATE	JOB_ID 	SALARY
    100	ABC	DEF	abef	9876543210	2020-06-06 	AD_PRES	24000.00
    101	GHI	JKL	ghkl	9876543211 	2021-02-08	AD_VP	17000.00
    102	MNO 	PQR	mnqr	9876543212	2016-05-14	AD_VP	17000.00
    103	STU	VWX	stwx	9876543213	2019-06-24	IT_PROG	9000.00
    DECLARE
    employee_salary  NUMBER(8,2);

PROCEDURE update_salary (
emp        NUMBER,
salary IN OUT NUMBER
) IS
BEGIN
salary := salary + 1000;
END;

BEGIN
SELECT salary INTO employee_salary
FROM ib_employee
WHERE employee_id = 102;

DBMS_OUTPUT.PUT_LINE
('Before update_salary procedure, salary is: ' || employee_salary);

update_salary (100, employee_salary);

DBMS_OUTPUT.PUT_LINE
('After update_salary procedure, salary is: ' || employee_salary);
END;
/
Result:

Before update_salary procedure, salary is: 17000
After update_salary procedure, salary is: 18000
30. Write a PL/SQL code to find whether a given string is palindrome or not.
    DECLARE
    -- Declared variables string, letter, reverse_string where string is the original string.
    string VARCHAR2(10) := 'abccba';
    letter VARCHAR2(20);
    reverse_string VARCHAR2(10);
    BEGIN
    FOR i IN REVERSE 1..LENGTH(string) LOOP
    letter := SUBSTR(string, i, 1);
    -- concatenate letter to reverse_string variable
    reverse_string := reverse_string ||''||letter;
    END LOOP;
    IF reverse_string = string THEN
    dbms_output.Put_line(reverse_string||''||' is palindrome');
    ELSE
    dbms_output.Put_line(reverse_string ||'' ||' is not palindrome');
    END IF;
    END;

31. Write PL/SQL program to convert each digit of a given number into its corresponding word format.
    DECLARE
    -- declare necessary variables
    -- num represents the given number
    -- number_to_word represents the word format of the number
    -- str, len and digit are the intermediate variables used for program execution
    num   INTEGER;
    number_to_word VARCHAR2(100);
    digit_str   VARCHAR2(100);
    len   INTEGER;
    digit   INTEGER;
    BEGIN
    num := 123456;
    len := LENGTH(num);
    dbms_output.PUT_LINE('Input: ' ||num);
    -- Iterate through the number one by one
    FOR i IN 1..len LOOP
    digit := SUBSTR(num, i, 1);
    -- Using DECODE, get the str representation of the digit
    SELECT Decode(digit, 0, 'Zero ',
    1, 'One ',
    2, 'Two ',
    3, 'Three ',
    4, 'Four ',
    5, 'Five ',
    6, 'Six ',
    7, 'Seven ',
    8, 'Eight ',
    9, 'Nine ')
    INTO digit_str
    FROM dual;
    -- Append the str representation of digit to final result.
    number_to_word := number_to_word || digit_str;
    END LOOP;
    dbms_output.PUT_LINE('Output: ' ||number_to_word);
    END;
    Input: 12345
    Output: One Two Three Four Five

32. Write PL/SQL program to find the sum of digits of a number.
    DECLARE
    --Declare variables num, sum_of_digits and remainder of datatype Integer
    num  INTEGER;
    sum_of_digits INTEGER;
    remainder  INTEGER;
    BEGIN
    num := 123456;
    sum_of_digits := 0;
    -- Find the sum of digits until original number doesnt become null
    WHILE num <> 0 LOOP
    remainder := MOD(num, 10);
    sum_of_digits := sum_of_digits + remainder;
    num := TRUNC(num / 10);
    END LOOP;
    dbms_output.PUT_LINE('Sum of digits is '|| sum_of_digits);
    END;
    Input: 9874
    Output: 28





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




#### part 8









#### part 9










#### part 10


### references
- https://en.wikibooks.org/wiki/Oracle_Database/SQL_Cheatsheet
- https://www.pcwdld.com/sql-cheat-sheet#wbounce-modal
- https://s3-us-west-2.amazonaws.com/citp/oracle_sql_function_cheat_sheet.pdf
- https://intellipaat.com/mediaFiles/2019/02/SQL-Basic-Cheat-Sheet.pdf
- https://www.interviewbit.com/sql-interview-questions/
- https://www.interviewbit.com/mysql-interview-questions/
- https://www.interviewbit.com/pl-sql-interview-questions/
- https://www.interviewbit.com/blog/sql-vs-mysql/
- https://www.interviewbit.com/blog/postgresql-vs-mysql/
- https://www.interviewbit.com/blog/sql-vs-nosql/