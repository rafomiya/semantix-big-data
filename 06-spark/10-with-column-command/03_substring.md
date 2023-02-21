# Function Substring

​	As the name suggests, the function `substring` returns the substring of a given string.
​	Its parameters are: the column itself; the initial character; and the length of the result string. Note that the index of the characters starts at 1, not 0.

​	Example: create a new field `short_name`, getting only the first 4 characters of the `name`.

```python
from pyspark.sql.functions import substring, col


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

# adding the column "short_name"
person = person.withColumn("short_name", substring(col("name"), 1, 4))

person.show()
# output:
# +---+------+----------+----------+
# | id|  name| birthdate|short_name|
# +---+------+----------+----------+
# |  1|Robert|1974-12-06|      Robe|
# |  2| Annie|1996-02-21|      Anni|
# |  3|Rafael|2006-04-06|      Rafa|
# |  4|Jessie|1986-11-15|      Jess|
# +---+------+----------+----------+
```

## `substring` with `concat`

​	Another important feature is the `concat` function. It simply concatenates two strings.

​	Example: concatenating the month with the year of the previous example, in the format `month-year`:

```python
from pyspark.sql.functions import concat, lit


month_year = person.withColumn("month_year", concat(substring("birthdate", 6, 2), lit("-"), substring("birthdate", 1, 4)))
month_year.show()
# output:
# +---+------+----------+----------+
# | id|  name| birthdate|month_year|
# +---+------+----------+----------+
# |  1|Robert|06/12/1974|   12-1974|
# |  3|Rafael|06/04/2006|   04-2006|
# |  4|Jessie|15/11/1986|   11-1986|
# |  2| Annie|21/02/1996|   02-1996|
# +---+------+----------+----------+
```
