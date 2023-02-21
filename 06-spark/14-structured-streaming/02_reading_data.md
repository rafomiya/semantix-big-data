# Reading Data

​	Example: reading a stream on `localhost:9999`:

```python
# dataframe
read_str = spark.readStream \
    .format("socket") \
    .option("host", "localhost") \
    .option("port", 9999) \
    .load()

# desired opearations goes here

write_str = read_str.writeStream.format("console").start()
```

​	Example: reading a CSV file on `localhost:9999`:

```python
# the definition of a schema is mandatory
user_schema = StructType([StructField("name", StringType()), StructField("age", IntegerType())])
# or
user_schema = StructType().add("name", "string").add("age", "integer")

# it is also mandatory to point to a directory
# on the `path` parameter of the `csv` method
read_csv_df = spark.readStream \
    .schema(user_schema) \
    .csv("/user/rafael/names")

read_csv_df.printSchema()
```

​	Example: saving data:

```python
read_csv_df.writeStream \
    .format("csv") \
    .option("checkpointLocation", "/tmp/checkpoint")
    .option("path", "/home/data") \
    .start()
```