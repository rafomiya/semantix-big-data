# `withColumn`

​	When working with data cleaning, it is pretty common to use the `withColumn` command. It creates columns.

​	Syntax:

```python
dataframe.withColumn(column_name, column)
```

​	If the `column_name` already exists on the dataframe, the column will be replaced. If the `column_name` doesn't exist, it will be added to the dataframe.

​	Example: this snippet would just duplicate the column `id` from the dataframe.

```python
data = spark.read \
    .option("sep", "|") \
    .option("header", "true") \
    .option("quote", "\'") \
    .option("mode", "DROPMALFORMED") \
    .csv("hdfs:///user/test/")

add_column = data.withColumn("new id", col("id"))
```

## Accessing Columns

​	There are many ways to access the columns of a dataframe or dataset:

- Python:
    - `col("field")` (`from pyspark.sql.functions import col`)
    - `dataframe["field"]`
    - `dataframe.field`
- Scala:
    - `col("field")`
    - `dataframe("field")`
    - `$"field"`
