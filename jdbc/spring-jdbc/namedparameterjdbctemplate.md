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

One nice feature related to the`NamedParameterJdbcTemplate`\(and existing in the same Java package\) is the`SqlParameterSource`interface. You have already seen an example of an implementation of this interface in one of the previous code snippet \(the`MapSqlParameterSource`class\). An`SqlParameterSource`is a source of named parameter values to a`NamedParameterJdbcTemplate`. The`MapSqlParameterSource`class is a very simple implementation that is simply an adapter around a`java.util.Map`, where the keys are the parameter names and the values are the parameter values.

Another`SqlParameterSource`implementation is the`BeanPropertySqlParameterSource`class. This class wraps an arbitrary JavaBean \(that is, an instance of a class that adheres to[the JavaBean conventions](http://www.oracle.com/technetwork/java/javase/documentation/spec-136004.html)\), and uses the properties of the wrapped JavaBean as the source of named parameter values.

```java
public class Actor {

    private Long id;
    private String firstName;
    private String lastName;

    public String getFirstName() {
        return this.firstName;
    }

    public String getLastName() {
        return this.lastName;
    }

    public Long getId() {
        return this.id;
    }

    // setters omitted...

}
```

```java
// some JDBC-backed DAO class...
private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

public void setDataSource(DataSource dataSource) {
    this.namedParameterJdbcTemplate = new NamedParameterJdbcTemplate(dataSource);
}

public int countOfActors(Actor exampleActor) {

    // notice how the named parameters match the properties of the above 'Actor' class
    String sql = "select count(*) from T_ACTOR where first_name = :firstName and last_name = :lastName";

    SqlParameterSource namedParameters = new BeanPropertySqlParameterSource(exampleActor);

    return this.namedParameterJdbcTemplate.queryForObject(sql, namedParameters, Integer.class);
}
```

Remember that the NamedParameterJdbcTemplate class wraps a classic JdbcTemplate template; if you need access to the wrapped JdbcTemplate instance to access functionality only present in the JdbcTemplate class, you can use the getJdbcOperations\(\) method to access the wrapped JdbcTemplate through the JdbcOperations interface.

