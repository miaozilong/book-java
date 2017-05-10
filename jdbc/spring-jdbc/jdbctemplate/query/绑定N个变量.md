```java
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



