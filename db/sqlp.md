# Devopssec
## databases
### PostgreSQL

#### PostgreSQL CS 

#### PostgreSQL QA
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

