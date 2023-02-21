# Stream Aggregations

​	Differently from usual SQL aggregations, all the aggregations need a `group by`.
​	For instance, if we want to count the amount of rows in a topic, what we would try to do is:

```sql
select count(*) from topic
```

​	That would throw an exception. The correct way to do so is using a field always set to 1 in all the messages, and then counting with a `group by`:

```sql
-- creating the stream with the 1 field
create stream stream_to_count as
select 1 as unit from <streamname>;

-- counting using this new stream
select count(unit)
from stream_to_count
group by unit;
```
