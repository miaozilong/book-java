Most JDBC drivers provide improved performance if you batch multiple calls to the same prepared statement. By grouping updates into batches you limit the number of round trips to the database.

参考：

https://docs.spring.io/spring/docs/current/spring-framework-reference/html/jdbc.html\#jdbc-advanced-jdbc

