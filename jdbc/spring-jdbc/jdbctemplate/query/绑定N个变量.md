```java

```

The SQL standard allows for selecting rows based on an expression that includes a variable list of values. A typical example would be

`select * from T_ACTOR where id in (1, 2, 3)`

. This variable list is not directly supported for prepared statements by the JDBC standard; you cannot declare a variable number of placeholders. You need a number of variations with the desired number of placeholders prepared, or you need to generate the SQL string dynamically once you know how many placeholders are required. The named parameter support provided in the

`NamedParameterJdbcTemplate`

and

`JdbcTemplate`

takes the latter approach. Pass in the values as a

`java.util.List`

of primitive objects. This list will be used to insert the required placeholders and pass in the values during the statement execution.



```
@Test
public void test3() {
DataSource ds=new ComboPooledDataSource();
NamedParameterJdbcTemplate npjt=new NamedParameterJdbcTemplate(ds);
Map<String,Object> maps=new HashMap<>();
maps.put("ids", Arrays.asList(1,2,3));
List<User> users=npjt.query("select id,username from t_user where id in (:ids)", 
maps,
new BeanPropertyRowMapper<User>(User.class)
);
System.out.println(users);
}
```



