# Exercises - Dataset

1. Create the dataframe `names_us` to read the HDFS files at `/user/rafael/data/names`.

```scala
val names_us = spark.read.csv("/user/rafael/data/names")
// output:
// names_us: org.apache.spark.sql.DataFrame = [_c0: string, _c1: string ... 1 more field]
```

2. Visualize the schema of `names_us`.

```scala
names_us.printSchema
// output:
// root
//  |-- _c0: string (nullable = true)
//  |-- _c1: string (nullable = true)
//  |-- _c2: string (nullable = true)
```

3. Show the first 5 rows of `names_us`.

```scala
names_us.show(5)
// output:
// +--------+---+-----+
// |     _c0|_c1|  _c2|
// +--------+---+-----+
// |    Emma|  F|18809|
// |Isabella|  F|18612|
// |   Emily|  F|17429|
// |  Olivia|  F|17078|
// |     Ava|  F|17035|
// +--------+---+-----+
// only showing top 5 rows
```

4. Create a case class `Birth` for the data of `names_us`.

```scala
case class Birth(name: String, sex: String, quantity: Int)
// output:
// defined class Birth
```

5. Create the dataset `names_ds` to read the HDFS data at `/user/rafael/data/names`, using the case class `Birth`.

```scala
import org.apache.spark.Encoders
// output:
// import org.apache.spark.sql.Encoders

val names_schema = Encoders.product[Birth].schema
// output:
// names_schema: org.apache.spark.sql.types.StructType = StructType(StructField(name,StringType,true), StructField(sex,StringType,true), StructField(quantity,IntegerType,false))

val names_ds = spark.read.schema(names_schema).csv("/user/rafael/data/names").as[Birth]
// output:
// names_ds: org.apache.spark.sql.Dataset[Birth] = [name: string, sex: string ... 1 more field]
```

6. Visualize the schema of `names_ds`.

```scala
names_ds.printSchema
// output:
// root
//  |-- name: string (nullable = true)
//  |-- sex: string (nullable = true)
//  |-- quantity: integer (nullable = true)
```

7. Show the first 5 rows of `names_ds`.

```scala
names_ds.show(5)
// output:
// +--------+---+--------+
// |    name|sex|quantity|
// +--------+---+--------+
// |    Emma|  F|   18809|
// |Isabella|  F|   18612|
// |   Emily|  F|   17429|
// |  Olivia|  F|   17078|
// |     Ava|  F|   17035|
// +--------+---+--------+
// only showing top 5 rows
```

8. Save the dataset `names_ds` on the HDFS at `/user/rafael/names_us_parquet` on the format parquet with snappy compression

```scala
names_ds.write.option("compression", "snappy").parquet("/user/rafael/data/names_us_parquet")
```

