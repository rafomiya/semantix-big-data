# Function Timestamp

​	To change the date format of a field to a new format, we need to follow this steps:

- `unix_timestamp()`: convert the value of the field to timestamp.
- `from_unixtime()`: convert the timestamp to the desired date format.

​	Example:

```python
from pyspark.sql.functions import unix_timestamp, from_unixtime, col


person.printSchema()
person.show()
# output:
# root
#  |-- id: integer (nullable = true)
#  |-- name: string (nullable = true)
#  |-- birthdate: date (nullable = true)
# 
# +---+------+----------+
# | id|  name| birthdate|
# +---+------+----------+
# |  1|Robert|1974-12-06|
# |  2| Annie|1996-02-21|
# |  3|Rafael|2006-04-06|
# |  4|Jessie|1986-11-15|
# +---+------+----------+


# changing the date format of a field:
# current format: yyyy/MM/dd
# desired format: MM-dd-yyyy

dates = person.select(col("id"), col("birthdate")) # works just like `select("id", "birthdate")`

# creates a timestamp field called "timestamp" equivalent to the `birthdate` field
dates_timestamp = dates.withColumn("timestamp", unix_timestamp(col("birthdate"), "yyyy-MM-dd"))

# creates a string field called "new_birthdate" equivalent to the `timestamp` field
dates_desired = dates_timestamp.withColumn("new_birthdate", from_unixtime(col("timestamp"), "dd/MM/yyyy"))

dates_desired.show()
dates_desired.printSchema()
# output:
# +---+----------+----------+-------------+
# | id| birthdate| timestamp|new_birthdate|
# +---+----------+----------+-------------+
# |  1|1974-12-06| 155520000|   06/12/1974|
# |  2|1996-02-21| 824860800|   21/02/1996|
# |  3|2006-04-06|1144281600|   06/04/2006|
# |  4|1986-11-15| 532396800|   15/11/1986|
# +---+----------+----------+-------------+
# 
# root
#  |-- id: integer (nullable = true)
#  |-- birthdate: date (nullable = true)
#  |-- timestamp: long (nullable = true)
#  |-- new_birthdate: string (nullable = true)


# doing it with a single line of code:
dates = person.select("id", "birthdate").withColumn("birthdate", from_unixtime(unix_timestamp(col("birthdate"), "yyyy-MM-dd"), "dd/MM/yyyy"))

dates.printSchema()
dates.show()
# output:
# root
#  |-- id: integer (nullable = true)
#  |-- birthdate: string (nullable = true)
# 
# +---+----------+
# | id| birthdate|
# +---+----------+
# |  1|06/12/1974|
# |  2|21/02/1996|
# |  3|06/04/2006|
# |  4|15/11/1986|
# +---+----------+
```
