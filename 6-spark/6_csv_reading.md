# Reading Options in CSV

​	When reading a CSV file with Spark, there are many options we can customize:

​	Example:

```scala
spark.read \
    .option("sep", "|") \
    .option("header", "true") \
    .option("quote", "\"") \
    .option("mode", "DROPMALFORMED") \
    .csv("hdfs:///user/test/)
```

- `sep`: defines the separator of the CSV file. `,` by default.
- `header`: boolean value to define if the CSV files have a header.
- `quote`: defines which caracter is used as quote. `"` by default.
- `mode`: defines how to deal with records with errors.
