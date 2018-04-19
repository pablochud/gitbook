Przy wprowadzaniu constrainów typu Unique - \(typem takim jest również PRIMARY KEY\) automatycznie zakładany jest index. Można wymusić by dla kolumny z constrain unique index nie był typu unique.

Hint /\*result cashe\*/ - dla enterprice edition, optymalizator mówi: weź selecta z casha.

```
create table t
as
select * from all_objects;
```

```
exec dbms_stats.gather_table_stats( user, 'T', cascade=>true );
```

```
delete from plan_table;
```

```
explain plan for delete from t where created<to_date('01-jan-2009');
```

```
select * from table(dbms_xplan.display);
```



