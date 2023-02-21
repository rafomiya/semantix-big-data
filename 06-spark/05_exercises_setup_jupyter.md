# Exercises - Test Jupyter Notebook

1. Create a notebook file with the name `teste_spark.ipynb`.

2. Get informations about the spark session (`spark`).

```bash
spark
# output:
# SparkContext
# 
# Spark UI
# 
# Version
# v2.4.1
# Master
# local[*]
# AppName
# pyspark-shell
```

3. Get informations about the spark context (`sc`).

```bash
sc
# output:
# SparkSession - hive
# 
# SparkContext
# 
# Spark UI
# 
# Version
# v2.4.1
# Master
# local[*]
# AppName
# pyspark-shell
```

4. Set the log as INFO.

```bash
sc.setLogLevel("INFO")
```

5. Visualize all the databases using the `catalog`.

```bash
spark.catalog.listDatabases()
# output:
# [Database(name='default', description='Default Hive database', locationUri='hdfs://namenode:8020/user/hive/warehouse')]
```

6. Read the data from `hdfs://namenode:8020/user/rafael/data/juros_selic/juros_selic.json` as a dataframe.

```bash
# this path can be reduced:
# "hdfs://namenode:8020/user/rafael/data/juros_selic/juros_selic.json"
# "hdfs://namenode/user/rafael/data/juros_selic/juros_selic.json" since 8020 is the default port
# "hdfs:///user/rafael/data/juros_selic/juros_selic.json" since the hdfs is on the namenode
# "/user/rafael/data/juros_selic/juros_selic.json" since the hdfs is the default data source
fees = spark.read.json("hdfs://namenode:8020/user/rafael/data/juros_selic/juros_selic.json")

fees.show(5)
# output:
# +----------+-----+
# |      data|valor|
# +----------+-----+
# |01/06/1986| 1.27|
# |01/07/1986| 1.95|
# |01/08/1986| 2.57|
# |01/09/1986| 2.94|
# |01/10/1986| 1.96|
# +----------+-----+
# only showing top 5 rows
```

7. Save the dataframe as `fees` on the format of a Hive table.

```bash
fees.write.saveAsTable("fees")
```

8. Visualize all the tables with the `catalog`.

```bash
spark.catalog.listTables()
# output:
# [Table(name='fees', database='default', description=None, tableType='MANAGED', isTemporary=False)]
```

9. Visualize on the HDFS the format and compression of the table `fees` on Hive.

```bash
!hdfs dfs -ls /user/hive/warehouse/fees
# output:
# Found 2 items
# -rw-r--r--   2 root supergroup          0 2022-04-10 19:58 /user/hive/warehouse/fees/_SUCCESS
# -rw-r--r--   2 root supergroup       3883 2022-04-10 19:58 /user/hive/warehouse/fees/part-00000-d3b26fa5-4756-4e57-ad0e-1b14912d9c4f-c000.snappy.parquet
```

10. Read and visualize the data from the table `fees`, using dataframe on the format of Hive table.

```bash
spark.read.table("fees").show()
# output:
# +----------+-----+
# |      data|valor|
# +----------+-----+
# |01/06/1986| 1.27|
# |01/07/1986| 1.95|
# |01/08/1986| 2.57|
# |01/09/1986| 2.94|
# |01/10/1986| 1.96|
# |01/11/1986| 2.37|
# |01/12/1986| 5.47|
# |01/01/1987|11.00|
# |01/02/1987|19.61|
# |01/03/1987|11.95|
# |01/04/1987|15.30|
# |01/05/1987|24.63|
# |01/06/1987|18.02|
# |01/07/1987| 8.91|
# |01/08/1987| 8.09|
# |01/09/1987| 7.99|
# |01/10/1987| 9.45|
# |01/11/1987|12.92|
# |01/12/1987|14.38|
# |01/01/1988|16.78|
# +----------+-----+
# only showing top 20 rows
```

11. Read and visualize the data from the table `fees`, using dataframe on the format parquet.

```bash
spark.read.parquet("/user/hive/warehouse/fees").show()
# output:
# +----------+-----+
# |      data|valor|
# +----------+-----+
# |01/06/1986| 1.27|
# |01/07/1986| 1.95|
# |01/08/1986| 2.57|
# |01/09/1986| 2.94|
# |01/10/1986| 1.96|
# |01/11/1986| 2.37|
# |01/12/1986| 5.47|
# |01/01/1987|11.00|
# |01/02/1987|19.61|
# |01/03/1987|11.95|
# |01/04/1987|15.30|
# |01/05/1987|24.63|
# |01/06/1987|18.02|
# |01/07/1987| 8.91|
# |01/08/1987| 8.09|
# |01/09/1987| 7.99|
# |01/10/1987| 9.45|
# |01/11/1987|12.92|
# |01/12/1987|14.38|
# |01/01/1988|16.78|
# +----------+-----+
# only showing top 20 rows
```

