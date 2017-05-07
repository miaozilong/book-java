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



