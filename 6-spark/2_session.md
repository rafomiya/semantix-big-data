# Spark Session

​	With a `SparkSession` variable defined, we have access to a lot of Spark's functionalities, such as:

- `sql`: executes SparkSQL queries.
- `catalog`: manages the tables.
- `read`: reads data from a file or other data sources.
- `conf`: object to manage Spark's configs.
- `sparkContext`: Core Spark API

​	Example: most simple as possible creation of a `SparkSession` object.

```python
spark = SparkSession \
	.builder \
	.appName("example") \
	.getOrCreate()
```

## Log

​	Spark uses `log4j` for logging. Those settings are stored on the file `conf/log4j.properties`.
​	These are the main log levels:

- `TRACE`
- `DEBUG`
- `INFO`: default in spark applications.
- `WARN`: default in spark shell applications.
- `ERROR`
- `FATAL`
- `OFF`

​	Setting the log level:

```python
spark.sparkContext.setLogLevel("INFO")
```
