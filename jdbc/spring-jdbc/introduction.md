# JDBC类库介绍

常用的类库：Hibernate,MyBatis/iBatis,Toplink,DBUtils,JdbcTemplate

# JDBC的尴尬

![](/assets/20130619102459-708751837.jpg)

JDBC作为Java平台的访问关系数据库的标准，其成功是 有目共睹的。几乎所有java平台的数据访问，都直接或者间接的使用了JDBC，它是整个java平台面向关系数据库进行数据访问的基石。

作为一个标准，无疑JDBC是很成功的，但是要说JDBC在使用过程当中多么的受人欢迎，则不尽然了。JDBC主要是面向较为底层的数据库操作，所以在设计的过程当中 ，比较的贴切底层以提供尽可能多的功能特色。从这个角度来说，JDBC API的设计无可厚非。可是，过于贴切底层的API的设计，对于开发人员则未必是一件好事。即使执行一个最简单的查询，开发人员也要按照API的规矩写上一大堆雷同的代码，如果不能合理的封装使用JDBC API，在项目中使用JDBC访问数据所出现的问题估计会使人发疯！

# 为什么要使用JDBCTemplate

While working with the database using plain old JDBC, it becomes cumbersome to write unnecessary code to handle exceptions, opening and closing database connections, etc. However, Spring JDBC Framework takes care of all the low-level details starting from opening the connection, prepare and execute the SQL statement, process exceptions, handle transactions and finally close the connection.

# **Spring JDBC - who does what?**

| Action | Spring | You |
| :--- | :--- | :--- |


| Define connection parameters. |  | X |
| :--- | :--- | :--- |


| Open the connection. | X |  |
| :--- | :--- | :--- |


| Specify the SQL statement. |  | X |
| :--- | :--- | :--- |


| Declare parameters and provide parameter values |  | X |
| :--- | :--- | :--- |


| Prepare and execute the statement. | X |  |
| :--- | :--- | :--- |


| Set up the loop to iterate through the results \(if any\). | X |  |
| :--- | :--- | :--- |


| Do the work for each iteration. |  | X |
| :--- | :--- | :--- |


| Process any exception. | X |  |
| :--- | :--- | :--- |


| Handle transactions. | X |  |
| :--- | :--- | :--- |


| Close the connection, statement and resultset. | X |  |
| :--- | :--- | :--- |




