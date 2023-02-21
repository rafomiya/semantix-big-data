# Spark SQL vs. Spark Operations

​	Spark SQL example:

```scala
val df = spark.sql("select * from customer where id = 36")
```

​	Spark operation example:

```scala
val df = spark.read.table("customer").where("id = 36")
```

​	These two snippets above does the same thing. Spark SQL is easier to learn if you already have some previous database knowledge, although Spark operations can have more separability than the queries.
