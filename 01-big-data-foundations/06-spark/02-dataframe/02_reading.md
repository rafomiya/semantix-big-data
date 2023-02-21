# File Reading

​	File formats supported for writing and reading on a dataframe:

- Textfiles:
  - CSV.
  - JSON.
  - Plain text.
- Binary files:
  - Parquet (very used).
  - ORC.
- Tables:
  - Hive metastore.
  - JDBC
- Other configured types.

## Reading a file on Scala

```scala
val <dataframe> = spark.read.<format>("<file>")
```

​	Possible formats:

- `textFile("file.txt")`
- `csv("file.csv")`
- `jdbc(jdbcUrl, "bd.table", connectionProperties)`
- `load` or `parquet("file.parquet")`
  - Parquet is the default file format for Spark, so `load()` and `parquet()` are equivalents.

- `table("hiveTable")`
- `json("file.json")`
- `orc("file.orc")`

​	Possible files:

- `directory/`
- `directory/*.log`
- `file1.txt, file2.txt`
- `file*`

​	Another way:

```scala
val userDataFrame = spark.read.json("user.json")
// or
val userDataFrame = spark.read.format("json").load("user.json")
```

