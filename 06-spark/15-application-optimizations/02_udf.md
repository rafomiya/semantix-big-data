# User Defined Functions

​	It is possible to define a function and use it in SparkSQL's dataframes or datasets:

```python
spark.udf.register(udf_name, func)
```

## SparkSQL Example

​	When creating a UDF to be used in Spark SQL, we need to follow 3 simple steps:

- create the function object.
- register it with a name through `spark.udf`.
- use it with the registered name inside `spark.sql` queries.

​	OBS: `spark.range(x, y)` creates a dataset with only a field `id`, going from x to y.

```python
# defining the function
square = lambda s: s * s

# registering the UDF
spark.udf.register("square", square)

# creating a temp test table
spark.range(1, 20).registerTempTable("test")

# executing a SparkSQL query
spark.sql("select id, square(id) as square_id from test")
# output:
# +---+---------+
# | id|square_id|
# +---+---------+
# |  1|        1|
# |  2|        4|
# |  3|        9|
# |  4|       16|
# |  5|       25|
# |  6|       36|
# |  7|       49|
# |  8|       64|
# |  9|       81|
# | 10|      100|
# | 11|      121|
# | 12|      144|
# | 13|      169|
# | 14|      196|
# | 15|      225|
# | 16|      256|
# | 17|      289|
# | 18|      324|
# | 19|      361|
# +---+---------+
```

## Dataframe Example

​	When creating a UDF to be used in dataframes/datasets operations, we need to follow 3 simple steps:

- import `udf` from `sql.functions`
- create the function object and pass it to the `udf`, creating a UDF object.
- apply it as any other transformation.

```python
# importing the necessary stuff
from pyspark.sql import functions as F


# defining the transformation
square = F.udf(lambda s: s * s)

# applying it
spark.range(1, 20).select(
    F.col("id"),
    square(F.col("id")).alias("square_id")
)
# output:
# +---+---------+
# | id|square_id|
# +---+---------+
# |  1|        1|
# |  2|        4|
# |  3|        9|
# |  4|       16|
# |  5|       25|
# |  6|       36|
# |  7|       49|
# |  8|       64|
# |  9|       81|
# | 10|      100|
# | 11|      121|
# | 12|      144|
# | 13|      169|
# | 14|      196|
# | 15|      225|
# | 16|      256|
# | 17|      289|
# | 18|      324|
# | 19|      361|
# +---+---------+
```

## Do you need to create a UDF?

​	Be careful so you don't end up reinventing the wheel.
