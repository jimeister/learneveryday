# Group Concat in Postgres

MySQL has a built-in function [`group_concat`](http://dev.mysql.com/doc/refman/5.7/en/group-by-functions.html#function_group-concat) which can automatically group non-null results from a group into a string. To get the equivalent functionality in Postgres 9.0 or later, use the following:

```
SELECT id, 
       string_agg(some_column, ',')
FROM the_table
GROUP BY id
```

[reference](http://stackoverflow.com/a/8803563)
