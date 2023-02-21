# Stream Operations

​	When using ksqlDB, we can do anything we would do in a usual SQL query, such as `JOIN`, `WHERE`, `GROUP BY`, `HAVING`, `LIMIT`, etc.

## Examples

### Read data from a stream

```sql
-- to verify the content of our stream:
select * from customer limit 10;

-- to verify the structure of our stream:
describe customer;
-- or
describe extended customer;
```

### Set and unset properties

```sql
set '<property>'='<value>'
unset '<property>'
```

### Add data

```sql
insert into <stream>
(
  column_1,
  column_2
) values (
  value_1,
  value_2
);
-- or
insert into <stream>
select <...>
```

### Delete the stream

```sql
-- deletes only the stream:
drop stream customer;

-- delets the stream and its topic:
drop stream customer delete topic;

```

