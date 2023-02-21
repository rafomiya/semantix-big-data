# Exercises - Structured Streaming

1. Create an application in Scala using Spark Structured Streaming to read the data from the port `9999` and show it on the console.

```scala
val streamDf = spark.readStream.format("socket").option("host", "localhost").option("port", 9999).load()

val writeStream = streamDf.writeStream.format("console").start()
// output: (data sent through netcat)
// 22/04/24 08:24:50 WARN sources.TextSocketSourceProvider: The socket source should not be used for production applications! It does not support recovery.
// writeStream: org.apache.spark.sql.streaming.StreamingQuery = org.apache.spark.sql.execution.streaming.StreamingQueryWrapper@29922188
// 
// -------------------------------------------                                     
// Batch: 0
// -------------------------------------------
// +-----+
// |value|
// +-----+
// +-----+
// 
// -------------------------------------------
// Batch: 1
// -------------------------------------------
// +-----+
// |value|
// +-----+
// |    a|
// +-----+
// 
// -------------------------------------------
// Batch: 2
// -------------------------------------------
// +-----+
// |value|
// +-----+
// |    b|
// +-----+
// 
// -------------------------------------------
// Batch: 3
// -------------------------------------------
// +-----+
// |value|
// +-----+
// |    c|
// +-----+
// 
// -------------------------------------------
// Batch: 4
// -------------------------------------------
// +-----+
// |value|
// +-----+
// |    d|
// +-----+
// 
// -------------------------------------------
// Batch: 5
// -------------------------------------------
// +-----+
// |value|
// +-----+
// |    e|
// |    f|
// +-----+
// 
// -------------------------------------------
// Batch: 6
// -------------------------------------------
// +-----+
// |value|
// +-----+
// |    g|
// |    h|
// +-----+
// 
// 22/04/24 08:25:07 WARN sources.TextSocketMicroBatchReader: Stream closed by localhost:9999
```

2. Read the CSV files at `hdfs://namenode:8020/user/rafael/data/iris/*.data` with the following schema:

- `sepal_length`: `float`
- `sepal_width`: `float`
- `petal_length`: `float`
- `petal_width`: `float`
- `class`: `string`

```scala
import org.apache.spark.sql.types.{StructType, StructField, FloatType, StringType}


val irisSchema = StructType(Seq(
    StructField("sepal_length", FloatType),
    StructField("sepal_width", FloatType),
    StructField("petal_length", FloatType),
    StructField("petal_width", FloatType),
    StructField("class", StringType)
))

val irisDf = spark.readStream.schema(irisSchema).csv("hdfs://namenode:8020/user/rafael/data/iris/*.data")
```

3. Visualize the schema of the informations.

```scala
irisDf.printSchema
// output:
// root
//  |-- sepal_length: float (nullable = true)
//  |-- sepal_width: float (nullable = true)
//  |-- petal_length: float (nullable = true)
//  |-- petal_width: float (nullable = true)
//  |-- class: string (nullable = true)
```

4. Save the data on the directory `hdfs://namenode:8020/user/rafael/stream_iris/path` and the checkpoint at `hdfs://namenode:8020/user/rafael/stream_iris/check`.

```scala
val irisOut = irisDf.writeStream.format("csv").option("checkpointLocation", "/user/rafael/stream_iris/check").option("path", "/user/rafael/stream_iris/path").start()
```

5. Verify the output on the HDFS and understand how the data was saved.

```bash
hdfs dfs -ls /user/rafael/stream_iris/path
# output:
# Found 3 items
# drwxr-xr-x   - root supergroup          0 2022-04-24 08:56 /user/rafael/stream_iris/path/_spark_metadata
# -rw-r--r--   2 root supergroup       4550 2022-04-24 08:56 /user/rafael/stream_iris/path/part-00000-563288da-0abb-4282-83d7-03181912872f-c000.csv
# -rw-r--r--   2 root supergroup       4550 2022-04-24 08:56 /user/rafael/stream_iris/path/part-00001-7c6d84eb-62df-4bcb-bac6-6eeb14f9afde-c000.csv
```

6. Bonus: Count the amount of words of the exercise 1.

```scala
// creating the stream to receive the words
val input = spark.readStream.format("socket").option("host", "localhost").option("port", 9999).load()

// flattening the df to get words "alone"
val words = input.withColumn("value", lower(col("value"))).as[String].flatMap(_.split(" "))

// getting word count
val counts = words.groupBy("value").count()

// creating a query 
val query = counts.writeStream.outputMode("complete").format("console").start()

query.awaitTermination()
```
