# Devopssec
## databases
### MyBatis 
#### p

Installation
To use MyBatis you just need to include the mybatis-x.x.x.jar file in the classpath.

If you are using Maven just add the following dependency to your pom.xml:

<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis</artifactId>
  <version>x.x.x</version>
</dependency>
Building SqlSessionFactory from XML
Every MyBatis application centers around an instance of SqlSessionFactory. A SqlSessionFactory instance can be acquired by using the SqlSessionFactoryBuilder. SqlSessionFactoryBuilder can build a SqlSessionFactory instance from an XML configuration file, or from a custom prepared instance of the Configuration class.

Building a SqlSessionFactory instance from an XML file is very simple. It is recommended that you use a classpath resource for this configuration, but you could use any InputStream instance, including one created from a literal file path or a file:// URL. MyBatis includes a utility class, called Resources, that contains a number of methods that make it simpler to load resources from the classpath and other locations.

String resource = "org/mybatis/example/mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory =
new SqlSessionFactoryBuilder().build(inputStream);
The configuration XML file contains settings for the core of the MyBatis system, including a DataSource for acquiring database Connection instances, as well as a TransactionManager for determining how transactions should be scoped and controlled. The full details of the XML configuration file can be found later in this document, but here is a simple example:

<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
      </dataSource>
    </environment>
  </environments>
  <mappers>
    <mapper resource="org/mybatis/example/BlogMapper.xml"/>
  </mappers>
</configuration>
While there is a lot more to the XML configuration file, the above example points out the most critical parts. Notice the XML header, required to validate the XML document. The body of the environment element contains the environment configuration for transaction management and connection pooling. The mappers element contains a list of mappers – the XML files and/or annotated Java interface classes that contain the SQL code and mapping definitions.

Building SqlSessionFactory without XML
If you prefer to directly build the configuration from Java, rather than XML, or create your own configuration builder, MyBatis provides a complete Configuration class that provides all of the same configuration options as the XML file.

DataSource dataSource = BlogDataSourceFactory.getBlogDataSource();
TransactionFactory transactionFactory =
new JdbcTransactionFactory();
Environment environment =
new Environment("development", transactionFactory, dataSource);
Configuration configuration = new Configuration(environment);
configuration.addMapper(BlogMapper.class);
SqlSessionFactory sqlSessionFactory =
new SqlSessionFactoryBuilder().build(configuration);
Notice in this case the configuration is adding a mapper class. Mapper classes are Java classes that contain SQL Mapping Annotations that avoid the need for XML. However, due to some limitations of Java Annotations and the complexity of some MyBatis mappings, XML mapping is still required for the most advanced mappings (e.g. Nested Join Mapping). For this reason, MyBatis will automatically look for and load a peer XML file if it exists (in this case, BlogMapper.xml would be loaded based on the classpath and name of BlogMapper.class). More on this later.

Acquiring a SqlSession from SqlSessionFactory
Now that you have a SqlSessionFactory, as the name suggests, you can acquire an instance of SqlSession. The SqlSession contains absolutely every method needed to execute SQL commands against the database. You can execute mapped SQL statements directly against the SqlSession instance. For example:

try (SqlSession session = sqlSessionFactory.openSession()) {
Blog blog = session.selectOne(
"org.mybatis.example.BlogMapper.selectBlog", 101);
}
While this approach works, and is familiar to users of previous versions of MyBatis, there is now a cleaner approach. Using an interface (e.g. BlogMapper.class) that properly describes the parameter and return value for a given statement, you can now execute cleaner and more type safe code, without error prone string literals and casting.

For example:

try (SqlSession session = sqlSessionFactory.openSession()) {
BlogMapper mapper = session.getMapper(BlogMapper.class);
Blog blog = mapper.selectBlog(101);
}
Now let's explore what exactly is being executed here.

Exploring Mapped SQL Statements
At this point you may be wondering what exactly is being executed by the SqlSession or Mapper class. The topic of Mapped SQL Statements is a big one, and that topic will likely dominate the majority of this documentation. But to give you an idea of what exactly is being run, here are a couple of examples.

In either of the examples above, the statements could have been defined by either XML or Annotations. Let's take a look at XML first. The full set of features provided by MyBatis can be realized by using the XML based mapping language that has made MyBatis popular over the years. If you've used MyBatis before, the concept will be familiar to you, but there have been numerous improvements to the XML mapping documents that will become clear later. Here is an example of an XML based mapped statement that would satisfy the above SqlSession calls.

<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.mybatis.example.BlogMapper">
  <select id="selectBlog" resultType="Blog">
    select * from Blog where id = #{id}
  </select>
</mapper>
While this looks like a lot of overhead for this simple example, it is actually very light. You can define as many mapped statements in a single mapper XML file as you like, so you get a lot of mileage out of the XML header and doctype declaration. The rest of the file is pretty self explanatory. It defines a name for the mapped statement “selectBlog”, in the namespace “org.mybatis.example.BlogMapper”, which would allow you to call it by specifying the fully qualified name of “org.mybatis.example.BlogMapper.selectBlog”, as we did above in the following example:

Blog blog = session.selectOne(
"org.mybatis.example.BlogMapper.selectBlog", 101);
Notice how similar this is to calling a method on a fully qualified Java class, and there's a reason for that. This name can be directly mapped to a Mapper class of the same name as the namespace, with a method that matches the name, parameter, and return type as the mapped select statement. This allows you to very simply call the method against the Mapper interface as you saw above, but here it is again in the following example:

BlogMapper mapper = session.getMapper(BlogMapper.class);
Blog blog = mapper.selectBlog(101);
The second approach has a lot of advantages. First, it doesn't depend on a string literal, so it's much safer. Second, if your IDE has code completion, you can leverage that when navigating your mapped SQL statements.

NOTE A note about namespaces.

Namespaces were optional in previous versions of MyBatis, which was confusing and unhelpful. Namespaces are now required and have a purpose beyond simply isolating statements with longer, fully-qualified names.

Namespaces enable the interface bindings as you see here, and even if you don’t think you’ll use them today, you should follow these practices laid out here in case you change your mind. Using the namespace once, and putting it in a proper Java package namespace will clean up your code and improve the usability of MyBatis in the long term.

Name Resolution: To reduce the amount of typing, MyBatis uses the following name resolution rules for all named configuration elements, including statements, result maps, caches, etc.

Fully qualified names (e.g. “com.mypackage.MyMapper.selectAllThings”) are looked up directly and used if found.
Short names (e.g. “selectAllThings”) can be used to reference any unambiguous entry. However if there are two or more (e.g. “com.foo.selectAllThings and com.bar.selectAllThings”), then you will receive an error reporting that the short name is ambiguous and therefore must be fully qualified.
There's one more trick to Mapper classes like BlogMapper. Their mapped statements don't need to be mapped with XML at all. Instead they can use Java Annotations. For example, the XML above could be eliminated and replaced with:

package org.mybatis.example;
public interface BlogMapper {
@Select("SELECT * FROM blog WHERE id = #{id}")
Blog selectBlog(int id);
}
The annotations are a lot cleaner for simple statements, however, Java Annotations are both limited and messier for more complicated statements. Therefore, if you have to do anything complicated, you're better off with XML mapped statements.

It will be up to you and your project team to determine which is right for you, and how important it is to you that your mapped statements be defined in a consistent way. That said, you're never locked into a single approach. You can very easily migrate Annotation based Mapped Statements to XML and vice versa.

Scope and Lifecycle
It's very important to understand the various scopes and lifecycles classes we've discussed so far. Using them incorrectly can cause severe concurrency problems.

NOTE Object lifecycle and Dependency Injection Frameworks

Dependency Injection frameworks can create thread safe, transactional SqlSessions and mappers and inject them directly into your beans so you can just forget about their lifecycle. You may want to have a look at MyBatis-Spring or MyBatis-Guice sub-projects to know more about using MyBatis with DI frameworks.

SqlSessionFactoryBuilder
This class can be instantiated, used and thrown away. There is no need to keep it around once you've created your SqlSessionFactory. Therefore the best scope for instances of SqlSessionFactoryBuilder is method scope (i.e. a local method variable). You can reuse the SqlSessionFactoryBuilder to build multiple SqlSessionFactory instances, but it's still best not to keep it around to ensure that all of the XML parsing resources are freed up for more important things.

SqlSessionFactory
Once created, the SqlSessionFactory should exist for the duration of your application execution. There should be little or no reason to ever dispose of it or recreate it. It's a best practice to not rebuild the SqlSessionFactory multiple times in an application run. Doing so should be considered a “bad smell”. Therefore the best scope of SqlSessionFactory is application scope. This can be achieved a number of ways. The simplest is to use a Singleton pattern or Static Singleton pattern.

SqlSession
Each thread should have its own instance of SqlSession. Instances of SqlSession are not to be shared and are not thread safe. Therefore the best scope is request or method scope. Never keep references to a SqlSession instance in a static field or even an instance field of a class. Never keep references to a SqlSession in any sort of managed scope, such as HttpSession of the Servlet framework. If you're using a web framework of any sort, consider the SqlSession to follow a similar scope to that of an HTTP request. In other words, upon receiving an HTTP request, you can open a SqlSession, then upon returning the response, you can close it. Closing the session is very important. You should always ensure that it's closed within a finally block. The following is the standard pattern for ensuring that SqlSessions are closed:

try (SqlSession session = sqlSessionFactory.openSession()) {
// do work
}
Using this pattern consistently throughout your code will ensure that all database resources are properly closed.

Mapper Instances
Mappers are interfaces that you create to bind to your mapped statements. Instances of the mapper interfaces are acquired from the SqlSession. As such, technically the broadest scope of any mapper instance is the same as the SqlSession from which they were requested. However, the best scope for mapper instances is method scope. That is, they should be requested within the method that they are used, and then be discarded. They do not need to be closed explicitly. While it's not a problem to keep them around throughout a request, similar to the SqlSession, you might find that managing too many resources at this level will quickly get out of hand. Keep it simple, keep Mappers in the method scope. The following example demonstrates this practice.

try (SqlSession session = sqlSessionFactory.openSession()) {
BlogMapper mapper = session.getMapper(BlogMapper.class);
// do work
}

#### p

Mapper XML Files
The true power of MyBatis is in the Mapped Statements. This is where the magic happens. For all of their power, the Mapper XML files are relatively simple. Certainly if you were to compare them to the equivalent JDBC code, you would immediately see a savings of 95% of the code. MyBatis was built to focus on the SQL, and does its best to stay out of your way.

The Mapper XML files have only a few first class elements (in the order that they should be defined):

cache – Configuration of the cache for a given namespace.
cache-ref – Reference to a cache configuration from another namespace.
resultMap – The most complicated and powerful element that describes how to load your objects from the database result sets.
parameterMap – Deprecated! Old-school way to map parameters. Inline parameters are preferred and this element may be removed in the future. Not documented here.
sql – A reusable chunk of SQL that can be referenced by other statements.
insert – A mapped INSERT statement.
update – A mapped UPDATE statement.
delete – A mapped DELETE statement.
select – A mapped SELECT statement.
The next sections will describe each of these elements in detail, starting with the statements themselves.

select
The select statement is one of the most popular elements that you'll use in MyBatis. Putting data in a database isn't terribly valuable until you get it back out, so most applications query far more than they modify the data. For every insert, update or delete, there are probably many selects. This is one of the founding principles of MyBatis, and is the reason so much focus and effort was placed on querying and result mapping. The select element is quite simple for simple cases. For example:

<select id="selectPerson" parameterType="int" resultType="hashmap">
  SELECT * FROM PERSON WHERE ID = #{id}
</select>
This statement is called selectPerson, takes a parameter of type int (or Integer), and returns a HashMap keyed by column names mapped to row values.

Notice the parameter notation:

#{id}
This tells MyBatis to create a PreparedStatement parameter. With JDBC, such a parameter would be identified by a "?" in SQL passed to a new PreparedStatement, something like this:

// Similar JDBC code, NOT MyBatis…
String selectPerson = "SELECT * FROM PERSON WHERE ID=?";
PreparedStatement ps = conn.prepareStatement(selectPerson);
ps.setInt(1,id);
Of course, there's a lot more code required by JDBC alone to extract the results and map them to an instance of an object, which is what MyBatis saves you from having to do. There's a lot more to know about parameter and result mapping. Those details warrant their own section, which follows later in this section.

The select element has more attributes that allow you to configure the details of how each statement should behave.

<select
id="selectPerson"
parameterType="int"
parameterMap="deprecated"
resultType="hashmap"
resultMap="personResultMap"
flushCache="false"
useCache="true"
timeout="10"
fetchSize="256"
statementType="PREPARED"
resultSetType="FORWARD_ONLY">
Select Attributes
Attribute	Description
id	A unique identifier in this namespace that can be used to reference this statement.
parameterType	The fully qualified class name or alias for the parameter that will be passed into this statement. This attribute is optional because MyBatis can calculate the TypeHandler to use out of the actual parameter passed to the statement. Default is unset.
parameterMap	This is a deprecated approach to referencing an external parameterMap. Use inline parameter mappings and the parameterType attribute.
resultType	The fully qualified class name or alias for the expected type that will be returned from this statement. Note that in the case of collections, this should be the type that the collection contains, not the type of the collection itself. Use resultType OR resultMap, not both.
resultMap	A named reference to an external resultMap. Result maps are the most powerful feature of MyBatis, and with a good understanding of them, many difficult mapping cases can be solved. Use resultMap OR resultType, not both.
flushCache	Setting this to true will cause the local and 2nd level caches to be flushed whenever this statement is called. Default: false for select statements.
useCache	Setting this to true will cause the results of this statement to be cached in 2nd level cache. Default: true for select statements.
timeout	This sets the number of seconds the driver will wait for the database to return from a request, before throwing an exception. Default is unset (driver dependent).
fetchSize	This is a driver hint that will attempt to cause the driver to return results in batches of rows numbering in size equal to this setting. Default is unset (driver dependent).
statementType	Any one of STATEMENT, PREPARED or CALLABLE. This causes MyBatis to use Statement, PreparedStatement or CallableStatement respectively. Default: PREPARED.
resultSetType	Any one of FORWARD_ONLY|SCROLL_SENSITIVE|SCROLL_INSENSITIVE|DEFAULT(same as unset). Default is unset (driver dependent).
databaseId	In case there is a configured databaseIdProvider, MyBatis will load all statements with no databaseId attribute or with a databaseId that matches the current one. If case the same statement if found with and without the databaseId the latter will be discarded.
resultOrdered	This is only applicable for nested result select statements: If this is true, it is assumed that nested results are contained or grouped together such that when a new main result row is returned, no references to a previous result row will occur anymore. This allows nested results to be filled much more memory friendly. Default: false.
resultSets	This is only applicable for multiple result sets. It lists the result sets that will be returned by the statement and gives a name to each one. Names are separated by commas.
insert, update and delete
The data modification statements insert, update and delete are very similar in their implementation:

<insert
id="insertAuthor"
parameterType="domain.blog.Author"
flushCache="true"
statementType="PREPARED"
keyProperty=""
keyColumn=""
useGeneratedKeys=""
timeout="20">

<update
id="updateAuthor"
parameterType="domain.blog.Author"
flushCache="true"
statementType="PREPARED"
timeout="20">

<delete
id="deleteAuthor"
parameterType="domain.blog.Author"
flushCache="true"
statementType="PREPARED"
timeout="20">
Insert, Update and Delete Attributes
Attribute	Description
id	A unique identifier in this namespace that can be used to reference this statement.
parameterType	The fully qualified class name or alias for the parameter that will be passed into this statement. This attribute is optional because MyBatis can calculate the TypeHandler to use out of the actual parameter passed to the statement. Default is unset.
parameterMap	This is a deprecated approach to referencing an external parameterMap. Use inline parameter mappings and the parameterType attribute.
flushCache	Setting this to true will cause the 2nd level and local caches to be flushed whenever this statement is called. Default: true for insert, update and delete statements.
timeout	This sets the maximum number of seconds the driver will wait for the database to return from a request, before throwing an exception. Default is unset (driver dependent).
statementType	Any one of STATEMENT, PREPARED or CALLABLE. This causes MyBatis to use Statement, PreparedStatement or CallableStatement respectively. Default: PREPARED.
useGeneratedKeys	(insert and update only) This tells MyBatis to use the JDBC getGeneratedKeys method to retrieve keys generated internally by the database (e.g. auto increment fields in RDBMS like MySQL or SQL Server). Default: false.
keyProperty	(insert and update only) Identifies a property into which MyBatis will set the key value returned by getGeneratedKeys, or by a selectKey child element of the insert statement. Default: unset. Can be a comma separated list of property names if multiple generated columns are expected.
keyColumn	(insert and update only) Sets the name of the column in the table with a generated key. This is only required in certain databases (like PostgreSQL) when the key column is not the first column in the table. Can be a comma separated list of columns names if multiple generated columns are expected.
databaseId	In case there is a configured databaseIdProvider, MyBatis will load all statements with no databaseId attribute or with a databaseId that matches the current one. If case the same statement if found with and without the databaseId the latter will be discarded.
The following are some examples of insert, update and delete statements.

<insert id="insertAuthor">
  insert into Author (id,username,password,email,bio)
  values (#{id},#{username},#{password},#{email},#{bio})
</insert>

<update id="updateAuthor">
  update Author set
    username = #{username},
    password = #{password},
    email = #{email},
    bio = #{bio}
  where id = #{id}
</update>

<delete id="deleteAuthor">
  delete from Author where id = #{id}
</delete>
As mentioned, insert is a little bit more rich in that it has a few extra attributes and sub-elements that allow it to deal with key generation in a number of ways.

First, if your database supports auto-generated key fields (e.g. MySQL and SQL Server), then you can simply set useGeneratedKeys="true" and set the keyProperty to the target property and you're done. For example, if the Author table above had used an auto-generated column type for the id, the statement would be modified as follows:

<insert id="insertAuthor" useGeneratedKeys="true"
eeyProperty="id">
insert into Author (username,password,email,bio)
values (#{username},#{password},#{email},#{bio})
</insert>
If your database also supports multi-row insert, you can pass a list or an array of Authors and retrieve the auto-generated keys.

<insert id="insertAuthor" useGeneratedKeys="true"
keyProperty="id">
insert into Author (username, password, email, bio) values
<foreach item="item" collection="list" separator=",">
(#{item.username}, #{item.password}, #{item.email}, #{item.bio})
</foreach>
</insert>
MyBatis has another way to deal with key generation for databases that don't support auto-generated column types, or perhaps don't yet support the JDBC driver support for auto-generated keys.

Here's a simple (silly) example that would generate a random ID (something you'd likely never do, but this demonstrates the flexibility and how MyBatis really doesn't mind):

<insert id="insertAuthor">
  <selectKey keyProperty="id" resultType="int" order="BEFORE">
    select CAST(RANDOM()*1000000 as INTEGER) a from SYSIBM.SYSDUMMY1
  </selectKey>
  insert into Author
    (id, username, password, email,bio, favourite_section)
  values
    (#{id}, #{username}, #{password}, #{email}, #{bio}, #{favouriteSection,jdbcType=VARCHAR})
</insert>
In the example above, the selectKey statement would be run first, the Author id property would be set, and then the insert statement would be called. This gives you a similar behavior to an auto-generated key in your database without complicating your Java code.

The selectKey element is described as follows:

<selectKey
keyProperty="id"
resultType="int"
order="BEFORE"
statementType="PREPARED">
selectKey Attributes
Attribute	Description
keyProperty	The target property where the result of the selectKey statement should be set. Can be a comma separated list of property names if multiple generated columns are expected.
keyColumn	The column name(s) in the returned result set that match the properties. Can be a comma separated list of column names if multiple generated columns are expected.
resultType	The type of the result. MyBatis can usually figure this out, but it doesn't hurt to add it to be sure. MyBatis allows any simple type to be used as the key, including Strings. If you are expecting multiple generated columns, then you can use an Object that contains the expected properties, or a Map.
order	This can be set to BEFORE or AFTER. If set to BEFORE, then it will select the key first, set the keyProperty and then execute the insert statement. If set to AFTER, it runs the insert statement and then the selectKey statement – which is common with databases like Oracle that may have embedded sequence calls inside of insert statements.
statementType	Same as above, MyBatis supports STATEMENT, PREPARED and CALLABLE statement types that map to Statement, PreparedStatement and CallableStatement respectively.
sql
This element can be used to define a reusable fragment of SQL code that can be included in other statements. It can be statically (during load phase) parametrized. Different property values can vary in include instances. For example:

<sql id="userColumns"> ${alias}.id,${alias}.username,${alias}.password </sql>
The SQL fragment can then be included in another statement, for example:

<select id="selectUsers" resultType="map">
  select
    <include refid="userColumns"><property name="alias" value="t1"/></include>,
    <include refid="userColumns"><property name="alias" value="t2"/></include>
  from some_table t1
    cross join some_table t2
</select>
Property value can be also used in include refid attribute or property values inside include clause, for example:

<sql id="sometable">
  ${prefix}Table
</sql>

<sql id="someinclude">
  from
    <include refid="${include_target}"/>
</sql>

<select id="select" resultType="map">
  select
    field1, field2, field3
  <include refid="someinclude">
    <property name="prefix" value="Some"/>
    <property name="include_target" value="sometable"/>
  </include>
</select>
Parameters
In all of the past statements, you've seen examples of simple parameters. Parameters are very powerful elements in MyBatis. For simple situations, probably 90% of the cases, there's not much to them, for example:

<select id="selectUsers" resultType="User">
  select id, username, password
  from users
  where id = #{id}
</select>
The example above demonstrates a very simple named parameter mapping. The parameterType is set to int, so therefore the parameter could be named anything. Primitive or simple data types such as Integer and String have no relevant properties, and thus will replace the full value of the parameter entirely. However, if you pass in a complex object, then the behavior is a little different. For example:

<insert id="insertUser" parameterType="User">
  insert into users (id, username, password)
  values (#{id}, #{username}, #{password})
</insert>
If a parameter object of type User was passed into that statement, the id, username and password property would be looked up and their values passed to a PreparedStatement parameter.

That's nice and simple for passing parameters into statements. But there are a lot of other features of parameter maps.

First, like other parts of MyBatis, parameters can specify a more specific data type.

#{property,javaType=int,jdbcType=NUMERIC}
Like the rest of MyBatis, the javaType can almost always be determined from the parameter object, unless that object is a HashMap. Then the javaType should be specified to ensure the correct TypeHandler is used.

NOTE The JDBC Type is required by JDBC for all nullable columns, if null is passed as a value. You can investigate this yourself by reading the JavaDocs for the PreparedStatement.setNull() method.

To further customize type handling, you can also specify a specific TypeHandler class (or alias), for example:

#{age,javaType=int,jdbcType=NUMERIC,typeHandler=MyTypeHandler}
So already it seems to be getting verbose, but the truth is that you'll rarely set any of these.

For numeric types there's also a numericScale for determining how many decimal places are relevant.

#{height,javaType=double,jdbcType=NUMERIC,numericScale=2}
Finally, the mode attribute allows you to specify IN, OUT or INOUT parameters. If a parameter is OUT or INOUT, the actual value of the parameter object property will be changed, just as you would expect if you were calling for an output parameter. If the mode=OUT (or INOUT) and the jdbcType=CURSOR (i.e. Oracle REFCURSOR), you must specify a resultMap to map the ResultSet to the type of the parameter. Note that the javaType attribute is optional here, it will be automatically set to ResultSet if left blank with a CURSOR as the jdbcType.

#{department, mode=OUT, jdbcType=CURSOR, javaType=ResultSet, resultMap=departmentResultMap}
MyBatis also supports more advanced data types such as structs, but you must tell the statement the type name when registering the out parameter. For example (again, don't break lines like this in practice):

#{middleInitial, mode=OUT, jdbcType=STRUCT, jdbcTypeName=MY_TYPE, resultMap=departmentResultMap}
Despite all of these powerful options, most of the time you'll simply specify the property name, and MyBatis will figure out the rest. At most, you'll specify the jdbcType for nullable columns.

#{firstName}
#{middleInitial,jdbcType=VARCHAR}
#{lastName}
String Substitution
By default, using the #{} syntax will cause MyBatis to generate PreparedStatement properties and set the values safely against the PreparedStatement parameters (e.g. ?). While this is safer, faster and almost always preferred, sometimes you just want to directly inject an unmodified string into the SQL Statement. For example, for ORDER BY, you might use something like this:

ORDER BY ${columnName}
Here MyBatis won't modify or escape the string.

String Substitution can be very useful when the metadata(i.e. table name or column name) in the sql statement is dynamic, for example, if you want to select from a table by any one of its columns, instead of writing code like:

@Select("select * from user where id = #{id}")
User findById(@Param("id") long id);

@Select("select * from user where name = #{name}")
User findByName(@Param("name") String name);

@Select("select * from user where email = #{email}")
User findByEmail(@Param("email") String email);

// and more "findByXxx" method
you can just write:
@Select("select * from user where ${column} = #{value}")
User findByColumn(@Param("column") String column, @Param("value") String value);
in which the ${column} will be substituted directly and the #{value} will be "prepared". Thus you can just do the same work by:
User userOfId1 = userMapper.findByColumn("id", 1L);
User userOfNameKid = userMapper.findByColumn("name", "kid");
User userOfEmail = userMapper.findByColumn("email", "noone@nowhere.com");
This idea can be applied to substitute the table name as well.

NOTE It's not safe to accept input from a user and supply it to a statement unmodified in this way. This leads to potential SQL Injection attacks and therefore you should either disallow user input in these fields, or always perform your own escapes and checks.

Result Maps
The resultMap element is the most important and powerful element in MyBatis. It's what allows you to do away with 90% of the code that JDBC requires to retrieve data from ResultSets, and in some cases allows you to do things that JDBC does not even support. In fact, to write the equivalent code for something like a join mapping for a complex statement could probably span thousands of lines of code. The design of the ResultMaps is such that simple statements don't require explicit result mappings at all, and more complex statements require no more than is absolutely necessary to describe the relationships.

You've already seen examples of simple mapped statements that don't have an explicit resultMap. For example:

<select id="selectUsers" resultType="map">
  select id, username, hashedPassword
  from some_table
  where id = #{id}
</select>
Such a statement simply results in all columns being automatically mapped to the keys of a HashMap, as specified by the resultType attribute. While useful in many cases, a HashMap doesn't make a very good domain model. It's more likely that your application will use JavaBeans or POJOs (Plain Old Java Objects) for the domain model. MyBatis supports both. Consider the following JavaBean:

package com.someapp.model;
public class User {
private int id;
private String username;
private String hashedPassword;

public int getId() {
return id;
}
public void setId(int id) {
this.id = id;
}
public String getUsername() {
return username;
}
public void setUsername(String username) {
this.username = username;
}
public String getHashedPassword() {
return hashedPassword;
}
public void setHashedPassword(String hashedPassword) {
this.hashedPassword = hashedPassword;
}
}
Based on the JavaBeans specification, the above class has 3 properties: id, username, and hashedPassword. These match up exactly with the column names in the select statement.

Such a JavaBean could be mapped to a ResultSet just as easily as the HashMap.

<select id="selectUsers" resultType="com.someapp.model.User">
  select id, username, hashedPassword
  from some_table
  where id = #{id}
</select>
And remember that TypeAliases are your friends. Use them so that you don't have to keep typing the fully qualified path of your class out. For example:

<!-- In Config XML file -->
<typeAlias type="com.someapp.model.User" alias="User"/>

<!-- In SQL Mapping XML file -->
<select id="selectUsers" resultType="User">
  select id, username, hashedPassword
  from some_table
  where id = #{id}
</select>
In these cases MyBatis is automatically creating a ResultMap behind the scenes to auto-map the columns to the JavaBean properties based on name. If the column names did not match exactly, you could employ select clause aliases (a standard SQL feature) on the column names to make the labels match. For example:

<select id="selectUsers" resultType="User">
  select
    user_id             as "id",
    user_name           as "userName",
    hashed_password     as "hashedPassword"
  from some_table
  where id = #{id}
</select>
The great thing about ResultMaps is that you've already learned a lot about them, but you haven't even seen one yet! These simple cases don't require any more than you've seen here. Just for example sake, let's see what this last example would look like as an external resultMap, as that is another way to solve column name mismatches.

<resultMap id="userResultMap" type="User">
  <id property="id" column="user_id" />
  <result property="username" column="user_name"/>
  <result property="password" column="hashed_password"/>
</resultMap>
And the statement that references it uses the resultMap attribute to do so (notice we removed the resultType attribute). For example:

<select id="selectUsers" resultMap="userResultMap">
  select user_id, user_name, hashed_password
  from some_table
  where id = #{id}
</select>
Now if only the world was always that simple.

Advanced Result Maps
MyBatis was created with one idea in mind: Databases aren't always what you want or need them to be. While we'd love every database to be perfect 3rd normal form or BCNF, they aren't. And it would be great if it was possible to have a single database map perfectly to all of the applications that use it, it's not. Result Maps are the answer that MyBatis provides to this problem.

For example, how would we map this statement?

<!-- Very Complex Statement -->
<select id="selectBlogDetails" resultMap="detailedBlogResultMap">
  select
       B.id as blog_id,
       B.title as blog_title,
       B.author_id as blog_author_id,
       A.id as author_id,
       A.username as author_username,
       A.password as author_password,
       A.email as author_email,
       A.bio as author_bio,
       A.favourite_section as author_favourite_section,
       P.id as post_id,
       P.blog_id as post_blog_id,
       P.author_id as post_author_id,
       P.created_on as post_created_on,
       P.section as post_section,
       P.subject as post_subject,
       P.draft as draft,
       P.body as post_body,
       C.id as comment_id,
       C.post_id as comment_post_id,
       C.name as comment_name,
       C.comment as comment_text,
       T.id as tag_id,
       T.name as tag_name
  from Blog B
       left outer join Author A on B.author_id = A.id
       left outer join Post P on B.id = P.blog_id
       left outer join Comment C on P.id = C.post_id
       left outer join Post_Tag PT on PT.post_id = P.id
       left outer join Tag T on PT.tag_id = T.id
  where B.id = #{id}
</select>
You'd probably want to map it to an intelligent object model consisting of a Blog that was written by an Author, and has many Posts, each of which may have zero or many Comments and Tags. The following is a complete example of a complex ResultMap (assume Author, Blog, Post, Comments and Tags are all type aliases). Have a look at it, but don't worry, we're going to go through each step. While it may look daunting at first, it's actually very simple.

<!-- Very Complex Result Map -->
<resultMap id="detailedBlogResultMap" type="Blog">
  <constructor>
    <idArg column="blog_id" javaType="int"/>
  </constructor>
  <result property="title" column="blog_title"/>
  <association property="author" javaType="Author">
    <id property="id" column="author_id"/>
    <result property="username" column="author_username"/>
    <result property="password" column="author_password"/>
    <result property="email" column="author_email"/>
    <result property="bio" column="author_bio"/>
    <result property="favouriteSection" column="author_favourite_section"/>
  </association>
  <collection property="posts" ofType="Post">
    <id property="id" column="post_id"/>
    <result property="subject" column="post_subject"/>
    <association property="author" javaType="Author"/>
    <collection property="comments" ofType="Comment">
      <id property="id" column="comment_id"/>
    </collection>
    <collection property="tags" ofType="Tag" >
      <id property="id" column="tag_id"/>
    </collection>
    <discriminator javaType="int" column="draft">
      <case value="1" resultType="DraftPost"/>
    </discriminator>
  </collection>
</resultMap>
The resultMap element has a number of sub-elements and a structure worthy of some discussion. The following is a conceptual view of the resultMap element.

resultMap
constructor - used for injecting results into the constructor of a class upon instantiation
idArg - ID argument; flagging results as ID will help improve overall performance
arg - a normal result injected into the constructor
id – an ID result; flagging results as ID will help improve overall performance
result – a normal result injected into a field or JavaBean property
association – a complex type association; many results will roll up into this type
nested result mappings – associations are resultMaps themselves, or can refer to one
collection – a collection of complex types
nested result mappings – collections are resultMaps themselves, or can refer to one
discriminator – uses a result value to determine which resultMap to use
case – a case is a result map based on some value
nested result mappings – a case is also a result map itself, and thus can contain many of these same elements, or it can refer to an external resultMap.
ResultMap Attributes
Attribute	Description
id	A unique identifier in this namespace that can be used to reference this result map.
type	A fully qualified Java class name, or a type alias (see the table above for the list of built-in type aliases).
autoMapping	If present, MyBatis will enable or disable the automapping for this ResultMap. This attribute overrides the global autoMappingBehavior. Default: unset.
Best Practice Always build ResultMaps incrementally. Unit tests really help out here. If you try to build a gigantic resultMap like the one above all at once, it's likely you'll get it wrong and it will be hard to work with. Start simple, and evolve it a step at a time. And unit test! The downside to using frameworks is that they are sometimes a bit of a black box (open source or not). Your best bet to ensure that you're achieving the behaviour that you intend, is to write unit tests. It also helps to have them when submitting bugs.

The next sections will walk through each of the elements in more detail.

id & result
<id property="id" column="post_id"/>
<result property="subject" column="post_subject"/>
These are the most basic of result mappings. Both id and result map a single column value to a single property or field of a simple data type (String, int, double, Date, etc.).

The only difference between the two is that id will flag the result as an identifier property to be used when comparing object instances. This helps to improve general performance, but especially performance of caching and nested result mapping (i.e. join mapping).

Each has a number of attributes:

Id and Result Attributes
Attribute	Description
property	The field or property to map the column result to. If a matching JavaBeans property exists for the given name, then that will be used. Otherwise, MyBatis will look for a field of the given name. In both cases you can use complex property navigation using the usual dot notation. For example, you can map to something simple like: username, or to something more complicated like: address.street.number.
column	The column name from the database, or the aliased column label. This is the same string that would normally be passed to resultSet.getString(columnName).
javaType	A fully qualified Java class name, or a type alias (see the table above for the list of built-in type aliases). MyBatis can usually figure out the type if you're mapping to a JavaBean. However, if you are mapping to a HashMap, then you should specify the javaType explicitly to ensure the desired behaviour.
jdbcType	The JDBC Type from the list of supported types that follows this table. The JDBC type is only required for nullable columns upon insert, update or delete. This is a JDBC requirement, not a MyBatis one. So even if you were coding JDBC directly, you'd need to specify this type – but only for nullable values.
typeHandler	We discussed default type handlers previously in this documentation. Using this property you can override the default type handler on a mapping-by-mapping basis. The value is either a fully qualified class name of a TypeHandler implementation, or a type alias.
Supported JDBC Types
For future reference, MyBatis supports the following JDBC Types via the included JdbcType enumeration.

BIT	FLOAT	CHAR	TIMESTAMP	OTHER	UNDEFINED
TINYINT	REAL	VARCHAR	BINARY	BLOB	NVARCHAR
SMALLINT	DOUBLE	LONGVARCHAR	VARBINARY	CLOB	NCHAR
INTEGER	NUMERIC	DATE	LONGVARBINARY	BOOLEAN	NCLOB
BIGINT	DECIMAL	TIME	NULL	CURSOR	ARRAY
constructor
While properties will work for most Data Transfer Object (DTO) type classes, and likely most of your domain model, there may be some cases where you want to use immutable classes. Often tables that contain reference or lookup data that rarely or never changes is suited to immutable classes. Constructor injection allows you to set values on a class upon instantiation, without exposing public methods. MyBatis also supports private properties and private JavaBeans properties to achieve this, but some people prefer Constructor injection. The constructor element enables this.

Consider the following constructor:

public class User {
//...
public User(Integer id, String username, int age) {
//...
}
//...
}
In order to inject the results into the constructor, MyBatis needs to identify the constructor for somehow. In the following example, MyBatis searches a constructor declared with three parameters: java.lang.Integer, java.lang.String and int in this order.

<constructor>
   <idArg column="id" javaType="int"/>
   <arg column="username" javaType="String"/>
   <arg column="age" javaType="_int"/>
</constructor>
When you are dealing with a constructor with many parameters, maintaining the order of arg elements is error-prone.
Since 3.4.3, by specifying the name of each parameter, you can write arg elements in any order. To reference constructor parameters by their names, you can either add @Param annotation to them or compile the project with '-parameters' compiler option and enable useActualParamName (this option is enabled by default). The following example is valid for the same constructor even though the order of the second and the third parameters does not match with the declared order.

<constructor>
   <idArg column="id" javaType="int" name="id" />
   <arg column="age" javaType="_int" name="age" />
   <arg column="username" javaType="String" name="username" />
</constructor>
javaType can be omitted if there is a property with the same name and type.

The rest of the attributes and rules are the same as for the regular id and result elements.

Attribute	Description
column	The column name from the database, or the aliased column label. This is the same string that would normally be passed to resultSet.getString(columnName).
javaType	A fully qualified Java class name, or a type alias (see the table above for the list of built-in type aliases). MyBatis can usually figure out the type if you're mapping to a JavaBean. However, if you are mapping to a HashMap, then you should specify the javaType explicitly to ensure the desired behaviour.
jdbcType	The JDBC Type from the list of supported types that follows this table. The JDBC type is only required for nullable columns upon insert, update or delete. This is a JDBC requirement, not an MyBatis one. So even if you were coding JDBC directly, you'd need to specify this type – but only for nullable values.
typeHandler	We discussed default type handlers previously in this documentation. Using this property you can override the default type handler on a mapping-by-mapping basis. The value is either a fully qualified class name of a TypeHandler implementation, or a type alias.
select	The ID of another mapped statement that will load the complex type required by this property mapping. The values retrieved from columns specified in the column attribute will be passed to the target select statement as parameters. See the Association element for more.
resultMap	This is the ID of a ResultMap that can map the nested results of this argument into an appropriate object graph. This is an alternative to using a call to another select statement. It allows you to join multiple tables together into a single ResultSet. Such a ResultSet will contain duplicated, repeating groups of data that needs to be decomposed and mapped properly to a nested object graph. To facilitate this, MyBatis lets you "chain" result maps together, to deal with the nested results. See the Association element below for more.
name	The name of the constructor parameter. Specifying name allows you to write arg elements in any order. See the above explanation. Since 3.4.3.
association
<association property="author" javaType="Author">
<id property="id" column="author_id"/>
<result property="username" column="author_username"/>
</association>
The association element deals with a "has-one" type relationship. For example, in our example, a Blog has one Author. An association mapping works mostly like any other result. You specify the target property, the javaType of the property (which MyBatis can figure out most of the time), the jdbcType if necessary and a typeHandler if you want to override the retrieval of the result values.

Where the association differs is that you need to tell MyBatis how to load the association. MyBatis can do so in two different ways:

Nested Select: By executing another mapped SQL statement that returns the complex type desired.
Nested Results: By using nested result mappings to deal with repeating subsets of joined results.
First, let's examine the properties of the element. As you'll see, it differs from a normal result mapping only by the select and resultMap attributes.

Attribute	Description
property	The field or property to map the column result to. If a matching JavaBeans property exists for the given name, then that will be used. Otherwise, MyBatis will look for a field of the given name. In both cases you can use complex property navigation using the usual dot notation. For example, you can map to something simple like: username, or to something more complicated like: address.street.number.
javaType	A fully qualified Java class name, or a type alias (see the table above for the list of built- in type aliases). MyBatis can usually figure out the type if you're mapping to a JavaBean. However, if you are mapping to a HashMap, then you should specify the javaType explicitly to ensure the desired behaviour.
jdbcType	The JDBC Type from the list of supported types that follows this table. The JDBC type is only required for nullable columns upon insert, update or delete. This is a JDBC requirement, not an MyBatis one. So even if you were coding JDBC directly, you'd need to specify this type – but only for nullable values.
typeHandler	We discussed default type handlers previously in this documentation. Using this property you can override the default type handler on a mapping-by-mapping basis. The value is either a fully qualified class name of a TypeHandler implementation, or a type alias.
Nested Select for Association
Attribute	Description
column	The column name from the database, or the aliased column label that holds the value that will be passed to the nested statement as an input parameter. This is the same string that would normally be passed to resultSet.getString(columnName). Note: To deal with composite keys, you can specify multiple column names to pass to the nested select statement by using the syntax column="{prop1=col1,prop2=col2}". This will cause prop1 and prop2 to be set against the parameter object for the target nested select statement.
select	The ID of another mapped statement that will load the complex type required by this property mapping. The values retrieved from columns specified in the column attribute will be passed to the target select statement as parameters. A detailed example follows this table. Note: To deal with composite keys, you can specify multiple column names to pass to the nested select statement by using the syntax column="{prop1=col1,prop2=col2}". This will cause prop1 and prop2 to be set against the parameter object for the target nested select statement.
fetchType	Optional. Valid values are lazy and eager. If present, it supersedes the global configuration parameter lazyLoadingEnabled for this mapping.
For example:

<resultMap id="blogResult" type="Blog">
  <association property="author" column="author_id" javaType="Author" select="selectAuthor"/>
</resultMap>

<select id="selectBlog" resultMap="blogResult">
  SELECT * FROM BLOG WHERE ID = #{id}
</select>

<select id="selectAuthor" resultType="Author">
  SELECT * FROM AUTHOR WHERE ID = #{id}
</select>
That's it. We have two select statements: one to load the Blog, the other to load the Author, and the Blog's resultMap describes that the selectAuthor statement should be used to load its author property.

All other properties will be loaded automatically assuming their column and property names match.

While this approach is simple, it will not perform well for large data sets or lists. This problem is known as the "N+1 Selects Problem". In a nutshell, the N+1 selects problem is caused like this:

You execute a single SQL statement to retrieve a list of records (the "+1").
For each record returned, you execute a select statement to load details for each (the "N").
This problem could result in hundreds or thousands of SQL statements to be executed. This is not always desirable.

The upside is that MyBatis can lazy load such queries, thus you might be spared the cost of these statements all at once. However, if you load such a list and then immediately iterate through it to access the nested data, you will invoke all of the lazy loads, and thus performance could be very bad.

And so, there is another way.

Nested Results for Association
Attribute	Description
resultMap	This is the ID of a ResultMap that can map the nested results of this association into an appropriate object graph. This is an alternative to using a call to another select statement. It allows you to join multiple tables together into a single ResultSet. Such a ResultSet will contain duplicated, repeating groups of data that needs to be decomposed and mapped properly to a nested object graph. To facilitate this, MyBatis lets you "chain" result maps together, to deal with the nested results. An example will be far easier to follow, and one follows this table.
columnPrefix	When joining multiple tables, you would have to use column alias to avoid duplicated column names in the ResultSet. Specifying columnPrefix allows you to map such columns to an external resultMap. Please see the example explained later in this section.
notNullColumn	By default a child object is created only if at least one of the columns mapped to the child's properties is non null. With this attribute you can change this behaviour by specifiying which columns must have a value so MyBatis will create a child object only if any of those columns is not null. Multiple column names can be specified using a comma as a separator. Default value: unset.
autoMapping	If present, MyBatis will enable or disable automapping when mapping the result to this property. This attribute overrides the global autoMappingBehavior. Note that it has no effect on an external resultMap, so it is pointless to use it with select or resultMap attribute. Default value: unset.
You've already seen a very complicated example of nested associations above. The following is a far simpler example to demonstrate how this works. Instead of executing a separate statement, we'll join the Blog and Author tables together, like so:

<select id="selectBlog" resultMap="blogResult">
  select
    B.id            as blog_id,
    B.title         as blog_title,
    B.author_id     as blog_author_id,
    A.id            as author_id,
    A.username      as author_username,
    A.password      as author_password,
    A.email         as author_email,
    A.bio           as author_bio
  from Blog B left outer join Author A on B.author_id = A.id
  where B.id = #{id}
</select>
Notice the join, as well as the care taken to ensure that all results are aliased with a unique and clear name. This makes mapping far easier. Now we can map the results:

<resultMap id="blogResult" type="Blog">
  <id property="id" column="blog_id" />
  <result property="title" column="blog_title"/>
  <association property="author" resultMap="authorResult" />
</resultMap>

<resultMap id="authorResult" type="Author">
  <id property="id" column="author_id"/>
  <result property="username" column="author_username"/>
  <result property="password" column="author_password"/>
  <result property="email" column="author_email"/>
  <result property="bio" column="author_bio"/>
</resultMap>
In the example above you can see at the Blog's "author" association delegates to the "authorResult" resultMap to load the Author instance.

Very Important: id elements play a very important role in Nested Result mapping. You should always specify one or more properties that can be used to uniquely identify the results. The truth is that MyBatis will still work if you leave it out, but at a severe performance cost. Choose as few properties as possible that can uniquely identify the result. The primary key is an obvious choice (even if composite).

Now, the above example used an external resultMap element to map the association. This makes the Author resultMap reusable. However, if you have no need to reuse it, or if you simply prefer to co-locate your result mappings into a single descriptive resultMap, you can nest the association result mappings. Here's the same example using this approach:

<resultMap id="blogResult" type="Blog">
  <id property="id" column="blog_id" />
  <result property="title" column="blog_title"/>
  <association property="author" javaType="Author">
    <id property="id" column="author_id"/>
    <result property="username" column="author_username"/>
    <result property="password" column="author_password"/>
    <result property="email" column="author_email"/>
    <result property="bio" column="author_bio"/>
  </association>
</resultMap>
What if the blog has a co-author? The select statement would look like:

<select id="selectBlog" resultMap="blogResult">
  select
    B.id            as blog_id,
    B.title         as blog_title,
    A.id            as author_id,
    A.username      as author_username,
    A.password      as author_password,
    A.email         as author_email,
    A.bio           as author_bio,
    CA.id           as co_author_id,
    CA.username     as co_author_username,
    CA.password     as co_author_password,
    CA.email        as co_author_email,
    CA.bio          as co_author_bio
  from Blog B
  left outer join Author A on B.author_id = A.id
  left outer join Author CA on B.co_author_id = CA.id
  where B.id = #{id}
</select>
Recall that the resultMap for Author is defined as follows.

<resultMap id="authorResult" type="Author">
  <id property="id" column="author_id"/>
  <result property="username" column="author_username"/>
  <result property="password" column="author_password"/>
  <result property="email" column="author_email"/>
  <result property="bio" column="author_bio"/>
</resultMap>
Because the column names in the results differ from the columns defined in the resultMap, you need to specify columnPrefix to reuse the resultMap for mapping co-author results.

<resultMap id="blogResult" type="Blog">
  <id property="id" column="blog_id" />
  <result property="title" column="blog_title"/>
  <association property="author"
    resultMap="authorResult" />
  <association property="coAuthor"
    resultMap="authorResult"
    columnPrefix="co_" />
</resultMap>
Multiple ResultSets for Association
Attribute	Description
column	When using multiple resultset this attribute specifies the columns (separated by commas) that will be correlated with the foreignColumn to identify the parent and the child of a relationship.
foreignColumn	Identifies the name of the columns that contains the foreign keys which values will be matched against the values of the columns specified in the column attibute of the parent type.
resultSet	Identifies the name of the result set where this complex type will be loaded from.
Starting from version 3.2.3 MyBatis provides yet another way to solve the N+1 problem.

Some databases allow stored procedures to return more than one resultset or execute more than one statement at once and return a resultset per each one. This can be used to hit the database just once and return related data without using a join.

In the example, the stored procedure executes the following queries and returns two result sets. The first will contain Blogs and the second Authors.

SELECT * FROM BLOG WHERE ID = #{id}

SELECT * FROM AUTHOR WHERE ID = #{id}
A name must be given to each result set by adding a resultSets attribute to the mapped statement with a list of names separated by commas.

<select id="selectBlog" resultSets="blogs,authors" resultMap="blogResult" statementType="CALLABLE">
  {call getBlogsAndAuthors(#{id,jdbcType=INTEGER,mode=IN})}
</select>
Now we can specify that the data to fill the "author" association comes in the "authors" result set:

<resultMap id="blogResult" type="Blog">
  <id property="id" column="id" />
  <result property="title" column="title"/>
  <association property="author" javaType="Author" resultSet="authors" column="author_id" foreignColumn="id">
    <id property="id" column="id"/>
    <result property="username" column="username"/>
    <result property="password" column="password"/>
    <result property="email" column="email"/>
    <result property="bio" column="bio"/>
  </association>
</resultMap>
You've seen above how to deal with a "has one" type association. But what about "has many"? That's the subject of the next section.

collection
<collection property="posts" ofType="domain.blog.Post">
<id property="id" column="post_id"/>
<result property="subject" column="post_subject"/>
<result property="body" column="post_body"/>
</collection>
The collection element works almost identically to the association. In fact, it's so similar, to document the similarities would be redundant. So let's focus on the differences.

To continue with our example above, a Blog only had one Author. But a Blog has many Posts. On the blog class, this would be represented by something like:

private List<Post> posts;
To map a set of nested results to a List like this, we use the collection element. Just like the association element, we can use a nested select, or nested results from a join.

Nested Select for Collection
First, let's look at using a nested select to load the Posts for the Blog.

<resultMap id="blogResult" type="Blog">
  <collection property="posts" javaType="ArrayList" column="id" ofType="Post" select="selectPostsForBlog"/>
</resultMap>

<select id="selectBlog" resultMap="blogResult">
  SELECT * FROM BLOG WHERE ID = #{id}
</select>

<select id="selectPostsForBlog" resultType="Post">
  SELECT * FROM POST WHERE BLOG_ID = #{id}
</select>
There are a number things you'll notice immediately, but for the most part it looks very similar to the association element we learned about above. First, you'll notice that we're using the collection element. Then you'll notice that there's a new "ofType" attribute. This attribute is necessary to distinguish between the JavaBean (or field) property type and the type that the collection contains. So you could read the following mapping like this:

<collection property="posts" javaType="ArrayList" column="id" ofType="Post" select="selectPostsForBlog"/>
Read as: "A collection of posts in an ArrayList of type Post."

The javaType attribute is really unnecessary, as MyBatis will figure this out for you in most cases. So you can often shorten this down to simply:

<collection property="posts" column="id" ofType="Post" select="selectPostsForBlog"/>
Nested Results for Collection
By this point, you can probably guess how nested results for a collection will work, because it's exactly the same as an association, but with the same addition of the ofType attribute applied.

First, let's look at the SQL:

<select id="selectBlog" resultMap="blogResult">
  select
  B.id as blog_id,
  B.title as blog_title,
  B.author_id as blog_author_id,
  P.id as post_id,
  P.subject as post_subject,
  P.body as post_body,
  from Blog B
  left outer join Post P on B.id = P.blog_id
  where B.id = #{id}
</select>
Again, we've joined the Blog and Post tables, and have taken care to ensure quality result column labels for simple mapping. Now mapping a Blog with its collection of Post mappings is as simple as:

<resultMap id="blogResult" type="Blog">
  <id property="id" column="blog_id" />
  <result property="title" column="blog_title"/>
  <collection property="posts" ofType="Post">
    <id property="id" column="post_id"/>
    <result property="subject" column="post_subject"/>
    <result property="body" column="post_body"/>
  </collection>
</resultMap>
Again, remember the importance of the id elements here, or read the association section above if you haven't already.

Also, if you prefer the longer form that allows for more reusability of your result maps, you can use the following alternative mapping:

<resultMap id="blogResult" type="Blog">
  <id property="id" column="blog_id" />
  <result property="title" column="blog_title"/>
  <collection property="posts" ofType="Post" resultMap="blogPostResult" columnPrefix="post_"/>
</resultMap>

<resultMap id="blogPostResult" type="Post">
  <id property="id" column="id"/>
  <result property="subject" column="subject"/>
  <result property="body" column="body"/>
</resultMap>
Multiple ResultSets for Collection
As we did for the association, we can call a stored procedure that executes two queries and returns two result sets, one with Blogs and another with Posts:

SELECT * FROM BLOG WHERE ID = #{id}

SELECT * FROM POST WHERE BLOG_ID = #{id}
A name must be given to each result set by adding a resultSets attribute to the mapped statement with a list of names separated by commas.

<select id="selectBlog" resultSets="blogs,posts" resultMap="blogResult">
  {call getBlogsAndPosts(#{id,jdbcType=INTEGER,mode=IN})}
</select>
We specify that the "posts" collection will be filled out of data contained in the result set named "posts":

<resultMap id="blogResult" type="Blog">
  <id property="id" column="id" />
  <result property="title" column="title"/>
  <collection property="posts" ofType="Post" resultSet="posts" column="id" foreignColumn="blog_id">
    <id property="id" column="id"/>
    <result property="subject" column="subject"/>
    <result property="body" column="body"/>
  </collection>
</resultMap>
NOTE There's no limit to the depth, breadth or combinations of the associations and collections that you map. You should keep performance in mind when mapping them. Unit testing and performance testing of your application goes a long way toward discovering the best approach for your application. The nice thing is that MyBatis lets you change your mind later, with very little (if any) impact to your code.

Advanced association and collection mapping is a deep subject. Documentation can only get you so far. With a little practice, it will all become clear very quickly.

discriminator
<discriminator javaType="int" column="draft">
<case value="1" resultType="DraftPost"/>
</discriminator>
Sometimes a single database query might return result sets of many different (but hopefully somewhat related) data types. The discriminator element was designed to deal with this situation, and others, including class inheritance hierarchies. The discriminator is pretty simple to understand, as it behaves much like a switch statement in Java.

A discriminator definition specifies column and javaType attributes. The column is where MyBatis will look for the value to compare. The javaType is required to ensure the proper kind of equality test is performed (although String would probably work for almost any situation). For example:

<resultMap id="vehicleResult" type="Vehicle">
  <id property="id" column="id" />
  <result property="vin" column="vin"/>
  <result property="year" column="year"/>
  <result property="make" column="make"/>
  <result property="model" column="model"/>
  <result property="color" column="color"/>
  <discriminator javaType="int" column="vehicle_type">
    <case value="1" resultMap="carResult"/>
    <case value="2" resultMap="truckResult"/>
    <case value="3" resultMap="vanResult"/>
    <case value="4" resultMap="suvResult"/>
  </discriminator>
</resultMap>
In this example, MyBatis would retrieve each record from the result set and compare its vehicle type value. If it matches any of the discriminator cases, then it will use the resultMap specified by the case. This is done exclusively, so in other words, the rest of the resultMap is ignored (unless it is extended, which we talk about in a second). If none of the cases match, then MyBatis simply uses the resultMap as defined outside of the discriminator block. So, if the carResult was declared as follows:

<resultMap id="carResult" type="Car">
  <result property="doorCount" column="door_count" />
</resultMap>
Then ONLY the doorCount property would be loaded. This is done to allow completely independent groups of discriminator cases, even ones that have no relationship to the parent resultMap. In this case we do of course know that there's a relationship between cars and vehicles, as a Car is-a Vehicle. Therefore, we want the rest of the properties loaded too. One simple change to the resultMap and we're set to go.

<resultMap id="carResult" type="Car" extends="vehicleResult">
  <result property="doorCount" column="door_count" />
</resultMap>
Now all of the properties from both the vehicleResult and carResult will be loaded.

Once again though, some may find this external definition of maps somewhat tedious. Therefore there's an alternative syntax for those that prefer a more concise mapping style. For example:

<resultMap id="vehicleResult" type="Vehicle">
  <id property="id" column="id" />
  <result property="vin" column="vin"/>
  <result property="year" column="year"/>
  <result property="make" column="make"/>
  <result property="model" column="model"/>
  <result property="color" column="color"/>
  <discriminator javaType="int" column="vehicle_type">
    <case value="1" resultType="carResult">
      <result property="doorCount" column="door_count" />
    </case>
    <case value="2" resultType="truckResult">
      <result property="boxSize" column="box_size" />
      <result property="extendedCab" column="extended_cab" />
    </case>
    <case value="3" resultType="vanResult">
      <result property="powerSlidingDoor" column="power_sliding_door" />
    </case>
    <case value="4" resultType="suvResult">
      <result property="allWheelDrive" column="all_wheel_drive" />
    </case>
  </discriminator>
</resultMap>
NOTE Remember that these are all Result Maps, and if you don't specify any results at all, then MyBatis will automatically match up columns and properties for you. So most of these examples are more verbose than they really need to be. That said, most databases are kind of complex and it's unlikely that we'll be able to depend on that for all cases.

Auto-mapping
As you have already seen in the previous sections, in simple cases MyBatis can auto-map the results for you and in others you will need to build a result map. But as you will see in this section you can also mix both strategies. Let's have a deeper look at how auto-mapping works.

When auto-mapping results MyBatis will get the column name and look for a property with the same name ignoring case. That means that if a column named ID and property named id are found, MyBatis will set the id property with the ID column value.

Usually database columns are named using uppercase letters and underscores between words and java properties often follow the camelcase naming covention. To enable the auto-mapping between them set the setting mapUnderscoreToCamelCase to true.

Auto-mapping works even when there is an specific result map. When this happens, for each result map, all columns that are present in the ResultSet that have not a manual mapping will be auto-mapped, then manual mappings will be processed. In the following sample id and userName columns will be auto-mapped and hashed_password column will be mapped.

<select id="selectUsers" resultMap="userResultMap">
  select
    user_id             as "id",
    user_name           as "userName",
    hashed_password
  from some_table
  where id = #{id}
</select>
<resultMap id="userResultMap" type="User">
  <result property="password" column="hashed_password"/>
</resultMap>
There are three auto-mapping levels:

NONE - disables auto-mapping. Only manually mapped properties will be set.
PARTIAL - will auto-map results except those that have nested result mappings defined inside (joins).
FULL - auto-maps everything.
The default value is PARTIAL, and it is so for a reason. When FULL is used auto-mapping will be performed when processing join results and joins retrieve data of several different entities in the same row hence this may result in undesired mappings. To understand the risk have a look at the following sample:

<select id="selectBlog" resultMap="blogResult">
  select
    B.id,
    B.title,
    A.username,
  from Blog B left outer join Author A on B.author_id = A.id
  where B.id = #{id}
</select>
<resultMap id="blogResult" type="Blog">
  <association property="author" resultMap="authorResult"/>
</resultMap>

<resultMap id="authorResult" type="Author">
  <result property="username" column="author_username"/>
</resultMap>
With this result map both Blog and Author will be auto-mapped. But note that Author has an id property and there is a column named id in the ResultSet so Author's id will be filled with Blog's id, and that is not what you were expecting. So use the FULL option with caution.

Regardless of the auto-mapping level configured you can enable or disable the automapping for an specific ResultMap by adding the attribute autoMapping to it:

<resultMap id="userResultMap" type="User" autoMapping="false">
  <result property="password" column="hashed_password"/>
</resultMap>
cache
MyBatis includes a powerful transactional query caching feature which is very configurable and customizable. A lot of changes have been made in the MyBatis 3 cache implementation to make it both more powerful and far easier to configure.

By default, just local session caching is enabled that is used solely to cache data for the duration of a session. To enable a global second level of caching you simply need to add one line to your SQL Mapping file:

<cache/>
Literally that's it. The effect of this one simple statement is as follows:

All results from select statements in the mapped statement file will be cached.
All insert, update and delete statements in the mapped statement file will flush the cache.
The cache will use a Least Recently Used (LRU) algorithm for eviction.
The cache will not flush on any sort of time based schedule (i.e. no Flush Interval).
The cache will store 1024 references to lists or objects (whatever the query method returns).
The cache will be treated as a read/write cache, meaning objects retrieved are not shared and can be safely modified by the caller, without interfering with other potential modifications by other callers or threads.
NOTE The cache will only apply to statements declared in the mapping file where the cache tag is located. If you are using the Java API in conjunction with the XML mapping files, then statements declared in the companion interface will not be cached by default. You will need to refer to the cache region using the @CacheNamespaceRef annotation.

All of these properties are modifiable through the attributes of the cache element. For example:

<cache
eviction="FIFO"
flushInterval="60000"
size="512"
readOnly="true"/>
This more advanced configuration creates a FIFO cache that flushes once every 60 seconds, stores up to 512 references to result objects or lists, and objects returned are considered read-only, thus modifying them could cause conflicts between callers in different threads.

The available eviction policies available are:

LRU – Least Recently Used: Removes objects that haven't been used for the longst period of time.
FIFO – First In First Out: Removes objects in the order that they entered the cache.
SOFT – Soft Reference: Removes objects based on the garbage collector state and the rules of Soft References.
WEAK – Weak Reference: More aggressively removes objects based on the garbage collector state and rules of Weak References.
The default is LRU.

The flushInterval can be set to any positive integer and should represent a reasonable amount of time specified in milliseconds. The default is not set, thus no flush interval is used and the cache is only flushed by calls to statements.

The size can be set to any positive integer, keep in mind the size of the objects your caching and the available memory resources of your environment. The default is 1024.

The readOnly attribute can be set to true or false. A read-only cache will return the same instance of the cached object to all callers. Thus such objects should not be modified. This offers a significant performance advantage though. A read-write cache will return a copy (via serialization) of the cached object. This is slower, but safer, and thus the default is false.

NOTE Second level cache is transactional. That means that it is updated when a SqlSession finishes with commit or when it finishes with rollback but no inserts/deletes/updates with flushCache=true where executed.

Using a Custom Cache
In addition to customizing the cache in these ways, you can also completely override the cache behavior by implementing your own cache, or creating an adapter to other 3rd party caching solutions.

<cache type="com.domain.something.MyCustomCache"/>
This example demonstrates how to use a custom cache implementation. The class specified in the type attribute must implement the org.apache.ibatis.cache.Cache interface and provide a constructor that gets an String id as an argument. This interface is one of the more complex in the MyBatis framework, but simple given what it does.

public interface Cache {
String getId();
int getSize();
void putObject(Object key, Object value);
Object getObject(Object key);
boolean hasKey(Object key);
Object removeObject(Object key);
void clear();
}
To configure your cache, simply add public JavaBeans properties to your Cache implementation, and pass properties via the cache Element, for example, the following would call a method called setCacheFile(String file) on your Cache implementation:

<cache type="com.domain.something.MyCustomCache">
  <property name="cacheFile" value="/tmp/my-custom-cache.tmp"/>
</cache>
You can use JavaBeans properties of all simple types, MyBatis will do the conversion. And you can specify a placeholder(e.g. ${cache.file}) to replace value defined at configuration properties.

Since 3.4.2, the MyBatis has been supported to call an initialization method after it's set all properties. If you want to use this feature, please implements the org.apache.ibatis.builder.InitializingObject interface on your custom cache class.

public interface InitializingObject {
void initialize() throws Exception;
}
NOTE Settings of cache (like eviction strategy, read write..etc.) in section above are not applied when using Custom Cache.

It's important to remember that a cache configuration and the cache instance are bound to the namespace of the SQL Map file. Thus, all statements in the same namespace as the cache are bound by it. Statements can modify how they interact with the cache, or exclude themselves completely by using two simple attributes on a statement-by-statement basis. By default, statements are configured like this:

<select ... flushCache="false" useCache="true"/>
<insert ... flushCache="true"/>
<update ... flushCache="true"/>
<delete ... flushCache="true"/>
Since that's the default, you obviously should never explicitly configure a statement that way. Instead, only set the flushCache and useCache attributes if you want to change the default behavior. For example, in some cases you may want to exclude the results of a particular select statement from the cache, or you might want a select statement to flush the cache. Similarly, you may have some update statements that don't need to flush the cache upon execution.

cache-ref
Recall from the previous section that only the cache for this particular namespace will be used or flushed for statements within the same namespace. There may come a time when you want to share the same cache configuration and instance between namespaces. In such cases you can reference another cache by using the cache-ref element.

<cache-ref namespace="com.someone.application.data.SomeMapper"/>


#### p
2. Defining the Model
   Let's start by defining simple POJO that we'll use throughout our article:

public class Article {
private Long id;
private String title;
private String author;

    // constructor, standard getters and setters
}
And an equivalent SQL schema.sql file:

CREATE TABLE IF NOT EXISTS `ARTICLES`(
`id`          INTEGER PRIMARY KEY,
`title`       VARCHAR(100) NOT NULL,
`author`      VARCHAR(100) NOT NULL
);
Next, let's create a data.sql file, which simply inserts one record into our articles table:

INSERT INTO ARTICLES
VALUES (1, 'Working with MyBatis in Spring', 'Baeldung');
Both SQL files must be included in the classpath.

3. Spring Config
   To start using MyBatis, we have to include two main dependencies — MyBatis and MyBatis-Spring:

<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.2</version>
</dependency>

<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>2.0.2</version>
</dependency>
Apart from that, we'll need basic Spring dependencies:

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.8</version>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-beans</artifactId>
    <version>5.3.8</version>
</dependency>
In our examples, we'll use the H2 embedded database to simplify the setup and EmbeddedDatabaseBuilder class from the spring-jdbc module for configuration:

<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>1.4.199</version>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.3.8</version>
</dependency>
3.1. Annotation Based Configuration
Spring simplifies the configuration for MyBatis. The only required elements are javax.sql.Datasource, org.apache.ibatis.session.SqlSessionFactory, and at least one mapper.

First, let's create a configuration class:

@Configuration
@MapperScan("com.baeldung.mybatis")
public class PersistenceConfig {

    @Bean
    public DataSource dataSource() {
        return new EmbeddedDatabaseBuilder()
          .setType(EmbeddedDatabaseType.H2)
          .addScript("schema.sql")
          .addScript("data.sql")
          .build();
    }

    @Bean
    public SqlSessionFactory sqlSessionFactory() throws Exception {
        SqlSessionFactoryBean factoryBean = new SqlSessionFactoryBean();
        factoryBean.setDataSource(dataSource());
        return factoryBean.getObject();
    }
}
We also applied a @MapperScan annotation from MyBatis-Spring that scans defined packages and automatically picks up interfaces using any of the mapper annotations, such as @Select or @Delete.

Using @MapperScan also ensures that every provided mapper is automatically registered as a Bean and can be later used with the @Autowired annotation.

We can now create a simple ArticleMapper interface:

public interface ArticleMapper {
@Select("SELECT * FROM ARTICLES WHERE id = #{id}")
Article getArticle(@Param("id") Long id);
}
And finally, test our setup:

@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = PersistenceConfig.class)
public class ArticleMapperIntegrationTest {

    @Autowired
    ArticleMapper articleMapper;

    @Test
    public void whenRecordsInDatabase_shouldReturnArticleWithGivenId() {
        Article article = articleMapper.getArticle(1L);

        assertThat(article).isNotNull();
        assertThat(article.getId()).isEqualTo(1L);
        assertThat(article.getAuthor()).isEqualTo("Baeldung");
        assertThat(article.getTitle()).isEqualTo("Working with MyBatis in Spring");
    }
}
In the above example, we've used MyBatis to retrieve the only record we inserted previously in our data.sql file.

3.2. XML Based Configuration
As previously described, to use MyBatis with Spring, we need Datasource, SqlSessionFactory, and at least one mapper.

Let's create the required bean definitions in the beans.xml configuration file:

<jdbc:embedded-database id="dataSource" type="H2">
<jdbc:script location="schema.sql"/>
<jdbc:script location="data.sql"/>
</jdbc:embedded-database>

<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="dataSource" />
</bean>

<bean id="articleMapper" class="org.mybatis.spring.mapper.MapperFactoryBean">
    <property name="mapperInterface" value="com.baeldung.mybatis.ArticleMapper" />
    <property name="sqlSessionFactory" ref="sqlSessionFactory" />
</bean>
In this example, we also used the custom XML schema provided by spring-jdbc to configure our H2 datasource.

To test this configuration, we can reuse the previously implemented test class. However, we have to adjust the context configuration, which we can do by applying the annotation:

@ContextConfiguration(locations = "classpath:/beans.xml")
4. Spring Boot
   Spring Boot provides mechanisms that simplify the configuration of MyBatis with Spring even more.

First, let's add the mybatis-spring-boot-starter dependency to our pom.xml:

<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>2.1.0</version>
</dependency>
By default, if we use an auto-configuration feature, Spring Boot detects the H2 dependency from our classpath and configures both Datasource and SqlSessionFactory for us. In addition, it also executes both schema.sql and data.sql on startup.

If we don't use an embedded database, we can use configuration via an application.yml or application.properties file or define a Datasource bean pointing to our database.

The only thing we have left to do is to define a mapper interface, in the same manner as before, and annotate it with the @Mapper annotation from MyBatis. As a result, Spring Boot scans our project, looking for that annotation, and registers our mappers as beans.

After that, we can test our configuration using the previously defined test class by applying annotations from spring-boot-starter-test:

@RunWith(SpringRunner.class)
@SpringBootTest
#### p
Why dynamic SQL
​ Avoid different query parameters from the front end , So it leads to a lot of writing if else, There's a lot to pay attention to SQL Statement and, Space , Commas and escaped single quotes , Splicing and debugging sql It's very time consuming .

​ Mybatis The dynamics of the SQL That solves the problem , It is based on OGNL Of expression .

Dynamic Tags
if
<select id="findActiveBlogWithTitleLike"
resultType="Blog">
SELECT * FROM BLOG
WHERE state = ‘ACTIVE’
<if test="title != null">
AND title like #{title}
</if>
</select>
choose(when,otherwise)
<select id="findActiveBlogLike"
resultType="Blog">
SELECT * FROM BLOG WHERE state = ‘ACTIVE’
<choose>
<when test="title != null">
AND title like #{title}
</when>
<when test="author != null and author.name != null">
AND author_name like #{author.name}
</when>
<otherwise>
AND featured = 1
</otherwise>
</choose>
</select>
trim(where,set)
It's usually used to remove the prefix, the latter or the latter

<trim prefix="WHERE" prefixOverrides="AND |OR ">
  ...
</trim>
foreach
Dynamically generate statements when you need to traverse a collection

<select id="selectPostIn" resultType="domain.blog.Post">
  SELECT *
  FROM POST P
  WHERE ID in
  <foreach item="item" index="index" collection="list"
      open="(" separator="," close=")">
        #{item}
  </foreach>
</select>
The batch operation
​ We will have some batch operation scenarios in production projects , For example, when importing files and batch processing data ( Batch of new merchants 、 Batch modification of merchant information ), When the amount of data is very large , For example, when there are more than tens of thousands of them , stay Java Loop through the code SQL It must be unrealistic to go to the database for execution , Because this means creating tens of thousands of sessions with the database , Even if we use database connection pooling Technology , For the database server is also unbearable .

​ stay MyBatis It supports batch operation , Including batch inserts 、 to update 、 Delete . We can go straight I'm going to pass in a List、Set、Map Or array , Cooperation dynamics SQL The label of ,MyBatis Will automatically help us Generative grammar is correct SQL sentence .

​ Let's take a look at two examples , Batch insert and batch update .

Batch insert
The syntax for batch insertion is like this , As long as values Just add the inserted value later .

insert into tbl_emp (emp_id, emp_name, gender,email, d_id) values ( ?,?,?,?,? ) , ( ?,?,?,?,? ) , ( ?,?,?,?,? ) , ( ?,?,?,?,? ) , ( ?,?,?,?,? ) , ( ?,?,?,?,? ) , ( ?,?,?,?,? ) , ( ?,?,?,?,? ) , ( ?,?,?,?,? ) , ( ?,?,?,?,? )
stay Mapper In the document , We use foreach Label stitching values Part of the sentence :

<insert id="batchInsert" parameterType="java.util.List" useGeneratedKeys="true">
  <selectKey resultType="long" keyProperty="id" order="AFTER">
    SELECT LAST_INSERT_ID()
  </selectKey>
  insert into tbl_emp (emp_id, emp_name, gender,email, d_id)
  values
  <foreach collection="list" item="emps" index="index" separator=",">
    ( #{emps.empId},#{emps.empName},#{emps.gender},#{emps.email},#{emps.dId} )
  </foreach>
</insert>
Java In the code , Just pass in a List Parameters of type .

So let's test that out . It's more efficient than circular transmission SQL Execution is much higher . The key is to reduce the number of interaction with the database , And the time consumption of opening and closing transactions is avoided .

@Test
public void testBatchInsert() {
List<Employee> list = new ArrayList<Employee>();
long start = System.currentTimeMillis();
int count = 100000;
// max_allowed_packet  Default  4M, So over the length will report an error
for (int i = 0; i < count; i++) {
String gender = i % 2 == 0 ? "M" : "F";
Integer did = i % 2 == 0 ? 1 : 2;
Employee emp = new Employee(null, "TestName" + i, gender, "pony@baidu.com", did);
list.add(emp);
}

employeeMapper.batchInsert(list);
long end = System.currentTimeMillis();
System.out.println(" Batch insert " + count + " strip , Time consuming ：" + (end - start) + " millisecond ");
}
Batch update
<!--  Batch update  -->
<!--  Be careful separator  and  open -->
<update id="updateBatch">
    update tbl_emp set
    emp_name =
    <foreach collection="list" item="emps" index="index" separator=" " open="case emp_id" close="end">
        when #{emps.empId} then #{emps.empName}
    </foreach>
    ,gender =
    <foreach collection="list" item="emps" index="index" separator=" " open="case emp_id" close="end">
        when #{emps.empId} then #{emps.gender}
    </foreach>
    ,email =
    <foreach collection="list" item="emps" index="index" separator=" " open="case emp_id" close="end">
        when #{emps.empId} then #{emps.email}
    </foreach>
    where emp_id in
    <foreach collection="list" item="emps" index="index" separator="," open="(" close=")">
        #{emps.empId}
    </foreach>
</update>
Batch deletion is similar

Batch Executor
​ Of course MyBatis The batch operation of dynamic label also has some disadvantages , For example, there is a huge amount of data When , It's stitched together SQL The statement is too large .

​ MySQL The server of has a size limit for the received packets ,max_allowed_packet The default is 4M, You need to modify the default configuration to solve this problem .

Caused by: com.mysql.jdbc.PacketTooBigException: Packet for query is too large (7188967 > 4194304). You can change this value on the server by setting the max_allowed_packet' variable.
In our global profile , You can configure the default Executor The type of . One of them BatchExecutor.

<setting name="defaultExecutorType" value="BATCH"
You can also specify the type of executor when you create a session

SqlSession session = sqlSessionFactory.openSession(ExecutorType.BATCH);
BatchExecutor The bottom is right JDBC ps.addBatch() Encapsulation , The principle is to save a batch of SQL I'll send it later

Another parameter that may be new to you , Namely ExecutorType. This enumeration type defines three values :

ExecutorType.SIMPLE： This actuator type does nothing special . It creates a new preprocessing statement for the execution of each statement .
ExecutorType.REUSE： This type of actuator reuses the preprocessing statements .
ExecutorType.BATCH： This executor will execute all update statements in batches , If SELECT In the middle of them , If necessary, please distinguish them to ensure the legibility of behavior .
JDBC BatchExecutor Use
public void testJdbcBatch() throws IOException {
Connection conn = null;
PreparedStatement ps = null;

try {
Long start = System.currentTimeMillis();
//  Open the connection
conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=utf-8&rewriteBatchedStatements=true", "root", "123456");
ps = conn.prepareStatement(
"INSERT into blog values (?, ?, ?)");

    for (int i = 1000; i < 101000; i++) {
      Blog blog = new Blog();
      ps.setInt(1, i);
      ps.setString(2, String.valueOf(i)+"");
      ps.setInt(3, 1001);
      //ExecuteType=BATCH  It's about this ps Encapsulation , Batch insert 500w The data of , With this, the performance will be greatly improved <br>
      ps.addBatch();
    }

    ps.executeBatch();
    // conn.commit();
    ps.close();
    conn.close();
    Long end = System.currentTimeMillis();
    System.out.println("cost:"+(end -start ) +"ms");
} catch (SQLException se) {
se.printStackTrace();
} catch (Exception e) {
e.printStackTrace();
} finally {
try {
if (ps != null) ps.close();
} catch (SQLException se2) {
}
try {
if (conn != null) conn.close();
} catch (SQLException se) {
se.printStackTrace();
}
}
}
}
Three Executor The difference between
SimpleExecutor
Every time update or select, Just turn on one Statement object , Shut down immediately after use Statement object .

ReuseExecutor
perform update or select, With sql As key lookup Statement object , Use when you exist , Create... If it doesn't exist
After use , Don't shut down Statement object , It's placed in Map Inside , For the next use .
in short , It's reuse Statement object
Batch Executor
perform update( No, select,JDBC Batch processing does not support select)
Will all SQL All added to the batch ( add Batch())
Waiting for unified execution ( executebatch（）), It caches multiple Statement object , Every Statement Objects are add Batch() After the completion of , Wait for one by one execute Batch0 The batch . And DBC Batch processing is the same .
executeupdate()
It's a statement that accesses the database once
executebatch()
It's a batch of statements that visit the database once ( How many in a batch SQL With the server side max allowed packet of ).
Batchexecutor The bottom is right JDBC
ps. add Batch()
ps. execute Batch() Encapsulation .
nesting （ Relational query /N+1/ Delay loading )
https://mybatis.org/mybatis-3/zh/sqlmap-xml.html#Result_Maps

​ When we query business data, we often encounter cross table Association query , For example, querying employees will associate departments ( one-on-one ), Query grades will be associated with the course ( one-on-one ), Query the order will be associated with the product ( One to many ), wait .

Our mapping result has two labels , One is resultType, One is resultMap.

​ resultType yes select An attribute of the tag , Apply to return to JDK type ( such as Integer、String wait ) And the entity class . In this case, the columns of the result set and the attributes of the entity class can be mapped directly . If the returned word

Segments cannot be mapped directly , To use resultMap To establish a mapping relationship . In the case of associative queries , You can't usually use resultType To map . use resultMap mapping , Or modify it dto(Data Transfer Object), Add fields to it , This will lead to the addition of many unrelated fields . Or refer to the associated object , such as Blog It contains a Author object , This situation Next, we need to use association query (association, Or nested queries ),MyBatis It can help us make the results automatically Mapping .

There are two ways to configure one-to-one association queries :

Nesting results
<!--  Search the author according to the article , The results of a one-to-one query , Nesting results  -->
<resultMap id="BlogWithAuthorResultMap" type="com.zzjson.domain.associate.BlogAndAuthor">
  <id column="bid" property="bid" jdbcType="INTEGER"/>
  <result column="name" property="name" jdbcType="VARCHAR"/>
  <!--  The joint query , take author Properties of map to ResultMap -->
  <association property="author" javaType="com.zzjson.domain.Author">
    <id column="author_id" property="authorId"/>
    <result column="author_name" property="authorName"/>
  </association>
</resultMap>

<!--  Search the author according to the article , one-on-one , Nesting results , nothing N+1 problem  -->
<select id="selectBlogWithAuthorResult" resultMap="BlogWithAuthorResultMap">
  select b.bid, b.name, b.author_id, a.author_id, a.author_name
  from blog b
  left join author a
  on b.author_id = a.author_id
  where b.bid = #{bid, jdbcType=INTEGER}
</select>
nested queries N+1 problem
<!--  Another kind of joint query ( one-on-one ) The implementation of the , But in this way, there are “N+1” The problem of  -->
<resultMap id="BlogWithAuthorQueryMap" type="com.zzjson.domain.associate.BlogAndAuthor">
  <id column="bid" property="bid" jdbcType="INTEGER"/>
  <result column="name" property="name" jdbcType="VARCHAR"/>
  <association property="author" javaType="com.zzjson.domain.Author"
               column="author_id" select="selectAuthor"/> <!-- selectAuthor  It's defined below -->
</resultMap>

<!--  nested queries  -->
<select id="selectAuthor" parameterType="int" resultType="com.zzjson.domain.Author">
  select author_id authorId, author_name authorName
  from author
  where author_id = #{authorId}
</select>
​ It's two queries , When we look up employee information , Will send another SQL Go to the database to query the Department information .

​ We only perform the query of employee information once SQL( So-called 1), If you return N Bar record , It will be sent again N Search the database for department information ( So-called N), That's what we're talking about N+1 The problem of , This will waste the performance of our application and database .

Lazy loading
​ If we use nested queries , How to solve this problem ？

​ Can you wait until you use the information of the Department ？ This is what we call delayed loading , Or lazy loading

​ stay Mybatis It can solve this problem by turning on the delay loading switch .

setting To configure + agent
​ stay setting The tag can be configured with

<!-- Global switch for delayed loading . When opened , All associated objects delay loading . Default false -->
<setting name="lazyLoadingEnabled" value="true"/>
<!-- When opened , Any method call loads all the properties of the object . Default  false, It can be done by  select  Labeled  fetchType  To cover -->
<setting name="aggressiveLazyLoading" value="false"/>
<!-- Mybatis Proxy tools used to create objects with deferred loading capability , Default JAVASSIST-->
<setting name ="proxyFactory" value="CGLIB"/>
lazyLoadingEnabled Determines whether to delay loading .

aggressiveLazyLoading All methods that determine whether an object triggers a query .

So let's test that out ( You can also change it to a query list ):

1、 There is no switch to turn on delayed loading , Will send two queries in a row ;

2、 Turn on the delay loading switch , call blog.getAuthor() as well as default (equals,clone,hashCode,toString) The second query will be launched when the query is finished , Other methods don't trigger queries , such as blog.getName();

3、 If it's on aggressiveLazyLoading=true, Other methods also trigger queries , such as blog.getName().

problem : Why can we delay loading ?

blog.getAuthor(), It's just a way to get properties , There is no code to connect to the database , Why does it trigger a query to the database ?

It's because our class is represented

System.out.println(blog.getClass());
The print is wrong

class com.zzjson.domain.associate.BlogAndAuthor_$$_jvst70_0
After the name of this class is jvst, yes JAVASSIST Abbreviation

​ When the delay loading switch is turned on , How an object becomes a proxy object ?

​ DefaultResultSetHandler.createResultObject()

​ Since it's a proxy object , Then there must be a way to create a proxy object . What do we have to implement dynamic generation The way of reasoning ?

​ That's why settings There is a ProxyFactory attribute .MyBatis By default JAVASSIST Create proxy object . It can also be changed to CGLIB, It's time to introduce CGLIB My bag .

CGLIB and JAVASSIST What's the difference ?

Test it , We put the default JAVASSIST It is amended as follows CGLIB, Print this object again .

Pagination
RowBounds
public void testSelectByRowBounds() throws IOException {
SqlSession session = sqlSessionFactory.openSession();
try {
BlogMapper mapper = session.getMapper(BlogMapper.class);
int start = 0; // offset
int pageSize = 5; // limit
RowBounds rb = new RowBounds(start, pageSize);
List<Blog> list = mapper.selectBlogList(rb); //  Use logical paging
for(Blog b :list){
System.out.println(b);
}
} finally {
session.close();
}
}
Parameters of the incoming RowBounds

It's a pseudo pagination , In fact, all of them will be queried first , And then how many
org.apache.ibatis.executor.resultset.DefaultResultSetHandler#handleRowValuesForSimpleResultMap

image-20210116151119131

Manual limit
<select id="selectBlogPage" parameterType="map" resultMap="BaseResultMap">
select * from blog limit #{curIndex} , #{pageSize}
</select>
Need to be in java The code calculates the serial number

PageHelper
https://github.com/pagehelper/Mybatis-PageHelper

Using plug-ins
ThreadLocal To set up
rely on
<dependency>
<groupId>com.github.pagehelper</groupId>
<artifactId>pagehelper</artifactId>
<version>x.x.x</version>
</dependency>
The plug-in configuration
<plugins>
<plugin interceptor="com.github.pagehelper.PageInterceptor">
<!-- config params as the following -->
<property name="param1" value="value1"/>
</plugin>
</plugins>
Use
Static method calls
// For the first 1 page ,10 Article content , Default total number of queries count
PageHelper.startPage(1, 10);
PageInfo
// For the first 1 page ,10 Article content , Default total number of queries count
PageHelper.startPage(1, 10);
List<User> list = userMapper.selectAll();
// use PageInfo Package the results
PageInfo page = new PageInfo(list);
Parameters of the way
<plugins>
<!-- com.github.pagehelper by PageHelper The package name of the class  -->
<plugin interceptor="com.github.pagehelper.PageInterceptor">
<!--  Use the following method to configure parameters , All parameters will be introduced later  -->
<property name="supportMethodsArguments" value="true"/>
<property name="params" value="pageNum=pageNumKey;pageSize=pageSizeKey;"/>
</plugin>
</plugins>
List<User> selectByPageNumSize(
@Param("user") User user,
@Param("pageNumKey") int pageNum,
@Param("pageSizeKey") int pageSize);
MybatisGenerator
https://github.com/mybatis/generator

​ We use... In projects MyBaits When , For a table that needs to be operated , need Create entity class 、 Mapper mapper 、Mapper Interface , There are many fields and method configurations in it , This part of the job is Very cumbersome . And most of the time we operate on the same table , For example, query according to the primary key 、 according to Map Inquire about 、 Single insertion 、 Batch insert 、 Delete by primary key, etc . When we have a lot of watches , signify There's a lot of repetitive work . So is there a way , According to our table , Automatic generation Entity class 、Mapper mapper 、Mapper Interface , It contains the basic methods we need to use and SQL Well ?

​ MyBatis It also provides such a thing , be called MyBatis Generator, abbreviation MBG. We just need to modify one configuration file , Use related jar Package command or Java Code can help us generate entity classes 、 Mapper and interface file . Don't know how to use it. MyBatis Are you like me back then , Or a field of an entity class , A method of interface , One by one of the mapper SQL To write .

​ MBG There is one in the configuration file of Example The switch of , This thing is used to construct complex screening conditions , In other words, according to our code to generate where Conditions

​ principle : In the entity class, there are two... With inheritance relationship Criteria, Use the automatic generation method to build query conditions . Include this in Criteria The entity class of is passed to the query parameter as a parameter , In parsing Mapper Mapper will be converted to SQL Conditions .

(mybatis-standalone engineering :

com.zzjson.domain.BlogExample

com.zzjson.BlogExampleTest)

BlogExample It contains one, two Criteria:

image-20190709204628387

example : Inquire about bid=1 Of Blog, By creating a Criteria To build query conditions :

BlogMapper mapper = session.getMapper(BlogMapper.class);
BlogExample example = new BlogExample();
BlogExample.Criteria criteria = example.createCriteria();
criteria.andBidEqualTo(1);
List<Blog> list = mapper.selectByExample(example);
Generated statements

select 'true' as QUERYID, bid, name, author_id from blog WHERE ( bid = ? )
Page turning
​ In the age of writing stored procedures , Turning pages is also a very difficult thing to debug , We want to return the data accurately , It takes a lot of debugging and modification . But if you've written it yourself , You can understand the principle of pagination .

​ In our operation of querying the database , There are two ways to turn pages , One is logical page turning ( Fake paging ), One is physical flipping ( True Pagination ). The principle of logical page turning is to find out all the data , Delete and select data in memory . Physical flipping is real flipping , such as MySQL Use limit sentence ,Oracle Use rownum sentence ,SQLServer Use top sentence .

Logic turns the page
MyBatis There's a logical paging object in it RowBounds, There are two main attributes ,offset and limit( Start with the number , How many to look up ).

We can do it in Mapper Add this parameter to the method of the interface , It doesn't need to be modified xml Inside SQL sentence .

public List<Blog> selectBlogList(RowBounds rowBounds);
Use :mybatis-standalone- MyBatisTest-testSelectByRowBounds()

int start = 10; // offset, What line do you start with  
int pageSize = 5; // limit, How many to look up  
RowBounds rb = new RowBounds(start, pageSize);
List<Blog> list = mapper.selectBlogList(rb); for(Blog b :list){
System.out.println(b);
}
​ The bottom of it is actually right ResultSet To deal with . It will abandon the front offset Data , And then take the rest of the data limit strip .

// DefaultResultSetHandler.java
private void handleRowValuesForSimpleResultMap(ResultSetWrapper rsw, ResultMap resultMap, ResultHandler<?> resultHandler, RowBounds rowBounds, ResultMapping parentMapping) throws SQLException {
DefaultResultContext<Object> resultContext = new DefaultResultContext();
ResultSet resultSet = rsw.getResultSet();
this.skipRows(resultSet, rowBounds);
while(this.shouldProcessMoreRows(resultContext, rowBounds) && !resultSet.isClosed() && resultSet.next()) {
ResultMap discriminatedResultMap = this.resolveDiscriminatedResultMap(resultSet,
resultMap, (String)null);
Object rowValue = this.getRowValue(rsw, discriminatedResultMap, (String)null);
this.storeObject(resultHandler, resultContext, rowValue, parentMapping, resultSet); }
}
​ Obviously , If there's a lot of data , This kind of page flipping is inefficient ( Query to memory and use it again subList(start,end) No difference ). So we're going to use physics to turn the page .

Physics turns the page
Physical flipping is real flipping , It turns pages through statements supported by the database

The first simple way is to pass in parameters ( Or package one page object ), stay SQL Turn the page in the sentence .

<select id="selectBlogPage" parameterType="map" resultMap="BaseResultMap">
  select * from blog limit #{curIndex} , #{pageSize}
</select>
​ The first problem is that we are going to Java Start and end serial numbers are calculated in the code ; The second question is : Every one that needs to turn the page Statement We have to write limit sentence , Can cause Mapper There is a lot of code redundancy in mapper .

Then we need a universal way , You don't need to modify any of the configuration SQL sentence , As long as I Where you need to turn the page, just encapsulate the page turning object .

​ Our most common method is to use the page flipping plug-in , This is based on MyBatis Interceptor implementation of , such as PageHelper.

// pageSize  A few on each page
PageHelper.startPage(pn, 10);
List<Employee> emps = employeeService.getAll(); // navigatePages  Number of navigation pages
PageInfo page = new PageInfo(emps, 10);
return Msg.success().add("pageInfo", page);
​ PageHelper It's through MyBatis Interceptor implementation of , We will analyze the specific principle of plug-ins later . To put it simply , It will be based on PageHelper Parameters of , Rewrite our SQL sentence . such as MySQL Will generate limit sentence ,Oracle Will generate rownum sentence ,SQL Server Will generate top sentence .

Universal Mapper
​ problem : When our table fields change , We need to modify the entity class and Mapper File defined fields and methods . If it's incremental maintenance , So one file after another to modify . If it's a full replacement , We have to compare it with MBG Generated files . Once a field changes, it needs to be modified , It's very troublesome to maintain .

​ Solve this problem , We have two ideas .

​ first , because MyBatis Of Mapper It's in favor of inheritance ( see https://github.com/mybatis/mybatis-3/issues/35 ) . the With I People can With hold I People Of Mapper.xml and Mapper Interfaces are divided into two files . One is MBG Generated , This part is fixed . Then create DAO Class inherits the generated interface , The part of the change is DAO Internal maintenance .

mybatis-standalone engineering :

public interface BlogMapperExt extends BlogMapper {
public Blog selectBlogByName(String name);
}
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.zzjson.mapper.BlogMapperExt">
  <!--  Can only inherit statement, Cannot inherit sql、resultMap Such as tag  -->
  <resultMap id="BaseResultMap" type="blog">
    <id column="bid" property="bid" jdbcType="INTEGER"/>
    <result column="name" property="name" jdbcType="VARCHAR"/>
    <result column="author_id" property="authorId" jdbcType="INTEGER"/>
  </resultMap>

  <!--  stay parent xml  and child xml  Of  statement id In the same case , Will use child xml  Of statement id -->
  <select id="selectBlogByName" resultMap="BaseResultMap" statementType="PREPARED">
    select *
    from blog
    where name = #{name}
  </select>
</mapper>
So in the future, just change Ext That's fine .

There's a drawback to this , There will be more files .

​ Since the basic method of generating each table is the same , In other words, the code of common methods is the same , Can we merge this part into one file , Let it support generics ? Write a generic interface , For example GPBaseMapper<T>, Pass the entity class as a parameter Enter into . This interface defines a large number of basic methods for adding, deleting, modifying and querying , These methods all support generics . Self defined Mapper Interface inherits the generic interface , for example BlogMapper extends GPBaseMapper<Blog>, Get the operation method of entity class automatically . There's no way , We are still It can be in our own Mapper It's written in . The solutions we can think of , Someone has done this for a long time , This thing is called

Universal Mapper. https://github.com/abel533/Mapper/wiki

​ purpose : It mainly solves the problem of adding, deleting, modifying and querying single table , It is not suitable for the scenario of multi table Association query .

Apart from the problem of configuration file changes , Universal Mapper It can also solve :

Every Mapper A lot of definitions of repetitive methods in interfaces ;
Mask the differences between databases ;
Provide the method of batch operation ;
Implement paging .
Universal Mapper and PageHelper The author is the same person ( Liu Zenghui ).

Usage mode : stay Spring When used in , introduce jar package , Replace applicationContext.xml Medium sqlSessionFactory and configure.

<bean class="tk.mybatis.spring.mapper.MapperScannerConfigurer">
  <property name="backPackage" value="com.zzjson.crud.dao"/>
</bean
Mybatis-Plus
https://mybatis.plus/guide

MyBatis-Plus It's original MyBatis An enhancement tool for , You can use native MyBatis All of the On the basis of function , Use plus Unique function .

MyBatis-Plus Core functions :

Universal CRUD:

​ Well defined Mapper After the interface , Just inherit BaseMapper<T> The interface can obtain the general function of adding, deleting, modifying and checking , There is no need to write any interface methods and configuration files . Conditional constructor : adopt EntityWrapper<T>( Physical packaging class ), Can be used for splicing SQL sentence , And support sorting 、 Group query and so on SQL. Code generator : Support a series of policy configuration and global configuration , Than MyBatis Better code generation for . in addition MyBatis-Plus It also has paging function .

My note warehouse address gitee Come on, give me some Star Well

版权声明
本文为[The road of architecture in the golden age]所创，转载请带上原文链接，感谢
https://cdmana.com/2021/01/20210117131831933m.html


#### p

#Mybatis通用Mapper

##极其方便的使用Mybatis单表的增删改查

##优点?

不客气的说,使用这个通用Mapper甚至能改变你对Mybatis单表基础操作不方便的想法,使用它你能简单的使用单表的增删改查,包含动态的增删改查.

程序使用拦截器实现具体的执行Sql,完全使用原生的Mybatis进行操作.

你还在因为数据库表变动重新生成xml吗?还是要手动修改自动生成的insert|update|delete的xml呢?赶紧使用通用Mapper,表的变动只需要实体类保持一致,不用管基础的xml,你不止会拥有更多的时间陪老婆|孩子|女朋友|打DOTA,你也不用做哪些繁琐无聊的事情,感兴趣了吗?继续看如何使用吧!!相信这个通用的Mapper会让你更方便的使用Mybatis,这是一个强大的Mapper!!!

不管你信不信,这个项目的测试代码中没有一个Mapper的xml配置文件,但是却可以做到每个Mapper对应上百行xml才能完成的许多功能.没有了这些基础xml信息的干扰,你将会拥有清晰干净的Mapper.xml.

发现BUG可以提Issue,可以给我发邮件,可以加我QQ,可以进Mybatis群讨论.

作者博客：http://blog.csdn.net/isea533

作者QQ： 120807756

作者邮箱： abel533@gmail.com

Mybatis工具群： 211286137 (Mybatis相关工具插件等等)

推荐使用Mybatis分页插件:PageHelper分页插件

##v0.2.0版本说明

该版本做了大量的重构，在原有基础上增加了两个类，分别为MapperTemplate和MapperProvider，其他几个类都有相当大的改动。

但是，这次重构并不影响原有的业务代码。

这次重构的目的是为了方便开发者自行扩展，增加自己需要的通用Mapper。这次重构后，扩展变的更容易。稍后会写一篇如何进行扩展的文档。

这次更新还修复Oracle序列的BUG。

##如何开发自己的通用Mapper

##如何使用?

下面是通用Mapper的配置方法,还会提到Spring中的配置方法.还有和PageHelper分页插件集成的配置方式.

###1. 引入通用Mapper的代码

将本项目中的4个代码文件(EntityHelper,Mapper,MapperHelper,MapperInterceptor)复制到你自己的项目中.

项目依赖于JPA的注解,需要引入persistence-api-1.0.jar或者添加Maven依赖:

<dependency>
  <groupId>javax.persistence</groupId>
  <artifactId>persistence-api</artifactId>
  <version>1.0</version>
</dependency>
###2. 配置Mapper拦截器

在mybatis-config.xml中添加如下配置:

<plugins>
  <plugin interceptor="com.github.abel533.mapper.MapperInterceptor">
    <!--================================================-->
    <!--可配置参数说明(一般无需修改)-->
    <!--================================================-->
    <!--UUID生成策略-->
    <!--配置UUID生成策略需要使用OGNL表达式-->
    <!--默认值32位长度:@java.util.UUID@randomUUID().toString().replace("-", "")-->
    <!--<property name="UUID" value="@java.util.UUID@randomUUID().toString()"/>-->
    <!--主键自增回写方法,默认值MYSQL,详细说明请看文档-->
    <property name="IDENTITY" value="HSQLDB"/>
    <!--序列的获取规则,使用{num}格式化参数，默认值为{0}.nextval，针对Oracle-->
    <!--可选参数一共3个，对应0,1,2,分别为SequenceName，ColumnName,PropertyName-->
    <property name="seqFormat" value="{0}.nextval"/>
    <!--主键自增回写方法执行顺序,默认AFTER,可选值为(BEFORE|AFTER)-->
    <!--<property name="ORDER" value="AFTER"/>-->
    <!--通用Mapper接口，多个通用接口用逗号隔开-->
    <property name="mappers" value="com.github.abel533.mapper.Mapper"/>
  </plugin>
</plugins>
mappers参数：这里先记住是通用Mapper的全限定路径即可。后面讲如何扩展时，会详细介绍。

####INENTITY参数配置

对于不同的数据库，需要配置不同的参数，这些参数如下：

DB2: VALUES IDENTITY_VAL_LOCAL()
MYSQL: SELECT LAST_INSERT_ID()
SQLSERVER: SELECT SCOPE_IDENTITY()
CLOUDSCAPE: VALUES IDENTITY_VAL_LOCAL()
DERBY: VALUES IDENTITY_VAL_LOCAL()
HSQLDB: CALL IDENTITY()
SYBASE: SELECT @@IDENTITY
DB2_MF: SELECT IDENTITY_VAL_LOCAL() FROM SYSIBM.SYSDUMMY1
INFORMIX: select dbinfo('sqlca.sqlerrd1') from systables where tabid=1
为了配置的时候方便，可以直接使用这里的数据库名字进行配置，例如:

<plugins>
  <plugin interceptor="com.github.abel533.mapper.MapperInterceptor">
    <property name="IDENTITY" value="DB2"/>
  </plugin>
</plugins>
如果这里的值不是上面所提到的数据库，就会使用直接提供的语句。例如下面的这个配置和上面的效果一样：

<plugins>
  <plugin interceptor="com.github.abel533.mapper.MapperInterceptor">
    <property name="IDENTITY" value="VALUES IDENTITY_VAL_LOCAL()"/>
  </plugin>
</plugins>
附:Spring配置相关

如果你使用Spring的方式来配置该拦截器,你可以像下面这样:

<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
  <property name="dataSource" ref="dataSource"/>
  <property name="mapperLocations">
    <array>
      <value>classpath:mapper/*.xml</value>
    </array>
  </property>
  <property name="typeAliasesPackage" value="com.isea533.mybatis.model"/>
  <property name="plugins">
    <array>
      <-- 主要看这里 -->
      <bean class="com.isea533.mybatis.mapperhelper.MapperInterceptor"/>
    </array>
  </property>
</bean>
只需要像上面这样配置一个bean即可.

如果你同时使用了PageHelper分页插件,可以像下面这样配置:

<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
  <property name="dataSource" ref="dataSource"/>
  <property name="mapperLocations">
    <array>
      <value>classpath:mapper/*.xml</value>
    </array>
  </property>
  <property name="typeAliasesPackage" value="com.isea533.mybatis.model"/>
  <property name="plugins">
    <array>
      <bean class="com.isea533.mybatis.pagehelper.PageHelper">
        <property name="properties">
          <value>
            dialect=hsqldb
            reasonable=true
          </value>
        </property>
      </bean>
      <bean class="com.isea533.mybatis.mapperhelper.MapperInterceptor"/>
    </array>
  </property>
</bean>
一定要注意PageHelper和MapperInterceptor这两者的顺序不能颠倒.

如果你想配置MapperInterceptor的参数,可以像PageHelper中的properties参数这样配置

###3. 继承通用的Mapper<T>,必须指定泛型<T>

例如下面的例子:

public interface UserInfoMapper extends Mapper<UserInfo> {
//其他必须手写的接口...

}
一旦继承了Mapper<T>,继承的Mapper就拥有了以下通用的方法:

//根据实体类不为null的字段进行查询,条件全部使用=号and条件
List<T> select(T record);

//根据实体类不为null的字段查询总数,条件全部使用=号and条件
int selectCount(T record);

//根据主键进行查询,必须保证结果唯一
//单个字段做主键时,可以直接写主键的值
//联合主键时,key可以是实体类,也可以是Map
T selectByPrimaryKey(Object key);

//插入一条数据
//支持Oracle序列,UUID,类似Mysql的INDENTITY自动增长(自动回写)
//优先使用传入的参数值,参数值空时,才会使用序列、UUID,自动增长
int insert(T record);

//插入一条数据,只插入不为null的字段,不会影响有默认值的字段
//支持Oracle序列,UUID,类似Mysql的INDENTITY自动增长(自动回写)
//优先使用传入的参数值,参数值空时,才会使用序列、UUID,自动增长
int insertSelective(T record);

//根据实体类中字段不为null的条件进行删除,条件全部使用=号and条件
int delete(T key);

//通过主键进行删除,这里最多只会删除一条数据
//单个字段做主键时,可以直接写主键的值
//联合主键时,key可以是实体类,也可以是Map
int deleteByPrimaryKey(Object key);

//根据主键进行更新,这里最多只会更新一条数据
//参数为实体类
int updateByPrimaryKey(T record);

//根据主键进行更新
//只会更新不是null的数据
int updateByPrimaryKeySelective(T record);
###4. 泛型(实体类)<T>的类型必须符合要求

实体类按照如下规则和数据库表进行转换,注解全部是JPA中的注解:

表名默认使用类名,驼峰转下划线(只对大写字母进行处理),如UserInfo默认对应的表名为user_info。

表名可以使用@Table(name = "tableName")进行指定,对不符合第一条默认规则的可以通过这种方式指定表名.

字段默认和@Column一样,都会作为表字段,表字段默认为Java对象的Field名字驼峰转下划线形式.

可以使用@Column(name = "fieldName")指定不符合第3条规则的字段名

使用@Transient注解可以忽略字段,添加该注解的字段不会作为表字段使用.

建议一定是有一个@Id注解作为主键的字段,可以有多个@Id注解的字段作为联合主键.

默认情况下,实体类中如果不存在包含@Id注解的字段,所有的字段都会作为主键字段进行使用(这种效率极低).

实体类可以继承使用,可以参考测试代码中的com.github.abel533.model.UserLogin2类.

由于基本类型,如int作为实体类字段时会有默认值0,而且无法消除,所以实体类中建议不要使用基本类型.

除了上面提到的这些,Mapper还提供了序列(支持Oracle)、UUID(任意数据库,字段长度32)、主键自增(类似Mysql,Hsqldb)三种方式，其中序列和UUID可以配置多个，主键自增只能配置一个。

这三种方式不能同时使用,同时存在时按照 序列>UUID>主键自增的优先级进行选择.下面是具体配置方法:

使用序列可以添加如下的注解:
//可以用于数字类型,字符串类型(需数据库支持自动转型)的字段
@SequenceGenerator(name="Any",sequenceName="seq_userid")
@Id
private Integer id;
该字段不会回写。

使用UUID时:
//可以用于任意字符串类型长度超过32位的字段
@GeneratedValue(generator = "UUID")
private String countryname;
该字段不会回写。

使用主键自增:
//不限于@Id注解的字段,但是一个实体类中只能存在一个(继承关系中也只能存在一个)
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private Integer id;
增加这个注解后，会回写ID。

通过设置@GeneratedValue的generator参数可以支持更多的获取主键的方法，例如在Oracle中使用序列：

@Id
@GeneratedValue(strategy = GenerationType.IDENTITY,generator = "select SEQ_ID.nextval from dual")
private Integer id;
使用Oracle序列的时候，还需要配置:

<property name="ORDER" value="BEFORE"/>
因为在插入数据库前，需要先获取到序列值，否则会报错。

###5. 将继承的Mapper接口添加到Mybatis配置中

例如本项目测试中的配置:

<mappers>
  <mapper class="com.github.abel533.mapper.CountryMapper" />
  <mapper class="com.github.abel533.mapper.Country2Mapper" />
  <mapper class="com.github.abel533.mapper.CountryTMapper" />
  <mapper class="com.github.abel533.mapper.CountryUMapper" />
  <mapper class="com.github.abel533.mapper.CountryIMapper" />
  <mapper class="com.github.abel533.mapper.UserInfoMapper" />
  <mapper class="com.github.abel533.mapper.UserLoginMapper" />
  <mapper class="com.github.abel533.mapper.UserLogin2Mapper" />
</mappers>
附:Spring配置相关

如果你在Spring中配置Mapper接口,不需要像上面这样一个个配置,只需要有下面的这个扫描Mapper接口的这个配置即可:

<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
  <property name="basePackage" value="com.isea533.mybatis.mapper"/>
</bean>
###6. 代码中使用

例如下面这个简单的例子:

SqlSession sqlSession = MybatisHelper.getSqlSession();
try {
//获取Mapper
UserInfoMapper mapper = sqlSession.getMapper(UserInfoMapper.class);
UserInfo userInfo = new UserInfo();
userInfo.setUsername("abel533");
userInfo.setPassword("123456");
userInfo.setUsertype("2");
userInfo.setEmail("abel533@gmail.com");
//新增一条数据
Assert.assertEquals(1, mapper.insert(userInfo));
//ID回写,不为空
Assert.assertNotNull(userInfo.getId());
//6是当前的ID
Assert.assertEquals(6, (int)userInfo.getId());
//通过主键删除新增的数据
Assert.assertEquals(1,mapper.deleteByPrimaryKey(userInfo));
} finally {
sqlSession.close();
}
另一个例子:

SqlSession sqlSession = MybatisHelper.getSqlSession();
try {
//获取Mapper
CountryMapper mapper = sqlSession.getMapper(CountryMapper.class);
//查询总数
Assert.assertEquals(183, mapper.selectCount(new Country()));
//查询100
Country country = mapper.selectByPrimaryKey(100);
//根据主键删除
Assert.assertEquals(1, mapper.deleteByPrimaryKey(100));
//查询总数
Assert.assertEquals(182, mapper.selectCount(new Country()));
//插入
Assert.assertEquals(1, mapper.insert(country));
} finally {
sqlSession.close();
}
附:Spring使用相关

直接在需要的地方注入Mapper继承的接口即可,和一般情况下的使用没有区别.

###7.其他

如果你的实体是继承Map的，你可能需要将数据库查询的结果从大写下划线形式转换为驼峰形式，你可以搭配下面的拦截器使用：

CameHumpInterceptor - Map结果的Key转为驼峰式

http://git.oschina.net/free/Mybatis_Utils/tree/master/CameHumpMap

##当前版本v0.2.0

##这是一个新生的开源项目

首先感谢您能看到这里!

这是一个新生的项目,一切都刚刚开始,虽然项目中包含大量的测试,但是仍然会有很多未知的bug存在,希望各位能够在使用过程中发现问题时及时反馈,欢迎各位fork本项目进行参与!


#### p

```markdown
maven 依赖
1
2
3
4
5
6
7
8
9
<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
	<scope>runtime</scope>
<dependency>
	<groupId>org.mybatis.spring.boot</groupId>
	<artifactId>mybatis-spring-boot-starter</artifactId>
	<version>2.1.2</version>
</dependency>
配置
1
2
3
4
5
6
7
8
spring:
    datasource:
        username: root
        password: 123456
url: jdbc:mysql://127.0.0.1:3306/test

mybatis:
    mapperLocations: classpath:mapper/**/*.xml
基本用法
1
2
3
4
5
6
@Mapper
public interface TestMapper {

	// @Select("select * from todo limit 2")
	List<Map<String,Object>> findTodos();
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"   "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.justdoit.springboottest.mapper.TestMapper">
	<!-- 开启基于redis的二级缓存 -->
	<!-- <cache type="com.justdoit.springboottest.config.MybatisCacheConfig" /> -->


	<select id="findTodos" resultType="java.util.Map">
		SELECT
			*
		FROM
			todo
		limit 3
	</select>
</mapper>
最佳实践
多个参数
1
2
@Update("update role set role_name = #{role.roleName}, role_name_zh = #{role.roleNameZh} where id = #{id}")
public void update(int id, RoleParam role);
分页
PageHelper
依赖
配置
startPage
pageInfo
1
2
3
4
5
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.3.0</version>
</dependency>
1
2
3
4
5
6
7
8
9
10
11
12
// 第几页
int currentPage = 2;
// 每页数量
int pageSize = 5;
// 排序
String orderBy = "id desc";
PageHelper.startPage(currentPage, pageSize, orderBy);
List<Map<String, Object>> todos = testMapper.findTodos();
PageInfo<Map<String, Object>> pageInfo = new PageInfo<>(todos);
log.info(pageInfo.toString());

return todos;
like 模糊查询
在代码中加上%
1
List<User> test = userMapper.findUserByLikeName2("%" +name+"%");
1
2
3
<select id="findUserByLikeName2" parameterType="java.lang.String" resultMap="user">
	select * from t_user where name like #{name,jdbcType=VARCHAR}
</select>
动态 SQL
if
1
2
3
4
5
6
7
8
9
10
11
12
13
14
<select id="findActiveBlogWithTitleLike" resultType="Blog">
	SELECT
		*
	FROM
		BLOG
	WHERE
		state = ‘ACTIVE’
		<if test="title != null">
    	AND title like #{title}
		</if>
		<if test="author != null and author.name != null">
		AND author_name like #{author.name}
		</if>
</select>
choose、when、otherwise
从多个条件中选择一个使用

1
2
3
4
5
6
7
8
9
10
11
12
13
14
<select id="findActiveBlogLike" resultType="Blog">
	SELECT * FROM BLOG WHERE state = ‘ACTIVE’
	<choose>
		<when test="title != null">
		AND title like #{title}
		</when>
		<when test="author != null and author.name != null">
		AND author_name like #{author.name}
		</when>
		<otherwise>
		AND featured = 1
		</otherwise>
	</choose>
</select>
where
1
2
3
4
5
6
7
8
9
10
11
12
13
14
<select id="findActiveBlogLike" resultType="Blog">
	SELECT * FROM BLOG
	<where>
		<if test="state != null">
	state = #{state}
		</if>
		<if test="title != null">
	AND title like #{title}
		</if>
		<if test="author != null and author.name != null">
	AND author_name like #{author.name}
		</if>
	</where>
</select>
set
1
2
3
4
5
6
7
8
9
10
<update id="updateAuthorIfNecessary">
	update Author
	<set>
		<if test="username != null">username=#{username},</if>
		<if test="password != null">password=#{password},</if>
		<if test="email != null">email=#{email},</if>
		<if test="bio != null">bio=#{bio}</if>
	</set>
	where id=#{id}
</update>
foreach
item：集合中元素迭代时的别名，该参数为必选。
index：在 list 和数组中,index 是元素的序号，在 map 中，index 是元素的 key，该参数可选
open：foreach 代码的开始符号，一般是(和 close=”)”合用。常用在 in(),values()时。该参数可选
separator：元素之间的分隔符，例如在 in()的时候，separator=”,”会自动在元素中间用“,“隔开，避免手动输入逗号导致 sql 错误，如 in(1,2,)这样。该参数可选。
close: foreach 代码的关闭符号，一般是)和 open=”(“合用。常用在 in(),values()时。该参数可选。
collection: 要做 foreach 的对象，作为入参时，List 对象默认用”list”代替作为键，数组对象有”array”代替作为键，Map 对象没有默认的键。当然在作为入参时可以使用@Param(“keyName”)来设置键，设置 keyName 后，list,array 将会失效。 除了入参这种情况外，还有一种作为参数对象的某个字段的时候。举个例子：如果 User 有属性 List ids。入参是 User 对象，那么这个 collection = “ids”.如果 User 有属性 Ids ids;其中 Ids 是个对象，Ids 有个属性 List id;入参是 User 对象，那么 collection = “ids.id”
如果传入的是单参数且参数类型是一个 List 的时候，collection 属性值为 list .
如果传入的是单参数且参数类型是一个 array 数组的时候，collection 的属性值为 array .
如果传入的参数是多个的时候，我们就需要把它们封装成一个 Map 了，当然单参数也可以封装成 map，实际上如果你在传入参数的时候，在 MyBatis 里面也是会把它封装成一个 Map 的，map 的 key 就是参数名，所以这个时候 collection 属性值就是传入的 List 或 array 对象在自己封装的 map 里面的 key.

1
2
3
4
5
6
7
8
9
10
<select id="insertWeeklyCost" parameterType="java.util.List">
	insert into weekly_cost(game_id,date,epiboly_cost,publicity_cost)
	values
	<foreach collection="list" item="element" index="index" open="(" separator="),("  close=")">
		#{element.gameId},
		#{element.date},
		#{element.epiboly_cost},
		#{element.publicity_cost}
	</foreach>
</select>
一级缓存
二级缓存
1
<cache type="com.justdoit.springboottest.config.MybatisCacheConfig" />


```

#### p
#### p
#### p

### references
- <https://mybatis.org/mybatis-3/getting-started.html>
- <https://mybatis.org/mybatis-3/sqlmap-xml.html>
- <https://www.baeldung.com/spring-mybatis>
- <https://cdmana.com/2021/01/20210117131938364g.html>
- <https://github.com/hibatis/hibatis>
- <https://dalufanjiadan.github.io/2019/09/14/2019-09-14-03/>
- <>
