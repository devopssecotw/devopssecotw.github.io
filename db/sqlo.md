# Devopssec
## databases
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

