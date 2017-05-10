可使用execute\(...\)方法用于执行任意的SQL，通常用于DDL操作

```
this.jdbcTemplate.execute("create table mytable (id integer, name varchar(100))");
```

```
this.jdbcTemplate.update(
        "call SUPPORT.REFRESH_ACTORS_SUMMARY(?)",
        Long.valueOf(unionId));
```

该方法不返回任何值

