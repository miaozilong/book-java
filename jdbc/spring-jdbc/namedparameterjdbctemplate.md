NamedParameterJdbcTemplate能让JDBC执行时语句带上命名参数 而不在仅仅使用之前使用的"?"作为参数，NamedParameterJdbcTemplate是在JdbcTemplate基础上进行了封装，本节只介绍NamedParameterJdbcTemplate与JdbcTemplate不同之处

```java
// some JDBC-backed DAO class...
private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

public void setDataSource(DataSource dataSource) {
    this.namedParameterJdbcTemplate = new NamedParameterJdbcTemplate(dataSource);
}

public int countOfActorsByFirstName(String firstName) {

    String sql = "select count(*) from T_ACTOR where first_name = :first_name";

    SqlParameterSource namedParameters = new MapSqlParameterSource("first_name", firstName);

    return this.namedParameterJdbcTemplate.queryForObject(sql, namedParameters, Integer.class);
}
```

Notice the use of the named parameter notation in the value assigned to the sql variable, and the corresponding value that is plugged into the namedParameters variable \(of type MapSqlParameterSource\).

sql语句中使用 :变量名 作为可变参数，真正的值使用MapSqlParameterSource对象插入到语句中

Alternatively, you can pass along named parameters and their corresponding values to a NamedParameterJdbcTemplate instance by using the Map-based style.The remaining methods exposed by the NamedParameterJdbcOperations and implemented by the NamedParameterJdbcTemplate class follow a similar pattern and are not covered here.

同样，也可使用Map的样式插入变量到NamedParameterJdbcTemplate对象中

```java
// some JDBC-backed DAO class...
private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

public void setDataSource(DataSource dataSource) {
    this.namedParameterJdbcTemplate = new NamedParameterJdbcTemplate(dataSource);
}

public int countOfActorsByFirstName(String firstName) {

    String sql = "select count(*) from T_ACTOR where first_name = :first_name";

    Map<String, String> namedParameters = Collections.singletonMap("first_name", firstName);

    return this.namedParameterJdbcTemplate.queryForObject(sql, namedParameters,  Integer.class);
}
```



