可使用execute\(...\)方法用于执行任意的SQL，通常用于DDL操作

```
this.jdbcTemplate.execute("create table mytable (id integer, name varchar(100))");
```



