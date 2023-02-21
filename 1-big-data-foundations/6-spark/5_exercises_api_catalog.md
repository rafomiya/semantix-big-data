# Exercises - API Catalog

Do the exercises using API Catalog.

1. Visualize all the databases.

```scala
spark.catalog.listDatabases.show(false)
// output:
// +-------+---------------------+--------------------------------------------------+
// |name   |description          |locationUri                                       |
// +-------+---------------------+--------------------------------------------------+
// |default|Default Hive database|hdfs://namenode:8020/user/hive/warehouse          |
// |rafael |                     |hdfs://namenode:8020/user/hive/warehouse/rafael.db|
// +-------+---------------------+--------------------------------------------------+
```

2. Define the database `rafael` as your main.

```scala
spark.catalog.setCurrentDatabase("rafael")
```

3. Visualize all the tables from `rafael`.

```scala
spark.catalog.listTables.show
// output:
// +------------------+--------+-----------+---------+-----------+
// |              name|database|description|tableType|isTemporary|
// +------------------+--------+-----------+---------+-----------+
// |             birth|  rafael|       null| EXTERNAL|      false|
// |        fees_selic|  rafael|       null|  MANAGED|      false|
// |               pop|  rafael|       null|  MANAGED|      false|
// |       pop_parquet|  rafael|       null|  MANAGED|      false|
// |pop_parquet_snappy|  rafael|       null|  MANAGED|      false|
// |           student|  rafael|       null|  MANAGED|      false|
// |            titles|  rafael|       null|  MANAGED|      false|
// +------------------+--------+-----------+---------+-----------+
```

4. Visualize the columns from the table `student`.

```scala
spark.catalog.listColumns("student").show
// output:
// +-----------------+-----------+--------+--------+-----------+--------+
// |             name|description|dataType|nullable|isPartition|isBucket|
// +-----------------+-----------+--------+--------+-----------+--------+
// |      id_discente|       null|     int|    true|      false|   false|
// |             nome|       null|  string|    true|      false|   false|
// |     ano_ingresso|       null|     int|    true|      false|   false|
// | periodo_ingresso|       null|     int|    true|      false|   false|
// |            nivel|       null|  string|    true|      false|   false|
// |id_forma_ingresso|       null|     int|    true|      false|   false|
// |         id_curso|       null|     int|    true|      false|   false|
// +-----------------+-----------+--------+--------+-----------+--------+
```

5. Visualize the first 10 rows from the table `student` using Spark SQL.

```scala
spark.sql("select * from student limit 10").show
// output:
// +-----------+--------------------+------------+----------------+-----+-----------------+--------+
// |id_discente|                nome|ano_ingresso|periodo_ingresso|nivel|id_forma_ingresso|id_curso|
// +-----------+--------------------+------------+----------------+-----+-----------------+--------+
// |      18957|ABELARDO DA SILVA...|        2017|               1|    G|            62151|   76995|
// |        553| ABIEL GODOY MARIANO|        2015|            null|    M|          2081113|    3402|
// |      17977|ABIGAIL ANTUNES S...|        2017|               1|    T|          2081111|  759711|
// |      16613|ABIGAIL FERNANDA ...|        2017|            null|    M|            37350|    1222|
// |      17398|ABIGAIL JOSIANE R...|        2017|            null|    M|            37350|    5041|
// |      26880|ABIMAEL CHRISTOPF...|        2019|               1|    T|          2081115| 1913420|
// |      28508|   ABNER NUNES PERES|        2019|               1|    G|            37350|  181097|
// |      18693|ACSA PEREIRA RODR...|        2017|               1|    G|            62151|   77498|
// |      28071|ACSA ROBALO DOS S...|        2019|               1|    T|          2081115| 3996007|
// |      21968|AÇUCENA CARVALHO ...|        2018|               0|    N|          2081113| 2399357|
// +-----------+--------------------+------------+----------------+-----+-----------------+--------+
```
