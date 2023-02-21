# Exercises - Functions II

1. Create a dataframe to read the file on HDFS at `/user/rafael/data/juros_selic/juros_selic`.

```python
fees = spark.read.csv("hdfs://namenode:8020/user/rafael/data/juros_selic/juros_selic", header=True, sep=";")
fees.show(5)
# output:
# +----------+-----+
# |      data|valor|
# +----------+-----+
# |01/06/1986| 1,27|
# |01/07/1986| 1,95|
# |01/08/1986| 2,57|
# |01/09/1986| 2,94|
# |01/10/1986| 1,96|
# +----------+-----+
# only showing top 5 rows
```

2. Group all the dates by the year in descending order and save the amount of months ocurred, the average value, minimum and maximum of the field value with the following structure:

|Anual|Months|Average value|Minimum value|Maximum value|
|-----|------|-------------|-------------|-------------|
| 2019|     2|          0.0|          0.0|          0.0|
| 2018|    12|          0.0|          0.0|          0.0|
| 2017|    12|          0.0|          0.0|          0.0|
|  ...|   ...|          0.0|          0.0|          0.0|
| 1986|     2|          0.0|          0.0|          0.0|

```python
from pyspark.sql import functions as F
from pyspark.sql.types import IntegerType, FloatType


# creating a field `year`, as an `Integer` and ordering by year desc
fees = fees.withColumn("year", F.substring(F.col("data"), 7, 4).cast(IntegerType()))
fees.show(5)
# output:
# +----------+-----+----+
# |      data|valor|year|
# +----------+-----+----+
# |01/06/1986| 1,27|1986|
# |01/07/1986| 1,95|1986|
# |01/08/1986| 2,57|1986|
# |01/09/1986| 2,94|1986|
# |01/10/1986| 1,96|1986|
# +----------+-----+----+
# only showing top 5 rows

# transforming the field `valor` into a Float, and renaming it to `value`
fees = fees.withColumn("value", F.regexp_replace(F.col("valor"), ",", ".").cast(FloatType())).drop("valor")
fees.printSchema()
# output:
# root
#  |-- data: string (nullable = true)
#  |-- year: integer (nullable = true)
#  |-- value: float (nullable = true)

# replacing the field `data` for the field `month`, of type Integer
fees = fees.withColumn("month", F.substring(F.col("data"), 4, 2).cast(IntegerType())).drop("data")
fees.show(5)
# output:
# +----+-----+-----+
# |year|value|month|
# +----+-----+-----+
# |1986| 1.27|    6|
# |1986| 1.95|    7|
# |1986| 2.57|    8|
# |1986| 2.94|    9|
# |1986| 1.96|   10|
# +----+-----+-----+
# only showing top 5 rows

# creating the requested view
result = fees.groupBy(F.col("year").alias("Annual")).agg(
    F.countDistinct(F.col("month")).alias("Months"),
    F.avg(F.col("value")).alias("Average value"),
    F.min(F.col("value")).alias("Minimum value"),
    F.max(F.col("value")).alias("Maximum value")
).orderBy(-F.col("Annual"))

result.printSchema()
result.show(5)
# output:
# root
#  |-- Annual: integer (nullable = true)
#  |-- Months: long (nullable = false)
#  |-- Average value: double (nullable = true)
#  |-- Minimum value: float (nullable = true)
#  |-- Maximum value: float (nullable = true)
# 
# +------+------+-------------------+-------------+-------------+
# |Annual|Months|      Average value|Minimum value|Maximum value|
# +------+------+-------------------+-------------+-------------+
# |  2019|     2|0.45500001311302185|         0.37|         0.54|
# |  2018|    12| 0.5199999958276749|         0.47|         0.58|
# |  2017|    12| 0.7941666692495346|         0.54|         1.09|
# |  2016|    12|  1.099999984105428|          1.0|         1.22|
# |  2015|    12| 1.0449999918540318|         0.82|         1.18|
# +------+------+-------------------+-------------+-------------+
# only showing top 5 rows

```

3. Save on `hdfs:///user/rafael/relatorioAnual` with zlib compression and orc format.

```python
result.write.orc("hdfs:///user/rafael/relatorioAnual", compression="zlib", mode="overwrite")
```

```bash
hdfs dfs -ls /user/rafael/relatorioAnual
# output:
# Found 35 items
# -rw-r--r--   2 root supergroup          0 2022-04-20 17:05 /user/rafael/relatorioAnual/_SUCCESS
# -rw-r--r--   2 root supergroup        583 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00000-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        586 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00001-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        586 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00002-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        584 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00003-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        591 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00004-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        592 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00005-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        584 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00006-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        592 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00007-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        594 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00008-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        594 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00009-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        581 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00010-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        591 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00011-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        575 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00012-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        586 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00013-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        589 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00014-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        593 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00015-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        593 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00016-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        579 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00017-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        588 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00018-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        591 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00019-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        594 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00020-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        583 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00021-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        592 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00022-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        593 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00023-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        582 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00024-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        592 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00025-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        586 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00026-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        583 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00027-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        587 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00028-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        591 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00029-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        589 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00030-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        591 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00031-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        586 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00032-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
# -rw-r--r--   2 root supergroup        588 2022-04-20 17:05 /user/rafael/relatorioAnual/part-00033-73dbbc8d-107a-4e9d-8cf6-79a00007d6d5-c000.zlib.orc
```
