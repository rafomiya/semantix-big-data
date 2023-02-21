# Spark SQL

​	Spark SQL is a way of accessing the data from within a dataframe, but instead of using actions and transformations, using SQL.

​	Example:

```scala
val customerView = spark.sql("select name, age from people")  // returns a dataframe
customerView.printSchema
```

​	But where is the `people` table? It is inside a Hive, stored on the HDFS. If the data source is a file, we do as follows:

```scala
val customerView = spark.sql("select name, age from parquet.`/bd/people.parquet`")
// kinda ugly, right?
```

Example query:

```scala
val query = """
select
	mean(age) as mean_age,
	stddev(age) as sdev_age
from people
where pcode in
(
	select pcode from pcodes where state='MA'
)"""

val maAgeDf = spark.sql(query)
```

​	Many other SQL resources can be used, such as:

- `select`
- `where`
- `group by`
- `having`
- `order by`
- `limit`
- `count`
- `sum`
- `mean`
- `as`
- subqueries

## Views

​	Views are pretty much `select`s from a database, stored inside a table so you don't need to rewrite the same SQL query every time. In Spark, views are temporary.

​	Syntax:

```scala
df.createTempView("<viewname>")
// or
df.createOrReplaceTempView("<viewname>")
// or
df.createGlobalTempView()
```

​	Example:

```scala
val customerDf = spark.read.json("customer.json").createTempView("customerView")
spark.sql("select * from customrView").show(10)
```
