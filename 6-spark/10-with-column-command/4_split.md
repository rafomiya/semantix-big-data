# Function Split

​	`split` is a function that takes a string and a delimiter, and returns an array of strings, breaking the original string into pieces according to the delimiter.
​	Example: OBS: that's a pseudo-code.

```python
split("aoba yoba nairobi", " ") => ["aoba", "yoba", "nairobi"]
split("prefixes are for fouls", "e") => ["pr", "fix", "s ar", " for fouls"]
```

​	Syntax:

```python
dataframe.withColumn(new_column_name, split(column, delimiter))
```

​	Example:

```python
from pyspark.sql.functions import split


splitted_names = names.withColumn("splitted_name", split(col("fullname"), " "))

splitted_names.printSchema()
# root
#  |-- id: integer (nullable = true)
#  |-- name: string (nullable = true)
#  |-- splitted_name: array (nullable = true)

first_names = splitted_names.withColumn("first_name", col("splitted_name").getItem(0)).drop("splitted_name")
```
