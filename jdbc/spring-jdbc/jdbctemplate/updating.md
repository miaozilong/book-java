使用update\(...\)方法可用于insert,update和delete操作，数据操作的参数通常使用该方法的args形参或使用一组对象传入

```java
this.jdbcTemplate.update(
        "insert into t_actor (first_name, last_name) values (?, ?)",
        "Leonor", "Watling");
```

```java
this.jdbcTemplate.update(
        "update t_actor set last_name = ? where id = ?",
        "Banjo", 5276L);
```

```java
this.jdbcTemplate.update(
        "delete from actor where id = ?",
        Long.valueOf(actorId));
```



